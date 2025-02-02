---
title:  "[Unity] 유니티에서 오브젝트 풀(Object Pool) 사용하는 방법과 기본 개념 정리"
excerpt: Unity Object Pool

categories:
  - Unity Code
tags:
  - [Unity, Object Pool, 오브젝트 풀, Unity 공식지원]

toc: true
toc_sticky: true
 
date: 2022-08-13
last_modified_at: 2022-08-13
---

## 오브젝트 풀(Object Pool) 개념
그냥 생성 -> 삭제라는 형식을 사용할 경우 아래의 2가지 문제점이 발생 하기 때문에 이를 해소 하기 위해 미리 생성을 해서 'Pool'에 저장하여 메모리를 확보 후 이것을 먼저 사용, 사용후에 'Pool'에 반환하는 형식입니다.

* 메모리의 파편화(메모리는 존재하지만 할당이 불가능한 상태)
* 메모리 누수(메모리를 할당, 해제를 반복하면서 발생)

---

### 일반적인 방법
---
<br>

1. 풀 생성 및 사용과 반환 함수 작성
2. 초기에 일정 갯수만큼 생성하여 풀에 저장
3. 풀에서 꺼내오고 반환하기


#### 코드
---
<br>

오브젝트 풀은 어디에서든 접근하여 오브젝트를 생성해야하는 경우가 많기 때문에 싱글톤 패턴으로 구현하는 경우가 많이 있습니다. <br>
그리고, Pooling으로 생성할 오브젝트의 Prefab을 가지고 있어야 합니다. <br>
왜냐하면 처음 생성한 오브젝트를 모두 꺼내고 나서 꺼낸 오브젝트를 돌려받기 전에 오브젝트를 요청 받았을 때 새로운 오브젝트를 생성하여 꺼내기 위해서 입니다. <br>

```c#
public static ObjectPool _instance;

[SerializeField] GameObject _poolObjPrefab;
private void Awake()
{
    _instance = this;
    Initialize(10);
}
```
<br>

큐를 이용하여 생성된 총알 오브젝트를 관리합니다. <br>
여기서 관리하는 방법은 큐가 아니라 리스트등을 이용하셔도 상관없습니다.<br>
```c#
Queue<Bullet> _poolObjQueue = new Queue<Bullet>();
```
<br>

Initialze함수에서는 매개변수로 받은 초기화 갯수 값에 따라서 CreateObject함수를 호출하고<br>
만들어진 새로운 총알 오브젝트를 pooling Object Queue에 넣습니다.<br>
이렇게 게임이 시작하기 전에 사용될 게임 오브젝트를 미리 적절한 갯수를 만들어줌 으로써 게임 플레이 도중에 발생할 과부하를 게임 준비 과정인 로딩화면으로 돌릴 수 있습니다.<br>
```c#
private void Initialize(int initCount)
{
    for(int count = 0; count < initCount; count++) {
        _poolObjQueue.Enqueue(CreateObject());
    }
}
```
<br>

CreateObject함수는 _poolObjPrefab으로부터 새 게임 오브젝트를 만든 뒤 비활성화해서 반환하는 역할을 합니다. <br>
이렇게 생성 하자마자 비활성화 하는 이유는 아직 사용되지 않은 오브젝트를 플레이어의 눈에 띄지 않게 하기 때문입니다. <br>

```c#
private Bullet CreateObject()
{
    var newObj = Instantiate(_poolObjPrefab).GetComponent<Bullet>();
    newObj.gameObject.SetActive(false);
    newObj.transform.SetParent(transform);
    return newObj;
}
```
<br>

GetObject함수는 ObjectPool이 가지고 있는 게임 오브젝트를 요청한 자에게 꺼내주는 역할을 합니다. <br>
단, 모든 오브젝트를 꺼내서 빌려줄 오브젝트가 없는 상태라면 CreateObject함수를 호출해서 새로운 오브젝트를 생성해서 빌려줍니다. <br>
```c#
public static Bullet GetObject()
{
    if(_instance._poolObjQueue.Count > 0) {
        var obj = _instance._poolObjQueue.Dequeue();
        obj.transform.SetParent(null);
        obj.gameObject.SetActive(true);
        return obj;
    } else {
        var newObj = _instance.CreateObject();
        newObj.gameObject.SetActive(true);
        newObj.transform.SetParent(null);
        return newObj;
    }
}
```
<br>

ReturnObject함수는 빌려준 오브젝트를 돌려받아 비활성화한 뒤 정리하는 함수 입니다.
```c#
public static void ReturnObject(Bullet obj)
{
    obj.gameObject.SetActive(false);
    obj.transform.SetParent(_instance.transform);
    _instance._poolObjQueue.Enqueue(obj);
}
```
<br>


전체 코드
```c#
public class ObjectPool : MonoBehaviour
{
    public static ObjectPool _instance;

    [SerializeField] GameObject _poolObjPrefab;
    Queue<Bullet> _poolObjQueue = new Queue<Bullet>();

    private void Awake()
    {
        _instance = this;
        Initialize(10);
    }

    private void Initialize(int initCount)
    {
        for(int count = 0; count < initCount; count++) {
            _poolObjQueue.Enqueue(CreateNewObject());
        }
    }

    private Bullet CreateNewObject()
    {
        var newObj = Instantiate(_poolObjPrefab).GetComponent<Bullet>();
        newObj.gameObject.SetActive(false);
        newObj.transform.SetParent(transform);
        return newObj;
    }

    public static Bullet GetObject()
    {
        if(_instance._poolObjQueue.Count > 0) {
            var obj = _instance._poolObjQueue.Dequeue();
            obj.transform.SetParent(null);
            obj.gameObject.SetActive(true);
            return obj;
        } else {
            var newObj = _instance.CreateNewObject();
            newObj.gameObject.SetActive(true);
            newObj.transform.SetParent(null);
            return newObj;
        }
    }

    public static void ReturnObject(Bullet obj)
    {
        obj.gameObject.SetActive(false);
        obj.transform.SetParent(_instance.transform);
        _instance._poolObjQueue.Enqueue(obj);
    }
}
```

### 유니티 공식 지원 오브젝트 풀
---
<br>

1. 네임스페이스 pool선언
2. Pool에 넣을 오브젝트 지정
3. 사용, 반환, 오브젝트를 빌려올 함수 지정
4. pool을 new하고 파라메터로 오브젝트와 3번의 함수들, 초기 생성 및 저장 할 갯수를 지정
5. 실제 사용
   
#### 코드
---
<br>

먼저, Unity가 지원하는 ObjectPool을 사용하기 위해서는 아래와 같이 pool 네임스페이스를 Pooling을 사용할 주체와 사용될 오브젝트에 선언해주어야 합니다. <br>
```c#
using UnityEngine.Pool;
```
<br>

그 다음, Pooling을 사용할 주체에서 생성, 반환, Pool에서 오브젝트를 빌려올 함수를 작성해 줍니다. <br>
```c#
private Bullet CreateBullet()
{
    Bullet bullet = Instantiate(_bulletPrefab, transform.position, Quaternion.identity);
    bullet.SetPool(_bulletPool);
    return bullet;
}

private void OnGetBullet(Bullet bullet)
{
    bullet.gameObject.SetActive(true);
    bullet.transform.position = transform.position;
}

private void OnReleaseBullet(Bullet bullet)
{
    bullet.gameObject.SetActive(false);
}

private void OnDestroyBullet(Bullet bullet)
{
    Destroy(bullet.gameObject);
}
```
<br>

멤버 변수로 총알 오브젝트들을 관리할 IObjectPool<객체> 타입의 변수를 선언해줍니다.<br>
그리고 Awake 함수를 만들어서 IObjectPool<객체> 타입의 멤버 변수에 ObjectPool을 생성하고, <br>
상기에서 작성한 사용, 반환, 오브젝트를 빌려올 함수와 초기에 생성 및 저장할 갯수를 매개 변수로 넣어줍니다.<br>
```c#
[SerializeField] private Bullet _bulletPrefab;

private IObjectPool<Bullet> _bulletPool;

private void Awake()
{
    _bulletPool = new ObjectPool<Bullet>(CreateBullet, OnGetBullet, OnReleaseBullet, OnDestroyBullet, maxSize: 5);
}
```
<br>

대상 오브젝트에서 IObjectPool<객체> 타입으로 이 오브젝트를 관리 중인 Pool을 캐싱할 멤버 변수를 선언합니다. <br>
그리고 SetPool함수를 만들고 매개변수로 받은 풀을 IObjectPool<객체> 타입의 멤버 변수에 저장하도록 만들어줍니다.<br>
```c#
[SerializeField] private Vector3 _speed;
private IObjectPool<Bullet> _pool;

public void SetPool(IObjectPool<Bullet> pool)
{
    _pool = pool;
}
```
<br>

그 다음에는 OnBecameInvisible함수를 만들고 호출되면 오브젝트를 Pool에 반환하도록 코드를 작성합니다.<br>
```c#
private void OnBecameInvisible()
{
    _pool?.Release(this);
}
```
<br>


전체 코드

ObjectPool을 이용하는 주체 <br>
```c#
[SerializeField] private Bullet _bulletPrefab;

private IObjectPool<Bullet> _bulletPool;

private void Awake()
{
    _bulletPool = new ObjectPool<Bullet>(CreateBullet, OnGetBullet, OnReleaseBullet, OnDestroyBullet, maxSize: 5);
}


private Bullet CreateBullet()
{
    Bullet bullet = Instantiate(_bulletPrefab, transform.position, Quaternion.identity);
    bullet.SetPool(_bulletPool);
    return bullet;
}

private void OnGetBullet(Bullet bullet)
{
    bullet.gameObject.SetActive(true);
    bullet.transform.position = transform.position;
}

private void OnReleaseBullet(Bullet bullet)
{
    bullet.gameObject.SetActive(false);
}

private void OnDestroyBullet(Bullet bullet)
{
    Destroy(bullet.gameObject);
}

private void Update()
{
    if (Input.GetKeyDown(KeyCode.Space)){
         _bulletPool?.Get();
    }
}
```
<br>

대상 오브젝트 <br>
```c#
using UnityEngine;
using UnityEngine.Pool;

public class Bullet : MonoBehaviour
{
    [SerializeField] private Vector3 _speed;
    private IObjectPool<Bullet> _pool;

    public void SetPool(IObjectPool<Bullet> pool)
    {
        _pool = pool;
    }

    private void Update()
    {
        transform.position += _speed * Time.deltaTime;
    }

    private void OnBecameInvisible()
    {
        _pool?.Release(this);
    }
}
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}
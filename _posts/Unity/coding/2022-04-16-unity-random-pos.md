---
title:  "[Unity] "Unity에서 랜덤 좌표에 생성 및 좌표 이동"
excerpt: GameObject Random Instantiate in Unity

categories:
  - Unity Code
tags:
  - [Unity, Random Pos, 랜덤 생성, 랜덤 좌표]

toc: true
toc_sticky: true
 
date: 2022-04-16
last_modified_at: 2022-04-16
---

## *개요*
게임 개발에서 랜덤 좌표에 게임오브젝트를 생성해야될 때가 있습니다.(몬스터, 보스의 범위공격 등등)
기초적인 부분이지만 한번 짚고 가도록 하겠습니다.

---
## *순서*
1. 생성할 영역을 지정
2. 좌표를 랜덤으로 지정
3. 지정한 랜덤 좌표에 오브젝트를 생성(이미 생성되있는 오브젝트에 랜덤 좌표 입력)
 
---
### *예제*

---
#### **선언**<br> 
``` C#
    #region private
    [SerializeField] GameObject m_prefab;
    [SerializeField] BoxCollider m_area;
    [SerializeField] Button m_random_button;
    [SerializeField] Button m_init_button;
    [SerializeField] int m_count;

    bool m_isExist;
    List<GameObject> m_cubelist;

    #endregion
```

사용할 오브젝트, 전역변수, 지정영역을 선언 <br>
m_prefab : Prefab화한 게임오브젝트 <br>
m_area : 오브젝트를 생성할 지정영역 <br>
m_random_button : 좌표를 랜덤으로 생성하는 버튼 <br>
m_init_button : 초기화 버튼 <br>
m_count : 몇개의 오브젝트를 생성할것인지를 Editor상의 Component에서 정하기 <br>
m_isExist : 오브젝트가 생성되었는지 아닌지를 판단할 플래그 <br>
m_cubelist : 생성한 오브젝트를 관리할 리스트 <br>
<br>

---
#### **영역 및 랜덤 좌표 지정 부분** <br>
``` C#
    /// <summary>
    /// Calculate Random Pos
    /// </summary>
    /// <returns>Vector3 type Pos</returns>
    private Vector3 CalcRandomPos()
    {
        Vector3 _prefab_size = m_prefab.GetComponent<Transform>().localScale;
        Vector3 _size = m_area.size;

        float _pos_x = Random.Range(-20,20) + Random.Range(-_size.x/2f, _size.x/2f) + _prefab_size.x;
        float _pos_z = Random.Range(-20,20) + Random.Range(-_size.z/2f, _size.z/2f) + _prefab_size.z;

        return new Vector3(_pos_x, 1, _pos_z);
    }
``` 
<br>

---
#### **Initialize및 오브젝트 생성 부분** <br>
``` C#
    private void Initializa()
    {
        m_random_button.onClick.AddListener(OnPushRandomButton);
        m_init_button.onClick.AddListener(OnPushInitButton);

        m_cubelist = new List<GameObject>();
        m_isExist = false;
    }

    /// <summary>
    /// Activate When Press Random Button
    /// </summary>
    private void OnPushRandomButton()
    {
        var random_pos = Vector3.zero;
        GameObject _instance;

        // if already Instantiate Object, or not
        if (!m_isExist) {
            m_isExist = true;
            for (int count = 0; count < m_count; count++) {
                random_pos = CalcRandomPos();
                _instance = Instantiate(m_prefab, random_pos, Quaternion.identity);
                m_cubelist.Add(_instance);
            }
        } else {
            // if already Exist, change Pos
            for(int count = 0; count < m_count; count++) {
                m_cubelist[count].transform.position = CalcRandomPos();
            }
        }
    }
``` 

초기화함수에서 버튼을 누르면 실행할 함수를 지정하고 리스트 및 플래그등을 초기화<br>
OnpushRandomButton()함수내에서 생성할때 아래의 지역변수 randonPos 를 선언하지 않고 CalcRandomPos()함수를 Instantiate에 바로 넣어도 상관은 없으나, <br>
가독성의 문제로 지역변수를 선언-> Instantiate에 넣는 방식으로 하였습니다. <br> <br>
``` C#
/// <summary>
    /// Activate When Press Random Button
    /// </summary>
    private void OnPushRandomButton()
    {
        var random_pos = Vector3.zero;
        GameObject _instance;

        // if already Instantiate Object, or not
        if (!m_isExist) {
            m_isExist = true;
            for (int count = 0; count < m_count; count++) {
                random_pos = CalcRandomPos();
                _instance = Instantiate(m_prefab, random_pos, Quaternion.identity);
                m_cubelist.Add(_instance);
            }
        } else {
            // if already Exist, change Pos
            for(int count = 0; count < m_count; count++) {
                m_cubelist[count].transform.position = CalcRandomPos();
            }
        }
    }
``` 

---
#### **전체 코드** <br>
``` C#
public class GameManager : MonoBehaviour
{
    #region private
    [SerializeField] GameObject m_prefab;
    [SerializeField] BoxCollider m_area;
    [SerializeField] Button m_random_button;
    [SerializeField] Button m_init_button;
    [SerializeField] int m_count;

    bool m_isExist;
    List<GameObject> m_cubelist;


    #endregion

    private void Awake()
    {
        Initializa();
    }

    private void Initializa()
    {
        m_random_button.onClick.AddListener(OnPushRandomButton);
        m_init_button.onClick.AddListener(OnPushInitButton);

        m_cubelist = new List<GameObject>();
        m_isExist = false;
    }

    /// <summary>
    /// Activate When Press Random Button
    /// </summary>
    private void OnPushRandomButton()
    {
        var random_pos = Vector3.zero;
        GameObject _instance;

        // if already Instantiate Object, or not
        if (!m_isExist) {
            m_isExist = true;
            for (int count = 0; count < m_count; count++) {
                random_pos = CalcRandomPos();
                _instance = Instantiate(m_prefab, random_pos, Quaternion.identity);
                m_cubelist.Add(_instance);
            }
        } else {
            // if already Exist, change Pos
            for(int count = 0; count < m_count; count++) {
                m_cubelist[count].transform.position = CalcRandomPos();
            }
        }
    }

    /// <summary>
    /// Calculate Random Pos
    /// </summary>
    /// <returns>Vector3 type Pos</returns>
    private Vector3 CalcRandomPos()
    {
        Vector3 _prefab_size = m_prefab.GetComponent<Transform>().localScale;
        Vector3 _size = m_area.size;

        float _pos_x = Random.Range(-20,20) + Random.Range(-_size.x/2f, _size.x/2f) + _prefab_size.x;
        float _pos_z = Random.Range(-20,20) + Random.Range(-_size.z/2f, _size.z/2f) + _prefab_size.z;

        return new Vector3(_pos_x, 1, _pos_z);
    }

    /// <summary>
    /// Activate When Press Initialize Button
    /// </summary>
    private void OnPushInitButton()
    {
        m_isExist = false;
        for(int count = 0; count < m_cubelist.Count; count ++)
        {
            Destroy(m_cubelist[count]);
        }
        m_cubelist.Clear();
    }
}
``` 
<br>

#### **실행 영상** <br>
<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Unity/Unity/random_pos_005.mp4" type="video/mp4">
</video>

 <br> <br>

**[초기화버튼 추가]** <br>
<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Unity/Unity/random_pos_006.mp4" type="video/mp4">
</video>




<br>
[Top](#){: .btn .btn--primary }{: .align-right}
---
title:  "[Unity] 유니티 데이터 또는 리소스(Resources) 로드하는 방법 총정리"
excerpt: Unity Load Resources

categories:
  - Unity Code
tags:
  - [Json, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2023-03-13
last_modified_at: 2023-03-13
---

## Resources 폴더를 사용한 리소스 로딩
---
유니티에서 이미지 같은 리소스 파일을 로드 하는 방법에 대해서 입니다. <br>
기본적 이며 실무에서 많이 사용하는 방법이니 익혀두시면 도움이 될 것 입니다. <br>

```Resources.Load``` 라는 Unity에서 제공하는 리소스를 로드하는 메소드를 사용하여 로드하는 방식입니다. <br>
여기서 Resources 폴더는 Unity에서 기본적으로 제공되는 폴더 이지만, 처음 유니티를 열었을 때 없을 수도 있으니 그때는 CreateFolder로 Resources폴더를 만들어서 사용하시면 됩니다. <br> <br>

## 주의점
---
* Resources 폴더에 너무 많은 리소스를 넣으면 빌드 시간이 길어지고 게임 용량이 커질 수 있습니다.
* Resources.Load() 메서드는 동기적으로 리소스를 로드하므로, 큰 파일을 로드할 경우 게임이 멈추는 현상이 발생할 수 있습니다.

## 예시 코드
---
```C#
// GameObject Prefab을 로드
GameObject prefab = Resources.Load<GameObject>(“PrefabName”);
// 로드한 Prefab을 인스턴스화
GameObject instantiatedObject = Instantiate(prefab);

// 이미지 Sprite를 로드 하는 방법1 
Sprite spriteImage = Resources.Load<Sprite>("Path + name");
Sprite testImageSprite = spriteImage;

// 이미지 sprite를 로드 하는 방법2
string path = ""illust/stage/" + illustName";
Sprite testImageSprite = Resources.Load<Sprite>(path);

// Resources 폴더에 있는 텍스처 로드
Texture2D texture = Resources.Load<Texture2D>("Textures/MyTexture");

// Resources 폴더에 있는 텍스트 파일 로드
TextAsset textAsset = Resources.Load<TextAsset>("Text/MyTextFile");

// Resources.LoadAll() 메서드를 사용하여 Resources 폴더의 모든 리소스 로드
Object[] resources = Resources.LoadAll("Textures");
```
<br>

위와같이 매우 간단하게 로드할 수 있습니다.<br>
다만, Resources폴더 내에 많은 리소스를 저장하는것은 매우 좋지않은 방법입니다. <br><br>
왜냐하면 Resources폴더 내에 리소스가 많을 수록 메모리 사용량과 APK,AAB의 용량이 늘어나기 때문입니다. <br>
메모리 사용량과 용량을 줄이기 위해서는 필요한것만 Resources내에 저장하는것이 좋습니다.<br>
(예를들어 Prefab나 BGM데이터 같은 경우 Resources폴더 내에 저장하지 않아도 상관없습니다.)<br><br>

또한 Resources 폴더의 경로는 상대 경로 이기때문에, 폴더 구조가 바뀔 경우 코드가 정상적으로 작동하지 않을 수 있습니다. <br>
이를 방지하기 위해 상대 경로 대신 절대 경로를 사용하는 것이 좋습니다.<br>
<br>

##  Asset Bundle을 사용한 리소스 로딩
---
Asset Bundle은 리소스를 압축하여 별도로 관리하는 방법입니다. Asset Bundle을 사용하면 필요한 리소스만 다운로드하여 로드할 수 있으므로 게임 용량을 줄이고 초기 로딩 시간을 단축할 수 있습니다.
<br><br>

### 주의점
---
* Asset Bundle을 사용하려면 별도로 Asset Bundle을 빌드해야 합니다.
* Asset Bundle을 잘못 관리하면 메모리 누수가 발생할 수 있습니다.
<br><br>

### 예시 코드
---
```C#
// Asset Bundle 로드
AssetBundle assetBundle = AssetBundle.LoadFromFile("path/to/myassetbundle");

// Asset Bundle에서 리소스 로드
Texture2D texture = assetBundle.LoadAsset<Texture2D>("MyTexture");

// Asset Bundle 해제
assetBundle.Unload(false);
```
<br><br>

## Addressable Asset System을 사용한 리소스 로딩
---
Addressable Asset System은 Unity 2018.3부터 도입된 새로운 리소스 관리 시스템입니다. Addressable Asset System을 사용하면 리소스를 쉽게 관리하고 로드할 수 있으며, Asset Bundle과 유사한 기능을 제공합니다.
<br><br>

### 주의점
---
* Addressable Asset System을 사용하려면 Addressables 패키지를 설치해야 합니다.
* Addressable Asset System은 비교적 복잡한 시스템이므로, 사용 방법을 충분히 숙지해야 합니다.

<br><br>

### 예시 코드
---
```C#
// Addressable Asset System을 사용하여 리소스 로드
AsyncOperationHandle<Texture2D> handle = Addressables.LoadAssetAsync<Texture2D>("Assets/Textures/MyTexture.png");

// 로드가 완료되면 콜백 함수 호출
handle.Completed += (AsyncOperationHandle<Texture2D> obj) =>
{
    Texture2D texture = obj.Result;
};

// 리소스 해제
Addressables.Release(handle);
```
<br><br>

## Resources.LoadAsync()를 사용한 비동기 리소스 로딩
---
Resources.LoadAsync() 메서드를 사용하면 리소스를 비동기적으로 로드할 수 있습니다. 비동기 로딩은 큰 파일을 로드할 때 게임이 멈추는 현상을 방지하는 데 유용합니다.
<br><br>

### 주의점
---
비동기 로딩은 완료될 때까지 기다려야 하므로, 콜백 함수를 사용하여 로드 완료 시점을 처리해야 합니다.
<br><br>

### 예시 코드
---
```C#
// Resources.LoadAsync() 메서드를 사용하여 텍스처 비동기 로드
ResourceRequest request = Resources.LoadAsync<Texture2D>("Textures/MyTexture");

// 로드가 완료되면 콜백 함수 호출
request.completed += (AsyncOperation operation) =>
{
    Texture2D texture = request.asset as Texture2D;
};
```

<br><br>

## Object.Instantiate()를 사용한 프리팹 생성
---
Object.Instantiate() 메서드를 사용하면 프리팹을 복제하여 게임 오브젝트를 생성할 수 있습니다.
<br><br>

### 주의점
---
Instantiate() 메서드는 동기적으로 프리팹을 생성하므로, 많은 프리팹을 한 번에 생성하면 게임이 멈추는 현상이 발생할 수 있습니다.
<br><br>

### 예시 코드
---
```C#
// 프리팹 로드
GameObject prefab = Resources.Load<GameObject>("Prefabs/MyPrefab");

// 프리팹 복제
GameObject instance = Instantiate(prefab);
```
<br><br>

## 데이터 파일을 이용한 로드
---
아래의 예시과 같이 텍스트 파일, JSON 파일, XML 파일 등 다양한 형식의 데이터 파일을 로드하여 사용할 수 있습니다.
<br><br>

### 주의점
---
* 데이터 파일의 형식을 정확하게 파악하고, 그에 맞는 파싱 라이브러리를 사용해야 합니다.
* 데이터 파싱 과정에서 예외 처리를 해야 합니다.
* 대용량 데이터를 로드하는 경우, 비동기 방식으로 처리하여 게임의 멈춤 현상을 방지해야 합니다.
<br><br>

### 예시 코드
---
[Text 파일]
```C#
// 텍스트 파일 로드
TextAsset textAsset = Resources.Load<TextAsset>("Text/MyTextFile");
string text = textAsset.text;
```
<br><br>

[JSON 파일]
```C#
// JSON 파일 로드
string json = Resources.Load<TextAsset>("JSON/MyJsonFile").text;
MyData data = JsonUtility.FromJson<MyData>(json);
```
<br><br>

[XML 파일]
```C#
// XML 파일 로드
XmlDocument xmlDoc = new XmlDocument();
xmlDoc.LoadXml(Resources.Load<TextAsset>("XML/MyXmlFile").text);
```
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}
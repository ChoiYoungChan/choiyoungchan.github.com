---
title:  "[Unity] 유니티에서 JSON 사용하기"
excerpt: Using JSON in Unity

categories:
  - Unity Code
tags:
  - [JSON, Unity, 유니티]

toc: true
toc_sticky: true
 
date: 2022-12-15
last_modified_at: 2022-12-15
---

## 개요
---
유니티에서 JSON데이터를 저장/읽기/사용하는 방법에 관한 글 입니다.<br>
게임 데이터 등으로 많이 이용되는것이 JSON, CSV, PlayerPref 인데 오늘은 이중에서 JSON데이터를 사용하는 방법에 대해 알아보겠습니다.<br><br>

[Unity CSV 사용법]()<br>
[Unity PlayerPref 사용법]()<br>

JSON의 개념은 기본적으로 다들 알고 계신다고 생각하여 생략하고 바로 장단점과  본론인 사용법으로 바로 들어가겠습니다.<br>

장점
- JSON은 웹이나 네트워크에서 서버와 클라이언트 사이에서 데이터를 주고 받을 때 사용하는 개방형 표준 포멧으로, 텍스트를 사용하기 때문에 사람이 이해하기 쉽다.
- JSON 포멧은 유니티에서도 많이 사용하며, 네트워크 게임을 개발할 때 필요한 데이터를 주고 받거나, 게임 진행 상황을 저장하거나, 게임 설정을 저장하는 방식으로도 사용할 수 있다.
- XML에 비해서 가독성이 좋고 직렬화(Serialize)와 비직렬화(Deserialize) 함수를 통해서 데이터에서 JSON 데이터로, JSON 데이터에서 데이터로 편하게 변환할 수 있다

단점
- JSON의 단점은 작은 문법 오류에도 매우 민감하다.(중간에 중괄호나 대괄호, 콜론, 쉼표가 하나라도 빠지면 JSON 파일이 깨져버리고 파일을 읽어들일 수 없게 된다.)


## 사용법
---

먼저, JSON을 저장하고 읽으려면 아래와 같은 방식으로 사용할 수 있습니다.<br>

공통 부분
1. JSON형식으로 저장할 객체의 클래스 또는 구조체를 정의
2. 객체를 JSON형식으로 직렬화

JSON 데이터를 저장하려면<br>
객체로부터 JSON형식의 문자열을 생성하고 해당 문자열을 바이트 시퀀스로 인코딩 후 파일을 생성합니다.<br>

JSON 데이터를 읽으려면<br>
파일의 바이트 시퀀스를 문자열로 디코딩후 string에 넣어서 출력 하거나 객체를 생성하여 그 객체 않에 넣고 사용<br><br>

### 1. JSON형식으로 저장할 객체의 클래스 또는 구조체를 정의
<br>

먼저 아래처럼 NewtonsoftJson이나 MiniJson등 사용하는 라이브러리의 네임스페이스를 추가해주세요
``` C#
using Newtonsoft.Json;    // newtonsoft json을 사용할 경우
using MiniJSON;           // MiniJson을 사용할 경우
```
<br>

구조체를 사용하는 방법
``` C#
struct Person
{
  public string Name { get; set; }
  public int Age { get; set; }
  public int Level { get; set; }
  public int Hp { get; set; }
}
```
<br>

클래스를 사용하는 방법(굳이 partial클래스를 사용하지 않아도 됩니다.)
``` C#
public partial class StatusData
{
    [JsonProperty("stage_id")]
    public int StageId { get; set; }

    [JsonProperty("question")]
    public string Question { get; set; }

    [JsonProperty("hint")]
    public string Hint { get; set; }

    [JsonProperty("hint_count")]
    public int HintCount { get; set; }

    // PRIVACY POLICY
    [JsonProperty("privacy_policy_link")]
    public string PrivacyPolicyLink { get; set; }

    // Share
    [JsonProperty("share_link")]
    public string ShareLink { get; set; }
}
```
<br>

### 2. 객체를 JSON형식으로 직렬화
``` C#
using UnityEngine;

[System.Serializable] // 직렬화 가능하도록 속성 추가
public class PlayerData
{
    public string playerName;
    public int level;
    public float experience;
}

public class JsonExample : MonoBehaviour
{
    void Start()
    {
        // 객체 생성
        PlayerData player = new PlayerData();
        player.playerName = "홍길동";
        player.level = 10;
        player.experience = 99.5f;

        // 객체를 JSON 문자열로 직렬화
        string json = JsonUtility.ToJson(player);

        // JSON 문자열 출력
        Debug.Log(json);

        // JSON 문자열을 객체로 역직렬화
        PlayerData loadedPlayer = JsonUtility.FromJson<PlayerData>(json);

        // 역직렬화된 객체 정보 출력
        Debug.Log("Loaded Player Name: " + loadedPlayer.playerName);
        Debug.Log("Loaded Player Level: " + loadedPlayer.level);
        Debug.Log("Loaded Player Experience: " + loadedPlayer.experience);
    }
}
```
<br>

### 데이터 클래스 샘플
---
먼저 아래의 JSON데이터를 저장/로드 코드에서 사용할 데이터 클래스 샘플입니다.

``` C#
using System; // Serializable 속성을 사용하기 위해 추가

[Serializable]
public class PlayerData
{
    public string playerName;
    public int level;
    public float experience;

    public PlayerData(string name, int lv, float exp) // 생성자 추가
    {
        playerName = name;
        level = lv;
        experience = exp;
    }
}
```

### JSON 데이터를 저장
아래와 같이 객체로부터 JSON형식의 문자열을 생성하고 해당 문자열을 바이트 시퀀스로 인코딩 후 파일을 생성합니다.<br>
``` C#
using UnityEngine;
using System.IO;
using Newtonsoft.Json; // Newtonsoft Json.NET 사용

public class JsonLoader : MonoBehaviour
{
    private string filePath;

    void Awake()
    {
        filePath = Path.Combine(Application.persistentDataPath, "playerData.json");
    }

    public PlayerData LoadData()
    {
        if (File.Exists(filePath))
        {
            try
            {
                string json = File.ReadAllText(filePath);
                PlayerData loadedData = JsonConvert.DeserializeObject<PlayerData>(json);
                Debug.Log("Player data loaded from: " + filePath);
                return loadedData;
            }
            catch (System.Exception e)
            {
                Debug.LogError("Error loading player data: " + e.Message);
                return null; // 오류 발생 시 null 반환
            }
        }
        else
        {
            Debug.LogWarning("Player data file not found.");
            return null; // 파일이 없을 경우 null 반환
        }
    }

    // 예시 호출 함수 (테스트용)
    public void TestLoad()
    {
        PlayerData loadedData = LoadData();
        if(loadedData != null)
        {
            Debug.Log("Loaded Player Name: " + loadedData.playerName);
            Debug.Log("Loaded Player Level: " + loadedData.level);
            Debug.Log("Loaded Player Experience: " + loadedData.experience);
        }
    }
}
```
<br>

(이후 해당 경로에서 생성한 JSON파일을 확인할 수 있습니다.)<br>


### JSON데이터를 읽기

아래와 같이 파일의 바이트 시퀀스를 문자열로 디코딩후 string에 넣어서 출력 하거나 객체를 생성하여 그 객체 않에 넣고 사용합니다. <br>


``` C#
using UnityEngine;
using System.IO;
using Newtonsoft.Json; // Newtonsoft Json.NET 사용

public class JsonLoader : MonoBehaviour
{
    private string filePath;

    void Awake()
    {
        filePath = Path.Combine(Application.persistentDataPath, "playerData.json");
    }

    public PlayerData LoadData()
    {
        if (File.Exists(filePath))
        {
            try
            {
                string json = File.ReadAllText(filePath);
                PlayerData loadedData = JsonConvert.DeserializeObject<PlayerData>(json);
                Debug.Log("Player data loaded from: " + filePath);
                return loadedData;
            }
            catch (System.Exception e)
            {
                Debug.LogError("Error loading player data: " + e.Message);
                return null; // 오류 발생 시 null 반환
            }
        }
        else
        {
            Debug.LogWarning("Player data file not found.");
            return null; // 파일이 없을 경우 null 반환
        }
    }

    // 예시 호출 함수 (테스트용)
    public void TestLoad()
    {
        PlayerData loadedData = LoadData();
        if(loadedData != null)
        {
            Debug.Log("Loaded Player Name: " + loadedData.playerName);
            Debug.Log("Loaded Player Level: " + loadedData.level);
            Debug.Log("Loaded Player Experience: " + loadedData.experience);
        }
    }
}
```
<br>


<br>
[Top](#){: .btn .btn--primary }{: .align-right}
---
title:  "[Unity] 유니티에서 GPT API 활용하기"
excerpt: 유니티에서 Gpt Api사용하기

categories:
  - AI
tags:
  - [Unity, AI, GPT, 유니티]

toc: true
toc_sticky: true
 
date: 2023-04-08
last_modified_at: 2023-04-08
---

## 개요
---
최근 GPT API같이 AI API를 유니티와 언리얼에서 이용해 챗봇이나 활용한 어플, 게임이 많이 나오고 있습니다.
그렇다면 지금까지 Unity에 AI가 없었는가? 라고 하기에는 기존의 Unity에도 AI를 사용하는 부분이 있었습니다.<br>
바로 유니티와 언리얼의 NavMesh라는것이며, 상세한 설명은 아래의 포스팅을 참조해 주시기 바랍니다.

[유니티 NavMesh](https://choiyoungchan.github.io/unity/navmesh/) <br>
[UE4 NavMesh]() <br>

기존에는 네비게이션 경로를 계산하여 AI에이전트가 걸어다닐 수 있는 표면을 만드는 정도였다면,<br>
앞으로는 AI를 어시스턴르로서 활용한 생산성 향상과 버그관리의 용이성에서 상당한 발전이 있을것이라 사료됩니다. <br>
(참고로 AI가 프로그래머를 완전히 대체하는건 아직 멀었습니다 ㅎㅎ)<br>

오늘은 에디터인 Unity에서 GPT API를 적용하는 방법을 알려 드리고자 합니다.<br>
<br>

---
## 사용 방법
---

먼저 gpt api를 유니티에 적용하는 방법은 아래의 순서대로 입니다. <br>


1. 회원 가입 및 api 키 발급
2. Unity에 발급 받은 키 적용
3. GPT API 컨트롤러와 모델 제작
4. Unitywebrequest로 데이터 송수신

깃 허브에 리포지토리를 공개하였으니 참조 부탁드립니다. [Git리포지토리](https://github.com/ChoiYoungChan/Unity_GPT3.5inUnity) <br>

<br>
순서대로 가보겠습니다 <br>
<br>


### 1. 회원 가입 및 api 키 발급
---
<br>
먼저 아래의 1번 URL에 들어가 회원가입을 하고 2번 URL에서 키를 발급할 수 있습니다.

1. https://chat.openai.com/
2. https://beta.openai.com/account/api-keys


<br>

이미 회원 가입을 하신분 또는 회원 가입을 완료하신 분은 다음과 같이 유료결제(광고아닙니다...;;) 하시면 됩니다.<br>

![000](https://user-images.githubusercontent.com/40765022/233368925-b1b6f59b-a98d-49b4-85b1-733c91fc30c9.png) <br><br>


이후 다음과 같이 2번 URL에서 로그인 한 뒤 API Key를 발급 받으실 수 있습니다. <br>
아래의 User -> API Keys 에서 Create new secret key 버튼을 누르시면 <br>

![003](https://user-images.githubusercontent.com/40765022/233369092-7388597b-a5a7-402e-96f7-a3790587a112.png)<br><br>


다음과 같이 키가 생성됩니다. <br>
![004](https://user-images.githubusercontent.com/40765022/233369634-a0b80171-2bae-4c71-b4bd-2c66f35a1f62.png) <br>

이제 이 키를 유니티에 적용하도록 하겠습니다. <br>

### 2. Unity에 발급 받은 키 적용
---
<br>

```C#
const string GPT_API_KEY = "input here";
const string API_END_POINT = "input here";
```
상기의 [input here]이라고 적힌 부분에 발급 받은 key를 입력해주시면 됩니다. <br>
(당연하지만)변하면 안되는 값이기 때문에 const지정을 해 줍니다. <br>
<br>


### 3. Request, Resoponse에 사용할 데이터 타입 및 클래스 선언
---
<br>

```C#
[JsonObject]
public class APIRequestData
{
    public string Model { get; set; }
    public string Prompt { get; set; }
    public int Temperature { get; set; }
    public int MaxTokens { get; set; }
}


[JsonObject]
public class APIResponseData
{
    public string Id { get; set; }
    public string Object { get; set; }
    public string Model { get; set; }
    public int Created { get; set; }
    public ChoiceData[] Choices { get; set; }
    public UsageData Usage { get; set; }
}

[JsonObject]
public class ChoiceData
{
    public string Message { get; set; }
    public int Index { get; set; }
    public string MessageLog { get; set; }
    public string FinishReason { get; set; }
}

[JsonObject]
public class UsageData
{
    public int PromptTokens { get; set; }
    public int CompletionTokens { get; set; }
    public int TotalTokens { get; set; }
}
```

<br>

### 4. Unitywebrequest로 데이터 송수신
---
<br>

```C#
/// <summary>
/// send question text data and wait response, return answer json data
/// </summary>
/// <param name="prompt"></param>
/// <returns></returns>
public async UniTask<APIResponseData> GetAPIResponse(string prompt)
{
  APIRequestData _requestData = new()
    {
     Prompt = prompt,
     MaxTokens = 300
     };
     
     string _requestJson = JsonConvert.SerializeObject(_requestData, Formatting.Indented);
     Debug.Log("### " + _requestJson);
     
     // text data for post
     byte[] _data = System.Text.Encoding.UTF8.GetBytes(_requestJson);
     
     string _jsonString = null;
     using (UnityWebRequest _request = UnityWebRequest.Post(API_END_POINT, "Post"))
     {
      _request.uploadHandler = new UploadHandlerRaw(_data);
       _request.downloadHandler = new DownloadHandlerBuffer();
       _request.SetRequestHeader("Content-Type", "application/json");
       _request.SetRequestHeader("Authorization", "Bearer" + GPT_API_KEY);
       await _request.SendWebRequest();
       
       switch(_request.result)
       {
        case UnityWebRequest.Result.InProgress :
             Debug.Log("### Processing");
             break;
        case UnityWebRequest.Result.Success:
             Debug.Log("### Success");
             _jsonString = _request.downloadHandler.text;
             break;
        case UnityWebRequest.Result.ConnectionError or UnityWebRequest.Result.DataProcessingError :
             Debug.LogError("### Error");
             throw new Exception();
        default:
             throw new ArgumentOutOfRangeException();
        }
      }
      
    return JsonConvert.DeserializeObject<APIResponseData>(_jsonString);
}
```

<br>

## 결과
---

<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Algorithm/AI/gpt_api_000.mp4" type="video/mp4">
</video>

<br>

[Top](#){: .btn .btn--primary }{: .align-right}
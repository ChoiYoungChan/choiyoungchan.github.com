---
title:  "[Unity] 머테리얼이나 오브젝트가 분홍색으로 깨질때 대응하는 방법"
excerpt: Responding to Material Cracking Error just like pink

categories:
  - Unity Error Respond
tags:
  - [Unity, 유니티, 머테리얼, 깨짐, 분홍색, Material, Cracking, pink]

toc: true
toc_sticky: true
 
date: 2023-02-17
last_modified_at: 2023-02-17
---

## 개요
---
유니티에서 개발을 하다 보면 아래와 같이 머테리얼 또는 3D오브젝트가 (아니면 전부 다) 핑크빛으로 되는 경우가 있습니다. 그래서 해당 현상에 대해 가능성이 높은 원인과 해결 방법을 적어보려고 합니다.

![Image](https://github.com/user-attachments/assets/71f6ea93-60b8-4151-bad0-31a0814e03d2)
<br><br>

![Image](https://github.com/user-attachments/assets/27609eff-6927-4b30-8981-3b2ed5eb7331)
<br><br>

## 원인
---
유니티에서 오브젝트나 머테리얼이 분홍색으로 나타나는 현상은 셰이더(Shader)와 관련된 문제일 가능성이 큽니다. 셰이더는 오브젝트의 표면을 어떻게 렌더링할지 결정하는 코드인데, 다음과 같은 이유로 인해 문제가 발생할 수 있습니다.

1. 셰이더 누락 또는 손상:
   * 셰이더 파일 삭제: 셰이더 파일이 실수로 삭제되었거나 프로젝트에서 누락되었을 수 있습니다.
   * 셰이더 파일 손상: 셰이더 파일이 어떤 이유로 손상되었을 수 있습니다.
   * 셰이더 컴파일 오류: 셰이더 코드가 문법 오류 등으로 인해 컴파일에 실패했을 수 있습니다.

2. 셰이더 호환성 문제
   * 렌더 파이프라인 불일치: 유니티의 렌더 파이프라인(Built-in, URP, HDRP)과 셰이더가 호환되지 않을 수 있습니다. 예를 들어, Built-in 렌더 파이프라인에서 사용하던 셰이더를 URP 환경에서 사용하면 문제가 발생할 수 있습니다.
   * 셰이더 버전 불일치: 셰이더의 버전이 유니티 버전과 호환되지 않을 수 있습니다. 오래된 셰이더를 최신 유니티 버전에서 사용하거나, 반대로 최신 셰이더를 구 버전 유니티에서 사용하면 문제가 발생할 수 있습니다.

3. 머티리얼 설정 오류: 잘못된 셰이더 할당: 머티리얼에 엉뚱한 셰이더가 할당되었거나, 셰이더가 할당되지 않았을 수 있습니다.
머티리얼 속성 오류: 머티리얼의 속성값이 셰이더와 맞지 않게 설정되었을 수 있습니다.

4. 기타 문제
   * 에셋 임포트 오류: 에셋을 임포트하는 과정에서 셰이더나 머티리얼이 제대로 임포트되지 않았을 수 있습니다.
   * 하드웨어 문제: 드물지만, 그래픽 카드 드라이버 문제나 하드웨어적인 문제로 인해 셰이더가 제대로 렌더링되지 않을 수 있습니다.
<br><br>

## 해결 방법
---
### URP Material Upgrade
---
아래의 과정을 통해 URP Material을 업그레이드 해줍니다. (업그레이드 후 Reimport를 해서 해결되는 경우도 있습니다.)

```
Edit -> Render Pipline -> Universal Render Pipline -> Upgrade Selected Material
```
<br>

![Image](https://github.com/user-attachments/assets/adbbcdb5-03cd-4f71-9013-5311807b9de7)
<br>

### Material Reimport
---

![Image](https://github.com/user-attachments/assets/1cde58a3-fa46-4ba0-b829-e9f30c79033a)
<br>

### Material 설정 수정
---
아무 값을 변경해서 설정을 살짝 건드려 주면 어이없게도 해결되는 경우도 있습니다. -_-
![Image](https://github.com/user-attachments/assets/d39a899c-b7ac-4f6e-b816-5509c020a049)

<br> 

[Top](#){: .btn .btn--primary }{: .align-right}
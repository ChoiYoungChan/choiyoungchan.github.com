---
title:  "[Unity] 유니티 Gradle Error 발생 대응 총정리"
excerpt: Responding to NullReferenceException error

categories:
  - Unity Error Respond
tags:
  - [Unity, 유니티, Gradle, 그래들]

toc: true
toc_sticky: true
 
date: 2025-01-12
last_modified_at: 2025-01-12
---

## 유니티 빌드시 Gradle Error가 발생하는 원인과 해결 방법
---
* ***Gradle 버전 불일치***
  * 원인 : 프로젝트에서 사용하는 Gradle 버전과 유니티에서 사용하는 버전이 달라서 발생합니다.
  * 해결 방법
    * ```Edit > Preferences > External Tools > Gradle Installed with Unity```체크 해제 후 수동으로 Gradle 버전 설정
    * ```gradle-wrapper.properties에서 Gradle```버전 확인 후 맞춰줌
    * Unity가 요구하는 Gradle 버전을 공식 문서에서 확인하고 다운로드
<br><br>

* Gradle 캐시 문제
  * 원인 : Gradle 빌드 캐시가 손상되거나 오래된 파일이 남아 충돌하는것이 원인인 경우 입니다.
  * 해결 방법
    * ```C:\Users\사용자명\.gradle```폴더 삭제
    * ```android\build```폴더 삭제 후 다시 빌드
    * ```Preferences > External Tools > Reset Packages to Defaults```실행
<br><br>

* Android SDK / NDK / JDK 버전 문제
  * 원인 : 유니티 프로젝트에서 사용하는 Android SDK, NDK, JDK 버전이 일치하지 않아 발생하는 경우 입니다.
  * 해결 방법
    * ```Edit > Preferences > External Tools```에서 Unity가 제공하는 SDK, NDK, JDK를 사용
    * ```Project Settings > Player > Android```에서 정확한 버전 확인
    * ```gradle.properties```에서 ```org.gradle.java.home```경로 수정
<br><br>

* Proguard / R8 관련 오류
  * 원인 : Proguard 또는 R8이 잘못된 설정으로 인해 빌드 실패할 수도 있습니다.
  * 해결 방법
    * ```Assets/Plugins/Android/proguard-user.txt```에서 잘못된 규칙 수정
    * ```radle.properties에서 android.enableR8=false```설정
    * ```Player Settings > Publishing Settings에서 Minify```옵션 비활성화
<br><br>

* Internet / Network 문제
  * 원인 : 흔하지는 않지만 Gradle이 의존성을 다운로드할 때 네트워크 문제 발생하는 경우 입니다.
  * 해결 방법
    * ```gradle.properties```에 ```org.gradle.daemon=false```추가
    * VPN을 사용하여 Gradle 리포지토리에 접근 가능하게 설정
    * ```android\gradle\wrapper\gradle-wrapper.properties```의 ```distributionUrl```을 최신 버전으로 변경
<br><br>

* Java Heap Space 오류
  * 원인 : Gradle 빌드 시 할당된 메모리 부족해서 발생하는 경우 입니다.
  * 해결 방법
    * ```gradle.properties```에 아래 추가
        ```
        org.gradle.jvmargs=-Xmx4096M
        ```
    * Unity Editor의 메모리 사용을 줄이거나 다른 프로그램 종료 후 빌드
<br><br>

* Unity Gradle Template 오류
  * 원인 : ```mainTemplate.gradle```이 손상되거나 누락되어 발생하는 경우입니다. 의외로 많이 발생합니다.
  * 해결 방법
    * ```Assets/Plugins/Android/mainTemplate.gradle```삭제 후 재생성
    * ```Edit > Preferences > External Tools```에서 ```Gradle Installed with Unity```체크 후 다시 빌드
<br><br>

* Keystore 관련 오류
  * 원인 : ```Keystore```파일이 누락되거나 암호가 달라서 발생하는 경우
  * 해결 방법
    * ```Player Settings > Publishing Settings에서 Keystore```경로 확인
    * 새 Keystore 생성 후 적용
<br><br>

* Firebase / Admob 플러그인 충돌
  * 원인 : Firebase나 Admob 같은 플러그인이 잘못 설정된 경우
  * 해결 방법
    * ```Assets/ExternalDependencyManager/Editor/Resolver```실행 후 ```Force Resolve```
    * ```Plugins/Android```폴더에서 중복된 ```.aar```파일 삭제
<br><br>

* Unsupported class file major version 오류
  * 원인 : JDK 버전이 낮아서 최신 Java 코드 실행 불가
  * 해결 방법
    * JDK 11 이상 설치 후 Preferences > External Tools에서 JDK 경로 변경
    * gradle.properties에서 org.gradle.java.home 수정
<br><br>

## 해결 방법에 대하여 개인적인 팁
---
1. 유니티 콘솔에서 전체 에러 메시지 확인
   * ```Preferences > Console```에서 ***Full Stack Trace*** 옵션 활성화를 해줍니다.
   * 오류 메시지를 기반으로 필요한 수정 진행합니다.
<br><br>

2. ***Gradle*** 빌드 수동 실행 테스트
    ```
    cd 프로젝트경로/Android
    ./gradlew build --stacktrace
    ```
<br>

3. ***Gradle*** 리포지토리 수동 업데이트
    ```
    gradle --refresh-dependencies
    ```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}
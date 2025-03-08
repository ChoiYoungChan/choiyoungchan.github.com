---
title:  "[Unity] Admob Unsupported class version number 에러 대응"
excerpt: Responding to NullReferenceException error

categories:
  - Unity Error Respond
tags:
  - [Unity, 유니티, Admob, 에러 대응]

toc: true
toc_sticky: true
 
date: 2024-03-21
last_modified_at: 2024-03-21
---

## Admob Unsupported class version number에러가 발생하는 원인
---
Unity에서 AdMob을 사용할 때 "Unsupported class version number" 오류는 일반적으로 Unity의 JDK(Java Development Kit) 버전이 너무 낮거나, Gradle이 최신 Java 클래스 파일을 처리할 수 없는 경우에 발생합니다. 주요 원인은 다음과 같습니다:

1. JDK 버전 문제
  * Unity가 사용하는 JDK 버전이 낮아, 최신 AdMob SDK에서 요구하는 Java 클래스 파일을 처리할 수 없음.
  * AdMob SDK는 Java 8 또는 11 이상을 필요로 하는데, Unity가 제공하는 내장 JDK가 이를지원하지 못할 가능성이 있음.
2. Gradle 버전 불일치
  * Unity가 사용하는 Gradle 버전이 낮아 최신 Java 클래스 버전을 지원하지 못함.
  * AdMob의 최신 버전은 Gradle 7.x 이상을 요구할 수 있음.
3. Android SDK 및 빌드 도구 미설치 또는 버전 불일치
   * AdMob SDK에서 요구하는 최신 Android SDK 버전과 Unity의 Android SDK 버전이 맞지 않는 경우.
  * compileSdkVersion이 낮거나, buildToolsVersion이 AdMob SDK와 호환되지 않는 경우.
4. Proguard 또는 R8 미지원
   * Proguard 또는 R8이 올바르게 설정되지 않아 최신 Java bytecode를 처리하지 못함.

## 해결 방법
---
1. JDK 버전 업그레이드
   * Unity에서 제공하는 기본 JDK가 아닌, JDK 11 이상을 사용하도록 변경합니다.
     1. AdoptOpenJDK 또는 Oracle JDK에서 JDK 11 또는 17을 다운로드 후 설치.
     2. Unity에서 Edit > Preferences > External Tools로 이동.
     3. JDK 항목에서 Unity 내장 JDK를 사용하지 않도록 체크 해제 후, 직접 설치한 JDK 경로를 지정.
     4. gradle.properties 파일을 열고 아래 설정 추가
        ```
        org.gradle.java.home=C:\\Program Files\\Java\\jdk-11
        ```

2. Gradle 버전 업데이트
   * Unity의 Gradle 버전이 낮으면 최신 Java 클래스를 지원하지 못할 수 있습니다.
     1.  Edit > Preferences > External Tools에서 Gradle Installed with Unity 옵션을 해제.
     2.  Unity 공식 문서에서 지원하는 최신 Gradle 버전을 다운로드하여 android\gradle\wrapper\gradle-wrapper.properties 파일을 수정:
          ```
          distributionUrl=https\://services.gradle.org/distributions/gradle-7.5-all.zip
          ```
     3.  android\build.gradle 파일에서 classpath 'com.android.tools.build:gradle:7.0.2'와 같이 최신 Gradle 플러그인 버전으로 업데이트.

3. Android SDK 및 빌드 도구 최신 버전 설치
   * AdMob이 최신 Android SDK와 호환되지 않을 수 있으므로 compileSdkVersion을 업데이트해야 합니다.
     1. Android SDK Manager를 열고 최신 Android API Level 31 이상을 설치.
     2. Unity에서 Edit > Preferences > External Tools에서 Android SDK 경로를 최신 버전으로 변경.
     3. android\build.gradle 파일을 열어 아래처럼 수정
        ```
        android {
            compileSdkVersion 31
            defaultConfig {
                minSdkVersion 21
                targetSdkVersion 31
            }
        }
        ```

4. Proguard 및 R8 활성화
   * AdMob은 최신 Java bytecode 최적화를 위해 Proguard 또는 R8을 사용하므로, 이를 활성화해야 합니다.

     1. ```Assets/Plugins/Android/proguard-user.txt``` 파일을 수정하거나 생성하여 아래 내용 추가
        ```
        -keep class com.google.** { *; }
        -keep class com.unity3d.** { *; }
        -keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,RuntimeVisibleAnnotations,AnnotationDefault,RuntimeInvisibleAnnotations,EnclosingMethod
        ```
     2. Unity에서 Edit > Project Settings > Player > Android > Publishing Settings에서 Minify 옵션을 Proguard로 설정.

### 추가 해결 방법
---
1. Gradle 캐시 삭제 후 다시 빌드
    ```
    rm -rf ~/.gradle/caches
    ```
2. Unity 캐시 삭제 후 다시 빌드
    ```
    rm -rf Library/Temp
    ```
3. AdMob SDK 및 External Dependency Resolver 최신화
   * Assets > External Dependency Manager > Android Resolver > Force Resolve 실행.
<br><br>

## 정리
---


[Top](#){: .btn .btn--primary }{: .align-right}
---
title:  "[Unity] APK또는 Keystore파일에서 fingerprint찾는법"
excerpt: shader in Unity

categories:
  - Unity
tags:
  - [Unity, fingerprint, APK, Keystore,유니티]

toc: true
toc_sticky: true
 
date: 2025-01-12
last_modified_at: 2025-01-12
---

## Keystore파일에서 찾는 방법
---
터미널을 열고 ```keystore```파일이 있는 곳으로 이동하여 ```keytool -list -keystore [file name]```을 입력하면 아래의 예시와 같이 표시가 되는데, 

```
$ keytool -list -keystore my-upload-key.keystore
Enter keystore password:
Keystore type: jks
Keystore provider: SUN

Your keystore contains 1 entry

my-key-alias, Aug 28, 2019, PrivateKeyEntry,
Certificate fingerprint (SHA1): F5:A5:7E:6F:C2:CE:08

Warning:
The JKS keystore uses a proprietary format. It is recommended to migrate to PKCS12 which is an industry standard format using "keytool -importkeystore -srckeystore my-upload-key.keystore -destkeystore my-upload-key.keystore -deststoretype pkcs12".
```
<br>

fingerprint는 보시다시피 아래의 부분입니다.
```
Certificate fingerprint (SHA1): F5:A5:7E:6F:C2:CE:08
```
<br><br>

---
## APK파일에서 찾는 방법
---
APK의 경우에도 비슷합니다. 터미널을 열고 ```apk```파일이 있는 곳으로 이동하여 ```keytool -list -printcert -jarfile [file name]```을 입력하면 아래의 예시와 같이 표시가 되는데, 

```
$ keytool -list -printcert -jarfile app-release.apk
Signer #1:

Signature:

Owner: CN=Unknown, OU=Unknown, O=Unknown, L=Unknown, ST=Unknown, C=Unknown
Issuer: CN=Unknown, OU=Unknown, O=Unknown, L=Unknown, ST=Unknown, C=Unknown
Serial number: 2085
Valid from: Mon Sep 02 19:52:00 PST 2019 until: Fri Jan 18 19:52:00 PST 2047
Certificate fingerprints:
	 MD5:  26:D0:0D:AA:71:7C:E4:30:D1
	 SHA1: 93:A2:2C:38:3B:AF:A9:2F:82
	 SHA256: F3:A4:38:06:2C:A5:6C:8A:54:4F:36:E6:23:A0:8E:38:50:DF
Signature algorithm name: SHA256
```
<br>

fingerprint는 아래의 부분입니다.
```
Certificate fingerprints:
	 MD5:  26:D0:0D:AA:71:7C:E4:30:D1
	 SHA1: 93:A2:2C:38:3B:AF:A9:2F:82
	 SHA256: F3:A4:38:06:2C:A5:6C:8A:54:4F:36:E6:23:A0:8E:38:50:DF
```
<br><br>

[Top](#){: .btn .btn--primary }{: .align-right}
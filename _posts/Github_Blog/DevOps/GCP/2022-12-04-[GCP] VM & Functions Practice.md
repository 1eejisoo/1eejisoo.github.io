---
title: "[GCP] VM & Functions Practice"
categories:
  - gcp
tags:
  - gcp
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-04 02:00:00
---

<details><summary><b>reference</b></summary>
학교 수업을 듣고 정리한 내용입니다.
</details>

<br>

> **목차**
>
> ​	1. VM 생성 후 Web Server 설치
>
> ​	2. Functions을 이용하여 기본 함수 생성

<br>

# 1. VM 생성 후 Web Server 설치

## 1-1. VM 생성

> **[Compute Engine]**

<img width="961" alt="스크린샷 2022-12-04 오전 10 22 52" src="https://user-images.githubusercontent.com/93996283/205474316-c65fbda7-a30d-45f4-a99e-c7aeb401d24a.png">

> **[인스턴스 만들기]**

<img width="1440" alt="스크린샷 2022-12-04 오전 10 23 37" src="https://user-images.githubusercontent.com/93996283/205474326-3b3119a9-751e-4d3a-aff3-b30814cb5285.png">

> **인스턴스 정보 입력**
>
> - **[이름]** 설정
> - **[리전]** : asia-northeast3 (서울)
> - **[영역]** : asia-northeast3-a

> **[머신 구성]** 
>
> -  **[머신 유형]** : e2-micro

<img width="1440" alt="스크린샷 2022-12-04 오전 10 26 33" src="https://user-images.githubusercontent.com/93996283/205474322-706d36dc-44af-4f50-b35f-22e9276756b6.png">

> **[ID 및 API 액세스]**
>
> - **[액세스 범위]** : 모든 Cloud API에 대한 전체 액세스 허용

> **[방화벽]**
>
> - HTTP 트래픽 허용, HTTPS 트래픽 허용

> **[만들기]**

<img width="1438" alt="스크린샷 2022-12-04 오전 10 27 21" src="https://user-images.githubusercontent.com/93996283/205474417-bd757447-ffc8-465b-a5ab-17345e7b500d.png">

<br>

## 1-2. VM 연결

public key를 GCP에 등록한다.

>**key 파일 생성**
>
>- key 파일을 생성할 폴더 내에서 아래 명령을 입력한다.

```bash
ssh-keygen -t rsa -C "[구글 계정]"
```

<img width="762" alt="스크린샷 2022-12-04 오전 10 36 05" src="https://user-images.githubusercontent.com/93996283/205475871-85268bdc-6dd0-4527-b368-a31e23bce1f7.png">

> **생성된 key 확인**
>
> - **.pub가 붙은 key** - *public key*
> - **.pub가 붙지 않은 key** - *private key*

<img width="762" alt="스크린샷 2022-12-04 오전 10 55 46" src="https://user-images.githubusercontent.com/93996283/205474537-b4576b19-d246-41c6-b315-4baad667f1d8.png">

> **public key 파일 내용 복사**

<img width="818" alt="스크린샷 2022-12-04 오전 10 57 58" src="https://user-images.githubusercontent.com/93996283/205474536-e5a06f8e-1556-455f-9219-68c8cad93672.png">

> **[Compute Engine] - [설정] - [메타데이터]**

<img width="259" alt="스크린샷 2022-12-04 오전 11 00 27" src="https://user-images.githubusercontent.com/93996283/205474535-09b00cb4-cd44-4de7-b210-4f9b096d5c41.png">

> **[SSH 키] - [수정]**

<img width="1440" alt="스크린샷 2022-12-04 오전 11 00 56" src="https://user-images.githubusercontent.com/93996283/205474668-3a4fe076-04b6-40b4-a23b-69824b31c0a5.png">

> **[+ 항목 추가]** - 복사했던 public key 입력 - **[저장]**

<img width="1440" alt="스크린샷 2022-12-04 오전 11 01 47" src="https://user-images.githubusercontent.com/93996283/205474666-26628427-c6ca-42c5-a33c-fd5a567eb01b.png">

> **[VM 인스턴스]** - 외부 IP 복사

<img width="1440" alt="스크린샷 2022-12-04 오전 11 04 22" src="https://user-images.githubusercontent.com/93996283/205474665-8a66c39c-5689-4b95-b627-80b702f8fa50.png">

> **아래 명령을 입력**

```bash
ssh -i [private key] [계정 ID]@[외부 IP]
```

- 정상적으로 접속된 모습

<img width="818" alt="스크린샷 2022-12-04 오전 11 06 44" src="https://user-images.githubusercontent.com/93996283/205474664-2b7a43e1-9be9-456c-93f9-33d32ba9359a.png">







## 1-3. Web Server 설치

> **S/W Update**

```bash
sudo apt-get –y update 
```

> **Apache Web Server 설치**

```bash
 sudo apt-get install apache2 
```

- 정상적으로 설치되었을 때의 화면

<img width="1042" alt="스크린샷 2022-12-04 오후 12 11 09" src="https://user-images.githubusercontent.com/93996283/205475414-a9ed68ec-5708-4187-9e26-c46c30ced994.png">

> **Nginx Server 설치**

```bash
sudo apt-get install nginx
```

<br>

---

<br>

# 2. Functions을 이용하여 기본 함수 생성

"Hello World"를 출력하는 기본 함수를 생성해보자.

## 2-1. Functions 생성

> **[서버리스] - [Cloud Functions]**

<img width="282" alt="스크린샷 2022-12-04 오후 12 21 53" src="https://user-images.githubusercontent.com/93996283/205475412-a2b3f0be-b258-403f-8b6e-7b26372533b3.png">

> **[함수 만들기]**

<img width="1438" alt="스크린샷 2022-12-04 오후 12 22 55" src="https://user-images.githubusercontent.com/93996283/205475410-74982332-af3d-4c9e-b579-4ce2ddc2a877.png">

> **[기본사항]**
>
> - **[함수 이름]** 설정
> - **[리전]** : us-central1

<img width="538" alt="스크린샷 2022-12-04 오후 12 23 35" src="https://user-images.githubusercontent.com/93996283/205475407-5ea95d1a-e9c6-4314-ba01-68a963866361.png">

>**[트리거]**
>
>- **[트리거 유형]** : HTTP
>- **[인증]** : 인증되지 않은 호출 허용
>- **[저장]**

<img width="536" alt="스크린샷 2022-12-04 오후 12 24 05" src="https://user-images.githubusercontent.com/93996283/205475577-089517f3-b82d-4531-8578-c98e81e13a31.png">

> **[런타임]** 
>
> - **[시간 제한]** : 20
> - **[자동 확장]** : 인스턴스 최소 개수 - 1, 최대 인스턴스 수 - 3
> - **[다음]**

<img width="579" alt="스크린샷 2022-12-04 오후 12 28 25" src="https://user-images.githubusercontent.com/93996283/205475403-a33d30a4-e692-4db9-9866-435291e7feeb.png">

> 하단의 **[배포]**

<img width="1438" alt="스크린샷 2022-12-04 오후 12 30 19" src="https://user-images.githubusercontent.com/93996283/205475657-5acd2ef2-5484-4384-9537-bdceacaa2d27.png">

<br>

## 2-2. URL 접속

> **[트리거]** - 트리거 URL로 접속

<img width="1438" alt="스크린샷 2022-12-04 오후 12 35 54" src="https://user-images.githubusercontent.com/93996283/205475654-3bae4c91-c05e-4e0c-9af3-24140b4b89b6.png">

> **정상적으로 접속되었을 때의 화면**

<img width="749" alt="스크린샷 2022-12-04 오후 12 36 46" src="https://user-images.githubusercontent.com/93996283/205475652-7b617f14-5aaa-4eaa-9ff2-8568392483a4.png">

cf. [인라인 편집기] 뿐만 아니라 [ZIP] 업로드 등 다른 방식을 이용하여 코드를 업로드할 수도 있다.


<img width="398" alt="스크린샷 2022-12-04 오후 12 30 00" src="https://user-images.githubusercontent.com/93996283/205475659-12f83785-6440-4dbf-9f71-816251a34b8a.png">

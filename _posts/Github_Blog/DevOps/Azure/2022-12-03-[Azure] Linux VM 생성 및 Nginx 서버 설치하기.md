---
title: "[Azure] Linux VM 생성 및 Nginx 서버 설치하기"
categories:
  - azure
tags:
  - Azure
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-03 
---

<details><summary><b>reference</b></summary>
학교 수업을 듣고 정리한 내용입니다.
</details>
<br>

> **전체적 구조**

![image](https://user-images.githubusercontent.com/93996283/205432004-40aea17d-33f1-4531-bfe6-aed95575550c.png)

<br>

---

<br>

# 1. 가상머신 생성

> **[Azure 서비스] - [가상 머신]**

<img width="1003" alt="스크린샷 2022-12-03 오후 5 46 26" src="https://user-images.githubusercontent.com/93996283/205435461-26c53506-8d74-48fb-a9e8-f9557ac22c53.png">

> **[+ 만들기] - [Azure 가상 머신]**

<img width="1004" alt="스크린샷 2022-12-03 오후 5 49 13" src="https://user-images.githubusercontent.com/93996283/205435459-6037f778-93e7-4914-a4ca-b198d06dda95.png">

> **[프로젝트 정보]**
>
> - **[구독]** : 생성되어있는 무료 구독 설정
> - **[리소스 그룹] - [새로 만들기]**

<img width="794" alt="스크린샷 2022-12-03 오후 5 55 25" src="https://user-images.githubusercontent.com/93996283/205435458-ec478ad4-2985-4e2b-aa0c-f4b4a624b370.png">

> **[인스턴스 정보]**
>
> - **[지역]** : (US) East US - 무료 계정이긴 하지만 그래도 요금이 제일 저렴한 Region 선택
> - **[가용성 옵션]** : 인프라 중복이 필요하지 않습니다.
> - **[이미지]** : Ubuntu Server 20.04 LTS - Gen2 (적격 무료 서비스)
> - **[크기]** : Standard_D2s_v3 - 2 vcpu, 8 GiB 메모리 (US$70.08/월)

<img width="796" alt="스크린샷 2022-12-03 오후 5 59 56" src="https://user-images.githubusercontent.com/93996283/205436196-e1b01acd-8e24-4e3f-aeb1-ed61ed50a23f.png">

> **[관리자 계정]**
>
> - **[사용자 이름]** 설정 - 이때 설정한 사용자 이름이 콘솔 접속 시 사용된다.

<img width="766" alt="스크린샷 2022-12-03 오후 6 02 07" src="https://user-images.githubusercontent.com/93996283/205435942-76768b37-c8da-4a3d-aeb4-5cdb39a6d1d3.png">

> **[인바운드 포트 규칙]**  설정 후 **[다음:디스크>]**
>
> - **[공용 인바운드 포트]** : 선택한 포트 허용
> - **[인바운드 포트 선택]** : HTTP(80), SSH(22)만 허용

<img width="765" alt="스크린샷 2022-12-03 오후 7 26 26" src="https://user-images.githubusercontent.com/93996283/205436395-2b39874c-791b-4211-bf07-de54bb6d2087.png">

> **[디스크], [네트워킹], [관리], [Monitoring], [고급], [태그], [검토]**는 따로 수정 사항 없이 넘어간다.

<img width="770" alt="스크린샷 2022-12-03 오후 7 32 08" src="https://user-images.githubusercontent.com/93996283/205436566-abbed284-e47b-4347-a5bd-f9971b3c6e66.png">



> **[검토 + 만들기]**
>
> - 하단의 **[만들기]** 클릭

<img width="795" alt="스크린샷 2022-12-03 오후 6 06 34" src="https://user-images.githubusercontent.com/93996283/205436601-988cc696-cde4-4c0e-b016-efeb069c1a60.png">

> **새 키 쌍 생성**
>
> - **[프라이빗 키 다운로드 및 리소스 만들기]**
>
>   다운로드 된 .pem 파일은 local 폴더에 잘 보관해둔다.

<img width="794" alt="스크린샷 2022-12-03 오후 6 06 53" src="https://user-images.githubusercontent.com/93996283/205436625-a1700ef0-33f5-4069-ac4b-b9428ac4a0b5.png">

> **배포 완료된 모습**

<img width="1212" alt="스크린샷 2022-12-03 오후 6 22 59" src="https://user-images.githubusercontent.com/93996283/205436697-6c1af4f1-38f7-4d3b-9e8e-07666fcf597a.png">

- **[홈] - [리소스]**에서 생성된 VM과 리소스 그룹을 확인할 수 있다.

<img width="718" alt="스크린샷 2022-12-03 오후 6 24 44" src="https://user-images.githubusercontent.com/93996283/205436717-d6863732-a69d-4fd8-b7f3-017e6113f9fe.png">

<br>

---

<br>

# 2. VM에 연결

>**key 파일 모드 변경**

```bash
sudo chmod 400 [key 파일 이름].pem
```

> **퍼블릭 IP 확인**

<img width="947" alt="스크린샷 2022-12-03 오후 6 27 16" src="https://user-images.githubusercontent.com/93996283/205436986-493b2d0a-b4e1-4cc7-951b-53d90e600958.png">

> **접속 시도**

터미널에서 key 파일이 있는 디렉토리로 이동하여 접속한다. (Windows는 Gitbash 사용)

```bash
ssh -i [key 파일 이름].pem [사용자 이름]@[ip 주소]
```

> **접속 성공한 모습**

<img width="762" alt="스크린샷 2022-12-03 오후 7 48 59" src="https://user-images.githubusercontent.com/93996283/205437138-616542ee-e60c-4b17-911b-a894ea0b6292.png">

<br>

---

<br>

# 3. Nginx 서버 설치

> **S/W 업데이트**

```bash
sudo apt-get -y update
```

> **Nginx 설치**

```bash
sudo apt-get -y install nginx
```

> **동작 확인** - 브라우저에 IP 입력

- 정상적으로 접속시 화면

<img width="886" alt="스크린샷 2022-12-03 오후 6 30 28" src="https://user-images.githubusercontent.com/93996283/205435404-8ee0c485-b394-4868-9c74-efba70bc6eb8.png">




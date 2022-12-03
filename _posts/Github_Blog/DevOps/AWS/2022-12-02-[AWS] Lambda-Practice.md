---
title: "[AWS] Lambda - Practice"
categories:
  - aws
tags:
  - AWS
  - Lambda
  - API Gateway
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-02 02:00:00
---

<details><summary><b>reference</b></summary>
학교 수업을 듣고 정리한 내용입니다.
</details>
<br>

# 1. 기본 함수 사용

## 1-1. Lambda 콘솔로 이동

<img width="996" alt="스크린샷 2022-12-02 오후 4 26 30" src="https://user-images.githubusercontent.com/93996283/205241623-539c6e4f-682e-433d-a3fb-71db739fa0a1.png">

## 1-2. Lambda 함수 생성

> **[블루프린트 사용]** 체크
>
> **[블루프린트]** - **[hello-world-python]** 을 검색한 후, 선택한 다음 **[구성]**

<img width="952" alt="스크린샷 2022-12-02 오후 4 27 19" src="https://user-images.githubusercontent.com/93996283/205241629-26bc64e0-fd15-40fb-8a42-435b6231a8cb.png">

## 1-3. 기본 정보 설정 및 함수 생성

> **새 역할 생성 시, IAM에 추가된다.**

<img width="864" alt="스크린샷 2022-12-02 오후 4 28 32" src="https://user-images.githubusercontent.com/93996283/205241972-04323695-5259-4e1d-9d8f-f033847add63.png">

> **생성된 Lambda 함수 코드**
>
> - event가 발생하면 `key1`을 return 한다.

<img width="841" alt="스크린샷 2022-12-02 오후 4 33 11" src="https://user-images.githubusercontent.com/93996283/205242102-f6576632-83dc-46ed-9705-0566c7c75c2d.png">

## **1-4. 테스트 이벤트 생성 후 테스트**

> `key1`, `key2`, `key3` 각각에 출력할 값을 넣고, **[테스트]** 버튼을 눌러 이벤트를 실행한다.

<img width="891" alt="스크린샷 2022-12-02 오후 4 36 19" src="https://user-images.githubusercontent.com/93996283/205242278-063a61b8-cb93-46c4-a79f-79257f32dc0f.png">

> **실행 결과**
>
> - "Hello World"가 출력된 것을 확인할 수 있다.

<img width="844" alt="스크린샷 2022-12-02 오후 6 42 37" src="https://user-images.githubusercontent.com/93996283/205263649-2b510655-3b2c-4ae7-8817-778eab8853f2.png">

## **1-5. 함수 코드 수정 후 테스트**

> `key2`가 return 되도록 코드를 수정한다.
>
> - **[File] - [Save]** 후,  **[Deploy]** 버튼 까지 눌러야 수정 사항이 정상적으로 반영된다.

<img width="897" alt="스크린샷 2022-12-02 오후 4 37 39" src="https://user-images.githubusercontent.com/93996283/205243116-8fb77fdf-f0a3-4893-bf8d-ff67401678f8.png">

> **실행 결과**
>
> - "by ljs"가 출력된 것을 확인할 수 있다.

<img width="939" alt="스크린샷 2022-12-02 오후 4 38 24" src="https://user-images.githubusercontent.com/93996283/205243341-cd2886e3-0edf-48fc-90fd-f51c4bef73dd.png">

## **1-6. 리소스 삭제**

> **[Lambda] - [함수] 삭제**

<img width="939" alt="스크린샷 2022-12-02 오후 4 40 05" src="https://user-images.githubusercontent.com/93996283/205244052-bc11f081-ca64-4759-9b28-0b6782c20bab.png">

> **[CloudWatch] - [로그 그룹] 삭제**

<img width="1038" alt="스크린샷 2022-12-02 오후 4 40 33" src="https://user-images.githubusercontent.com/93996283/205243915-b6e5615c-86dd-4039-b1ff-934beb39ccec.png">

> **[IAM] - [역할] - [labda_basic_execution] 삭제**

<img width="1013" alt="스크린샷 2022-12-02 오후 4 41 12" src="https://user-images.githubusercontent.com/93996283/205244190-5f953da4-2c26-4a51-8d28-8b2ee2c13a3b.png">

<br>

<br>

# 2. palindrome을 검사하는 isPalindrome 함수 생성

- **palindrome이란?** : 우리 말로 **회문**으로 번역되며, 'eye', 'madam' 처럼 역순으로 읽어도 제대로 읽은 것과 같은 문자열, 낱말, 숫 등을 말한다.

## 2-1. Lambda 함수 생성

> **[새로 작성]** ,  **[런타임]** : Node.js 12.x

<img width="884" alt="스크린샷 2022-12-02 오후 5 28 45" src="https://user-images.githubusercontent.com/93996283/205252478-a551f4ee-369b-4a84-932f-301bb3c3c660.png">

> **[기본 실행 역할 변경] - [정책 템플릿] - [단순 마이크로서비스 권한]**으로 설정

<img width="877" alt="스크린샷 2022-12-02 오후 5 29 26" src="https://user-images.githubusercontent.com/93996283/205252409-26c3efa4-3260-44bc-90c5-75290c5fd026.png">



## 2-2. palindrome 검사 코드 작성

```javascript
exports.handler = async (event, context, callback) => { 
    let isPalindrome, rev, key, result='';
    for (key in event) {
        rev = event[key].split('').reverse().join('');
        isPalindrome = (event[key] == rev);
        result += isPalindrome ? `${event[key]} is a Palindrome : ` : `${event[key]} is not a Palindrome : `;
    }
    callback(null, result);
};
```

<img width="1222" alt="스크린샷 2022-12-02 오후 5 35 27" src="https://user-images.githubusercontent.com/93996283/205251046-342bffcb-2bd8-449e-89bc-59e1fe6549cb.png">

## 2-3. 테스트 이벤트 생성

> 검사를 할 단어들을 `key1`, `key2`, `key3` 넣은 후 **[저장]**

<img width="926" alt="스크린샷 2022-12-02 오후 5 32 08" src="https://user-images.githubusercontent.com/93996283/205251056-c936b83e-fbc4-49b4-9214-01aa2212d9e8.png">

## 2-4. 테스트 후 출력 결과 확인

> 각각의 key에 대한  `isPalindrome` 함수 결과 값을 확인할 수 있다.

<img width="1225" alt="스크린샷 2022-12-02 오후 5 35 43" src="https://user-images.githubusercontent.com/93996283/205251030-4a681a2a-df3f-4984-be43-166da0bd6e61.png">

<br>

<br>

# 3. isPalindrome 함수와 API Gateway 연결

- **Lambda와 HTTP 통신** : 웹 사이트 접속을 통해 오는 요청을 처리하기 

## 3-1. `isPalindrome` 코드 수정

```javascript
exports.handler = async (event, context, callback) => { 
    const string = event.string;
    const reverse = string.split('').reverse().join('');
    const isPalindrome = (string == reverse);
    const result = isPalindrome ? `${string} is a palindrome` : `${string} is not a palindrome`;
    
    callback(null, result);
};
```

![스크린샷 2022-12-02 오후 6 00 32](https://user-images.githubusercontent.com/93996283/205257050-cdfc7e57-0f7c-4a26-aa42-b00c62b72ddc.png)

## 3-2. API Gateway 생성

>  **[API Gateway] - [REST API]** 구축

<img width="1059" alt="스크린샷 2022-12-02 오후 5 51 17" src="https://user-images.githubusercontent.com/93996283/205257261-30bda17e-1507-4f4b-9db2-f1f578434a0d.png">

> **[새 API 생성] - [API 이름]** 설정 후 **[API 생성]**

<img width="1059" alt="스크린샷 2022-12-02 오후 6 11 16" src="https://user-images.githubusercontent.com/93996283/205257557-5fa11153-d3d6-45ea-994f-2db7df364f87.png">

## 3-3. GET 메서드 생성 및 설정

- **[리소스] - [작업] - [메서드 생성]**

<img width="1030" alt="스크린샷 2022-12-02 오후 5 52 46" src="https://user-images.githubusercontent.com/93996283/205257980-f1ffd745-3281-4180-92a7-1c0b1894d9b5.png">

> `GET` 메서드 생성 후, **[Lambda 함수]** - `isPalindrome` 함수 설정 - **[저장]**

<img width="1108" alt="스크린샷 2022-12-02 오후 5 53 26" src="https://user-images.githubusercontent.com/93996283/205258209-507154b2-8d33-4a0c-adad-a656e4715b0d.png">

> **[통합 요청]** 

<img width="1100" alt="205258123-f983c084-48d6-4ae4-aab1-06191ed34af8" src="https://user-images.githubusercontent.com/93996283/205264997-caeec8cb-7cd1-4e4c-ad8e-fb5ea78baa78.png">

> JSON 형식의 **[매핑 템플릿]** 설정 - **[저장]**

<img width="872" alt="스크린샷 2022-12-02 오후 5 55 49" src="https://user-images.githubusercontent.com/93996283/205258830-b34d6f15-a6dc-44ed-a22d-8ec6dd277f59.png">

## 3-4. API 배포 (Deploy)

> **[작업] - [API 배포]**

<img width="323" alt="스크린샷 2022-12-02 오후 5 56 15" src="https://user-images.githubusercontent.com/93996283/205259303-6000a26b-a3a3-4cad-a0a5-06a936cc411c.png">

> **[스테이지 이름]** 설정 후 **[배포]**

<img width="584" alt="스크린샷 2022-12-02 오후 5 56 27" src="https://user-images.githubusercontent.com/93996283/205259456-3489a579-adf6-4f1a-8d47-0ba2e9276b9d.png">

> `isPalindrome` 함수에 `API Gateway`가 연결된 것을 확인할 수 있다.

<img width="804" alt="스크린샷 2022-12-02 오후 6 05 42" src="https://user-images.githubusercontent.com/93996283/205260476-090f8fe6-5686-423b-871e-402c373f727c.png">

## 3-5. URL 호출

> API 배포 후, 생성된 엔드포인트 확인

<img width="1112" alt="스크린샷 2022-12-02 오후 5 56 53" src="https://user-images.githubusercontent.com/93996283/205259410-20c60cbc-86a5-42ce-9958-38cddb735008.png">

> URL 접속 화면

<img width="1106" alt="스크린샷 2022-12-02 오후 6 03 27" src="https://user-images.githubusercontent.com/93996283/205259856-9fd33b7f-bf8a-430b-97c4-776182ed42c3.png">

## 3-6. palindrome 테스트

> URL 뒤에 `?string=[단어]` 형식의 **querystring**을 추가하여 테스트 해볼 수 있다.

<img width="1106" alt="스크린샷 2022-12-02 오후 6 03 32" src="https://user-images.githubusercontent.com/93996283/205259852-967ec1ea-035a-41e5-89fd-e02515a41e0b.png">

<img width="1106" alt="스크린샷 2022-12-02 오후 6 04 09" src="https://user-images.githubusercontent.com/93996283/205259843-ff3ad89b-6f73-46d3-8952-813fecb8a205.png">
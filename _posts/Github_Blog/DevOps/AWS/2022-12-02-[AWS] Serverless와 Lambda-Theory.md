---
title: "[AWS] Serverless와 Lambda - Theory"
categories:
  - aws
tags:
  - AWS
  - Serverless
  - Lambda
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-02 01:00:00
---

<details><summary><b>reference</b></summary>
학교 수업을 듣고 정리한 내용입니다.
</details>
<br>

# Serverless란?

- **사용량에 따라 백엔드 서비스를 제공하는 방법**
- 물리적 서버는 사용되며 개발자는 서버를 알 필요가 없다.
- 운영상의 책임을 클라우드로 전환한다.
- 서버를 고려하지 않고 application과 server를 구축하고 실행한다.
- 거의 모든 application, 백엔드 서비스가 구축이 가능하다.
- 고가용성 실행/확장에 필요한 사항이 자동으로 처리 된다.

> **웹 애플리케이션 구축 역사**

1. 서버 보유
2. 클라우드 시대 - 고정 개수 서버나 서버 공간을 대여한다.
3. 서버리스 - 고정 대역폭이나 서버 개수를 유지하지 않아도 된다.

<br>

## 사용 이유

- 빠르고, 적은 비용으로 최신 application 개발이 가능하다.
- 개발자는 개발에만 집중할 수 있는 환경이 주어진다.

<br>

## AWS Serverless Platform

- **serverless application 구축/실행을 위한 완전 관리형 서비스를 제공**
- 백엔드 구성 요소를 프로비저닝 해준다. 
- *플리케이션의 내결함성과 가용성에 대해 고려하지 않아도 된다.

### - 종류

- **Computing** : Lambda, Lambda@Edge, Fargate
- **Storage** : S3, EFS(Elastic File System)
- **Data Store** : Dynamo DB, Aurora Serverless
- **API Proxy** : API Gateway
- **Application 통합** : SNS, SQS, AppSync, EventBridge
- **Ochestration** : Step Functions
- **분석** : Kinesis, Athena
- **개발자 도구**

<br>

## 이점

- 낮은 비용 - 종량제 요금
- 서버 관리의 불필요
- 유연한 규모 조정 : 간편한 확장성
- 자동화된 고가용성
- 빠른 개발 : 복잡한 배포 과정과 버그 수정 대신, 필요에 따라 코드 추가/수정하는 방향으로 개발을 진행한다.

<br>

## Application 구축 사례

### 웹 애플리케이션과 백엔드 구축 사례 

- `Lambda`, `API Gateway`, `S3`, `Dynamo DB` 사용
- **예1) 날씨 애플리케이션**



![image](https://user-images.githubusercontent.com/93996283/205098782-80844eae-20c4-4237-a020-e575dc584e8a.png)

#### API Gateway란?

최근에는 **애플리케이션이 독립적인 구성 요소로 구축되어 각 애플리케이션 프로세스가 서비스로 실행되는** `마이크로서비스 아키텍처` 방식이 많이 사용되고 있다. 아래의 그림을 살펴보자.

![image](https://user-images.githubusercontent.com/93996283/205098814-2780df0f-febe-40ed-ad81-2e0b48f29cd4.png)

클라이언로부터 `/blog-account`, `/blog-post`, `/blog-storage` 라는 request가 오면, 각각에 해당하는 응답은 Microservice Account, Microservice Post, Microservice Storage이다.

이러한 **마이크로서비스**(Account, Post, Storage)**를 지원하는 도구**가  `API Gateway`이다. 클라이언트와 서비스 사이에 하나의 **엔드포인트**를 두는 것이다. `API Gateway`는 <u>클라이언트가 요청한 request에 맞는 서비스를 라우팅 해주는 역할을 한다.</u>

<br>

- **예2) 소셜 미디어 앱에 대한 모바일 백엔드**

![image](https://user-images.githubusercontent.com/93996283/205101753-946860d3-57bd-49d0-8e2b-cab71596a1e4.png)

<br>

### 실시간 데이터 처리 시스템 구축 사례

- `Lambda`, `Kinesis`, `S3`, `Dynamo DB` 사용

- **예1) 이미지 썸네일 생성**

  ![image](https://user-images.githubusercontent.com/93996283/205101762-1476de81-918e-49df-9930-b708e23b052f.png)

- **예2) 스트리밍 소셜 미디어 데이터 분석** 

![image](https://user-images.githubusercontent.com/93996283/205101773-b2640fef-0dc2-4b7e-b6ce-65dfe3d9eddc.png)

<br>

<br>

# AWS Lambda

> **AWS 공식 유튜브에 올라온 Lambda 소개 영상** 👍🏻 - [<span style="color:skyblue">https://youtu.be/eOBq__h4OJ4</span>](https://youtu.be/eOBq__h4OJ4)

## AWS Lambda란?

- **서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있게 해주는 컴퓨팅 서비스**
- 사용한 컴퓨팅 시간에 대해서만 과금한다.
- 모든 유형의 애플리케이션이나 백엔드 서비스에 대한 코드를 별도의 관리 없이 실행할 수 있다.
- 코드를 업로드하기만 하면, Lambda에서 높은 가용성으로 코드 실행 및 확장하는데 필요한 모든 것을 처리해준다.
- 다른 AWS 서비스에서 코드를 자동으로 트리거하도록 설정하거나 웹 또는 모바일 앱에서 직접 코드를 호출한다.

<br>

## What to do?

- 고가용성 컴퓨팅 인프라에서 코드를 실행한다.
- 서버 및 운영 체제를 유지하고 관리해준다.
- 용량을 프로비저닝 및 자동으로 조정해준다.
- 코드 및 보안 패치를 배포하는데 사용될 수 있다.
- 코드의 모니터링 및 로깅을 해준다.
- 모든 컴퓨팅 리소스를  관리해준다.

<br>

## 이점

- 서버 관리가 불필요하다.
- 지속적으로 규모를 조정해준다.
- 밀리초 단위의 측정이 가능하다.

<br>

## Event 기반 실행환경

- **Event 예**
  - S3 bucket이나 Dynamo DB table의 데이터 변화
  - Amazon API Gateway를 이용한 HTTP 요청에 대한 응답
  - AWS SDK를 이용한 API 호출

<br>

## 작동 방식

![image](https://user-images.githubusercontent.com/93996283/205110504-11b2406a-96e9-416c-80e4-4169cd2c67e2.png)

<br>

## 사용 사례 - 데이터 처리

- **예1) 실시간 파일 처리** : `Lambda`, `S3`
  - `S3`에 파일을 업로드 하는 즉시 데이터를 처리하도록 Lambda 트리거
  - 이미지 썸네일, 동영상 트랜스코딩, 파일 인덱싱, 로그 처리, 콘텐츠 검증, 데이터 수집/필터링 등
  - **The Seattle Times** 회사의 사례
    - 기자가 찍은 사진을 `S3`에 올리면 다양한 디바이스(데스크톱 컴퓨터, 태블릿, 스마트폰 등 )에서 볼 수 있도록 이미지 크기를 조정해주는 함수를 만든 후, `S3`에 변경이 생길 때마다 트리거 되도 설정을 해두었다.
    - [<span style="color:skyblue"><b>Serverless-실시간 데이터 처리 시스템 구축 사례-예1</b></span>](http://1eejisoo.github.io/aws/AWS-Serverless%EC%99%80-Lambda-%EC%9D%B4%EB%A1%A0/#%EC%8B%A4%EC%8B%9C%EA%B0%84-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%B2%98%EB%A6%AC-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%B6%95-%EC%82%AC%EB%A1%80)에서 구축 사례 사진을 볼 수 있다.
    - 참고 자료 : [<span style="color:skyblue">https://aws.amazon.com/ko/solutions/case-studies/the-seattle-times/</span>](https://aws.amazon.com/ko/solutions/case-studies/the-seattle-times/)

<br>

- **예2) 실시간 스트림 처리** : `Lambda`, `Kinesis`

  - 애플리케이션 활동 추적
  - 트랜잭션 주문 처리
  - 클릭 스트림 분석
  - 데이터 정리
  - 지표 생성
  - 로그 필터링
  - 인덱싱, 소셜 미디어 분석 등
  - **Localytics** 회사의 사례
    - 실시간으로 수십억 개의 데이터 포인트를 처리하고, `Lambda`를 사용하여 `S3`에 저장되거나 `Kinesis`에서 스트리밍 된 기록 데이터 및 실시간 데이터를 처리하였다.
    - [<span style="color:skyblue"><b>Serverless-실시간 데이터 처리 시스템 구축 사례-예2</b></span>](http://1eejisoo.github.io/aws/AWS-Serverless%EC%99%80-Lambda-%EC%9D%B4%EB%A1%A0/#%EC%8B%A4%EC%8B%9C%EA%B0%84-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%B2%98%EB%A6%AC-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%B6%95-%EC%82%AC%EB%A1%80)에서 구축 사례 사진을 볼 수 있다.
    - 참고 자료 : [<span style="color:skyblue">https://aws.amazon.com/ko/solutions/case-studies/localytics/</span>](https://aws.amazon.com/ko/solutions/case-studies/localytics/)

  <br>

## 사용 사례 - 백엔드

- **예1) IOT 백엔드** 

  - 웹, 모바일, 사물 인터넷 및 타사 API 요청

  ![image](https://user-images.githubusercontent.com/93996283/205116825-b13d4fda-9f56-4aa0-9189-1bf72fefaa35.png)



<br>

- **예2) 모바일 백엔드**

  - API 요청을 인증 및 처리하도록 백엔드 구성 -> 개인화된 앱 환경을 손쉽게 생성할 수 있다.

  ![image](https://user-images.githubusercontent.com/93996283/205116870-03137d91-44db-4f7c-90f2-2dd22f7fe501.png)

  - **Bustle** 회사의 사례
    - AWS Lambda와 Amazon API Gateway를 사용하여 Bustle iOS 앱 및 웹 사이트에 대해 Serverless 백엔드를 실행했다.

<br>

- **예3)  웹 애플리케이션** 

  - Lambda를 다른 AWS 서비스와 결합
  - 가용성 높은 구성에서 실행되는 강력한 웹 애플리케이션이 구축 가능하다.

  ![image](https://user-images.githubusercontent.com/93996283/205116896-89c8f8f7-b288-4b6c-8bf2-0ee906a3887a.png)

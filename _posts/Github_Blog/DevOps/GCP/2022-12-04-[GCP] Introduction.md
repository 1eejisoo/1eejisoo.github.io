---
title: "[GCP] Introduction"
categories:
  - gcp
tags:
  - gcp
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-04 01:00:00
---

<details><summary><b>reference</b></summary>
학교 수업을 듣고 정리한 내용입니다.
</details>

<br>

# 개요

## GCP란?

검색과 유튜브와 같은 최종 사용자 제품을 위해 내부적으로 구글이 사용하는, 동일한 지원 Infrastructure 위에서 호스팅을 제공하는 구글의 클라우드 컴퓨팅 서비스

- 2011년 10월 6일 발표

- 2019년 5월 기준으로 Regin 20개, Zone 61개, Edge Location 134개 



## 서비스

- App Engine, Compute Engine, BigQuery, AI products 등

![image](https://user-images.githubusercontent.com/93996283/205451589-44049c4c-e97f-4e51-a539-0bb2982c8577.png)

![image](https://user-images.githubusercontent.com/93996283/205451951-f0b5497b-a116-410b-a53a-f0e82004eff3.png)

<br>

## 활용 사례

> **위메프**

- BigQuery : 로그 데이터 관리를 위한 데이터 웨어 하우스
- Google Analytics 360 : 로그 분석

> **BestBuy**

- App Engine : 인력과 시간 절감

> **Skyscanner**

- Google Analytics 360 : 분석 시스템
- Big Query : 분석 시스템

> **Vimeo**

- Cloud Storage : 지연 시간 감축, 높은 처리량
- Compute : 동영상에 대한 확장성 확보

<br>

---

<br>

# 기본 개념

> **GCP 리소스 (= 데이터 센터)**

- **[Region] - [Detail Region] - [Zone]**의 형태로 표시
  - asia-east1-a

---

> **프로젝트**

- namespace 역할
- 모든 GCP 리소스는 하나의 프로젝트에 속해야 한다.
- 하나의 계정으로 여러 프로젝트를 만들어 관리할 수 있다. - 각 프로젝트는 독립적 환경

---

> **GCP 클라우드 콘솔**

- **프로젝트 및 리소스 관리를 위한 웹 기반 GUI 환경**
  - AWS Management Console, Azure Portal과 비슷한 개념
- 대시보드
- 클라우드 쉘
  - 웹 브라우저 인스턴스에 대한 CLI
  - vim, emacs editor 제공
  - 5GB repository 제공
  - Google Cloud SDK와 다른 도구들이 설치되어 있음
  - Java, Go, Python, Node.js, PHP, Ruby, .NET 등의 언어 지원

---

> **클라우드 SDK (gcloud)**

- 명령으로 GCP에 액세스 할 수 있는 CLI 도구

---

> **클라이언트 라이브러리**

- Google Cloud API를 호출하기 위한 라이브러리
- 서비스 계정 키 설정 + gcloud 설정

<br>

---

<br>

# 대표 서비스

## Compute

- **App Engine** : PaaS / AWS의 EB와 비슷한 개념
- **Container Engine** : Kubernetes 기반의 Docker 런타임
- **Compute Engine** : IaaS / AWS의 EC2와 비슷한 개념

![image](https://user-images.githubusercontent.com/93996283/205453033-d3310539-beeb-426f-9f3b-f0d0aa9976cd.png)

### Compute Engine

- 가상 머신 서비스이며 다양한 사양의 인스턴스를 제공한다.
- 초 단위로 과금되며 비용을 절감할 수 있다.
- 머신 유형
  - 사전 정의된 유형 : 표준형, 고성능 메모리형, 고성능 CPU형
  - 커스텀 머신 유형
  - 다양한 CPU Platform
  - GPU : Tesla T4, Tesla P4, Tesla V100 ...
- **Live Migration** (실시간 이전)
  - S/W, H/W 업데이트 중에도 인스턴스를 종료, 재부팅할 필요 없이 계속 실행시키는 기능을 말한다.
- **Preemptible VM instances** (선점형 VM 인스턴스)
  - 아무도 사용하고 있지 않은 리소스를 사용하여 비용을 절감한다.
  - 최대 24시간만 이용 가능하다.
- **인스턴스 그룹**
  - 관리형
    - 인스턴스 템플릿을 이용하여 **동일한** 인스턴스 그룹을 생성
    - 자동 Auto Scaling 및 자동 복구 정책
    - Load balancer를 붙여 트래픽을 분산시킨다.
    - 영역 관리형 VS 리전 관리형
    - 컨테이너를 이용한 애플리케이션 배포 간소화
  - 비관리형
    - 서로 다른 사양을 가진 인스턴스 그룹을 생성

<br>

<br>

## Storage

### Cloud Storage

- **대표적인 객체 Repository** (AWS의 S3와 비슷한 개념)

- Highly scalable immutable object/blob storage
- No capacity planning required
- **주요 개념** 
  - 객체, 버킷, 지리적 중복, 객체 불변성
  - repository 등급 : multi-regional, regional, nearline, coldline

---

### Cloud Datastore

- NoSQL database

- fully managed service

- fast and high scalable

---

### Cloud Bigtable

- Massible scalable NoSQL

- Hadoop ecosystem과 호환

- Gmail, Google Analytics에서 이용됨

---

### Cloud SQL

- managed by MySQL

- data 자동 암호화

- automatic failover for high availability

<br>

<br>

## Big Data

### BigQuery

- **대규모 저장 및 분석 플랫폼**
- **기업용 Serverless 기반의 데이터 웨어 하우스**
- SQL like syntax for querying
- 몇 초 만에 기가바이트 급에서 페타바이트 급에 이르는 데이터를 초고속으로 SQL query 실행을 한다.
- 배치, 스트리밍 데이터 분석
- 스트리밍 수집 기능 : 실시간 데이터 캡처, 분석
- BigQuery ML : SQL query로 ML model 학습

<br>

<Br>

## Machine Learning 

### Cloud ML

- TPU를 이용하여 실행됨
- 자신만의 ML Service를 개발하려는 사용자에게 적합하게 쓰일 수 있다.
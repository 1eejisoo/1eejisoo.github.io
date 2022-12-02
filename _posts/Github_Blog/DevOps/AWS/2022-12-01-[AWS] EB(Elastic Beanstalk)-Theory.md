---
title: "[AWS] EB(Elastic Beanstalk) - Theory"
categories:
  - aws
tags:
  - AWS
  - EB
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-01
---



<img width="668" alt="스크린샷 2022-12-01 오후 9 24 59" src="https://user-images.githubusercontent.com/93996283/205056408-6bff04d6-0e81-4fb7-99f7-0f010a2e6ce2.png">

- 애플리케이션(JAVA, PHP, Python, .NET, Node.js, RUBY, Docker 등)을 제공하면 애플리케이션을 서비스하는 여러가지 Infra Structure를 자동으로 만들어 준다.
- 탄성있게 필요한 양 만큼만의 실행 환경을 만들어준다.

<br>

# What?

- 애플리케이션을 쉽게 배포할 수 있고, 운영 및 관리를 지원하는 AWS 서비스
- **프로비저닝(provisioning)의 결정체**이다. 
  - <u><b>프로비저닝이란?</b> 어떠한 서비스를 위해 필요한 자원들을 준비하는 것을 말한다.</u>
  
- application을 저장/실행하는데 필요한 자원에 대한 비용만 지불하면 된다.
- **Easy-to-use service for deploying and scaling web applications and services**
  - 웹 애플리케이션이나 서비스의 배포나 규모 확장/축소에 있어 용이하게 해주는 서비스
- 사용자가 Upload만 하면, EB가 capacity provisioning, load balancing, auto scaling, health monitoring 등의 모든 배포를 자동으로 관리해준다.

<br>

# 장점

- **fast and simple to begin**
  - AWS management console, Git repository, IDE(Visual Studio), Eclipse 등을 통해서 가능하다.
  - 수분 내에 application이 준비됨 : infrastructure나 resource configuration을 하지 않아도 된다.
- **Developer productivity**
  - 개발자는 application 개발에만 집중할 수 있다.
  - application을 실행하는 platform을 최신으로 유지시켜준다.

- **Complete resource control**
  - 최적의 resource를 user가 선택할 수도 있다. (인스턴스 타입 등)

<br>

# 특징

- `auto-scaling`과 `load-balancing` 환경을 제공해준다.
- `EB dashboard`를 통해 아래와 같은 기능을 설정할 수 있다.
  - EC2 최대 개수 지정
  - instance 추가/삭제를 위한 triggering rule 추가
  - static file 캐싱을 위한 proxy server 선택
  - application health monitoring 활성화
  - alarm(경고) 생성

<br>

# EB 기초

<img width="555" alt="스크린샷 2022-12-01 오후 9 46 25" src="https://user-images.githubusercontent.com/93996283/205056455-aa1e3ad5-1027-4ae1-9280-288db753d133.png">

![image](https://user-images.githubusercontent.com/93996283/205056815-3119f023-a3a8-40ea-b34e-a470d7bdbf9e.png)

## Application

- 상위 개념

- **project의 folder** 역할을 한다.
  - EB application 내에서 실행되지 않고, project folder가 배포되면서 그 **환경(environment)** 안에서 실행된다.

## Environment

- 하위 개념

- application이 실행될 수 있는 환경이며, EB application 내에 만든다.

- application의 서로 다른 실행 버전을 관리해준다.
  - 예를 들어, 개발 단계의 환경과 배포 단계의 환경이 다를 수 있기 때문에 이러한 버전을 관리해준다.

## Environment tier

- `Web Server tier` : HTTP(S) request를 다룬다.
- `Worker tier` : background process를 다룬다.

## Environment health

- `green` : Good!
- `gray` : Environment가 변할 때 나타난다. (ex. Environment가 생성 중일때)
- `yellow` : 경고를 나타낸다.
- `red` : 문제가 있어서 Environment에서 application이 실행되지 않는 상태를 말한다.

## EB 사용 도구

- management console
- eb-Elastic Beanstalk CLI
- Web API

## EB Architecture

![image](https://user-images.githubusercontent.com/93996283/205059478-c2fae7da-eb4e-4b64-b970-d3d689ce8c56.png)

- `CNAME` : Environment에 대한 human-readable **URL** (이 URL(CNAME)은 `Load Balancer`에 할당된다.)
- `Load Balancer` : traffic을 multiple instance로 보낸다.
- `Auto Scaling Group` traffic을 처리할 때, instancße를 선정하고 instance의 개수를 증가/감소 시킨다.
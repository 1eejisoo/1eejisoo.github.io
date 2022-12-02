---
title: "[Azure] Introduction"
categories:
  - azure
tags:
  - Azure
toc_label: "목차"
toc: true
toc_sticky: true
date: 2022-12-02 03:00:00
---

<details><summary><b>reference</b></summary>
학교 수업을 듣고 정리한 내용입니다.
</details>

<br>

# Azure란?

> **2010년 2월 Microsoft에서 개발한 Cloud Computing Platform**

<img width="808" alt="스크린샷 2022-12-02 오후 8 20 07" src="https://user-images.githubusercontent.com/93996283/205281482-ee87b4f8-fdca-4907-9674-8ee999909eab.png">

<img width="900" alt="스크린샷 2022-12-02 오후 8 30 17" src="https://user-images.githubusercontent.com/93996283/205283313-4f6ce396-88c8-49ae-b2d0-80621e2da70f.png">

- **완전한 클라우드 컴퓨팅 플랫폼** - 응용 프로그램 개발, 테스트, 배포, 관리를 위한 클라우드 서비스를 통합
- 선호하는 도구, 프레임워크를 사용하여 글로벌 네트워크에서 application을 자유롭게 빌드, 관리, 배포할 수 있다.
- 기존 응용 프로그램을 호스트할 수 있다.
- 새 응용 프로그램의 개발을 간소화한다.
- on-premise 응용 프로그램 향상
- AI 및 기계 학습 서비스 제공 - 시각, 청각, 음성
- 저장소 솔루션 제공
- 그 밖에도 development, data storage, service hosting, service management 등을 제공한다.

<br>

<br>

# Azure의 서비스

![image](https://user-images.githubusercontent.com/93996283/205283750-61437130-2051-4863-9c6e-a36f97aa3b14.png)

![image](https://user-images.githubusercontent.com/93996283/205284060-3210012a-7d4c-47a9-bdca-7b966676c7f2.png)

## Application 호스팅

- 인프라 세부 정보에 대한 걱정 없이 application을 실행할 수 있는 다양한 클라우드 기반 컴퓨팅 제공 사항을 지원한다.
- **응용 프로그램 호스트 방법 결정**
  - 전체 인프라를 VM으로 관리 - *IaaS*
  - Azure에서 제공하는 플랫폼 관리 기능 사용 - *PaaS*
  - 코드 실행만 호스트하는 서버를 사용하지 않는 프레임워크 - *Functions*

<img width="918" alt="스크린샷 2022-12-02 오후 8 42 22" src="https://user-images.githubusercontent.com/93996283/205285238-bc902c5d-c935-4418-8aba-ffb4585c3532.png">

- **IaaS** 
  - 호스팅에 대한 모든 권한을 제공한다.
  - 코드가 실행되는 VM을 자세히 제어할 경우에 사용한다.
- **PaaS**
  - 앱을 지원하는데 필요한 완전히 관리되는 서비스를 제공한다.
  - **App Service** : 대부분의 웹 사이트나 웹 응용프로그램을 호스팅 하는데 쓰인다.
  - **Service Fabric** : 마이크로 서비스 아키텍처의 경우에 쓰인다.
- **Functions**
  - 서버를 사용하지 않는 호스팅 (코드만 작성)

---

### Azure Virtual Machines

- **IaaS**
- Windows / Linux VM 배포 지원
- 사용자가 컴퓨터 구성에 대한 모든 제어 권한을 갖는다.
- 사용자가 모든 서버 S/W 설치, 구성, 유지 관리, OS 패치를 담당한다.

>  **특징**

- `Size`
- `Region`
- `Network` : 가상 네트워크, 네트워크 보안 그룹
- `Resource Groups`
  - VM, Network, DB 등을 하나의 Resource group으로 묶어, **논리적 컨테이너**로 관리한다.

> **When?**

- application 인프라를 완전히 제어할 때 사용한다.
- on-premise application workload를 변경하지 않고 Azure에 migration 할 때 사용한다.

---

### Azure App Service

- **PaaS**
- 웹 기반 프로젝트를 가장 빠른 경로로 게시할 때 이용한다.
- 인프라를 관리할 필요 없이 선택한 프로그래밍 언어로 웹 응용프로그램을 빌드하고 호스팅 할 수 있다.
- 웹 응용 프로그램, REST API, 모바일 앱 백엔드를 호스팅 하는 서비스
- .NET, .NET Core, Java, Ruby, Node.js, PHP, Python 등의 다양한 언어 이용 가능
- **보안**, **부하 분산**(AWS의 Load Balancing), **자동 크기 조정**(AWS의 Auto Scaling)등의 Azure의 기능을 응용 프로그램에 추가할 수 있다.
- DevOps를 염두에 두고 설계되었다.
  - GitHub, Jenkins, Azure DevOps 등 게시 및 연속적인 통합 배포(CD/CI)를 위한 다양한 도구를 지원한다.
- 참고 자료 : [<span style="color:skyblue"><b>https://learn.microsoft.com/ko-kr/azure/app-service/</b></span>](https://learn.microsoft.com/ko-kr/azure/app-service/)

> **When?**

- 기존 웹 애플리케이션을 Azure로 migration 할 때 사용한다.
- 앱에 대해 완전히 관리되는 호스팅 플랫폼이 필요할 때 사용한다.
- 앱에서 모바일 클라이언트를 지원할 때 사용한다.

---

### Azure Service Fabric

- **PaaS**
- **마이크로 서비스**를 관리하는 분산된 시스템 플랫폼
- 배포된 응용 프로그램의 프로비전, 배포, 모니터링, 업그레이드/패치 및 삭제 등의 관리 기능을 제공한다.

> **When?**

- 응용 프로그램을 개발할 때 사용한다.
- **마이크로 서비스 아키텍처(MSA)**를 사용하도록 기존 애플리케이션을 다시 작성할 때 사용한다.

---

### Azure Functions

- 코드를 실행하기 위해 전체 프로그램 또는 인프라를 빌드, 관리하지 않아도 된다.
- **이벤트 또는 일정**에 대한 응답으로 실행할 때 코드 실행 환경이 만들어진다.
- **서버를 사용하지 않는** 스타일을 제공한다. -> 필요한 코드만 작성
- HTTP 요청, Webhook, 클라우드 서비스 event 또는 일정에 따라 코드 실행이 트리거 된다.
- C#, F#, Node.js, Python, PHP 등의 다양한 언어 이용 가능

> **When?**

- 웹 기반 이벤트 또는 일정에 따라 트리거 되는 코드가 있을 때 사용한다.
- 완전히 호스트된 프로젝트의 오버헤드가 필요하지 않을 때 사용한다.

<br>

## 인증

앱 클라이언트 인증을 위한 여러 가지 방법을 제공한다.

- **Azure AD (Active Directory)** : MS 다중 테넌트, 클라우드 기반 ID 및 액세스 관리 서비스 -> SSO (Single Sign-On) 추가
- **App Service 인증** : Azure AD, social ID 공급자 모두를 사용하여 인증할 때 사용한다.

<br>

## 모니터링 

- **Visual Studio Application Insights** : 웹 응용 프로그램 모니터링
- **Azure Monitor** : Azure 인프라, 리소스 모니터링

<br>

<br>

# Azure 지역

- **전 세계 여러 데이터 센터에 application을 배포**할 수 있다.
- 최대의 가용성을 제공하기 위해 **다중 지역 앱**을 지원한다.
  - 둘 이상의 데이터 센터에 application을 호스팅 가능
  - Azure Traffic Manager : 다중 지역 지원

<br>

<br>

# 응용 프로그램 및 프로젝트 관리 방법

- **Azure Portal** : portal.azure.com
- **Azure CLI**
- **Azure PowerShell**
- **REST API** : Azure 리소스와 응용 프로그램을 프로그래밍 방식으로 프로비저닝, 관리
- **API** : Azure SDK를 이용해 응용 프로그램에서 리소스를 프로그래밍 방식으로 관리

## Azure Portal

- 웹 기반 통합 콘솔
- 간단한 웹 앱, 복잡한 클라우드 배포 등 모든 것을 구축, 관리, 모니터링 할 수 있다.
- 사용자 지정 대시보드로 리소스를 관리한다.
- 필요한 옵션을 구성하여 최적의 환경을 구축할 수 있다.

<img width="810" alt="스크린샷 2022-12-02 오후 9 21 16" src="https://user-images.githubusercontent.com/93996283/205291919-42611d9a-117a-465b-93eb-877b3fe1d7f3.png">

<br>

<br>

# Azure Marketplace

Azure에서 실행되도록 최적화된 솔루션과 서비스의 검색, 체험, 구매, 프로비전을 제공한다.

![image](https://user-images.githubusercontent.com/93996283/205292285-3f43bd73-e8b1-4d2f-894a-5f36e2c76205.png)

<br>

Azure에 대한 더 많은 내용은 아래 사이트에서 학습할 수 있다.

 [<span style="color:skyblue"><b>https://learn.microsoft.com/ko-kr/training/azure/</b></span>](https://learn.microsoft.com/ko-kr/training/azure/)


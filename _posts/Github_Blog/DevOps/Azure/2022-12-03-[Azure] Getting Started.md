---
title: "[Azure] Getting Started"
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

# Azure의 리소스에 대한 계층 구조

> *Management groups - Subscriptions - Resource groups - Resources*

<img width="584" alt="스크린샷 2022-12-03 오후 4 53 43" src="https://user-images.githubusercontent.com/93996283/205430892-195f3e13-c0cc-4069-b58a-aadffb835d63.png">

- **Resource**
  - 가상 머신, 스토리지, SQL database, ... => **사용자가 만든 서비스 instance**
- **Resource group**
  - resource가 배포, 관리되는 **논리적 컨테이너**
- **Subscription**
  - 만들고 사용 가능한 리소스 양에 대한 제한/할당량 => 팀/프로젝트별 비용 관리
- **Management group**
  - 여러 구독에 대한 액세스, 정책 등을 관리

<br>

---

<br>

## Subscription

- Azure 제품/서비스에 대한 인증되고 권한이 부여된 액세스를 제공
- 리소스 프로비저닝
- Azure AD(Active Directory)에 있는 ID인 Azure 계정과 연결된 Azure 서비스의 논리적 단위

![image](https://user-images.githubusercontent.com/93996283/205431071-0951d300-5e76-4d99-b137-3e779f77756e.png)

<br>

---

<br>

## Resource group

- **리소스를 보관하는 컨테이너** - 리소스를 간편하게 구성하고 관리할 수 있다.
- Azure 플랫폼의 기본 요소
- 모든 resource 리소스 그룹에 있어야 한다.
- 하나의 resource는 하나의 resource gruop의 멤버여야 하기 때문에 **논리적 그룹화**가 중요하다.

![image](https://user-images.githubusercontent.com/93996283/205431226-de9b429a-d1b5-4107-8dc4-d40bff79307d.png)

- **수명 주기** : resource group을 삭제하면 모든 resource가 삭제된다.

- **Azure Resource Manager**
  - 배포 및 관리 서비스
  - 리소스 생성, 업데이트, 삭제 등의 관리 기능
  - 액세스 제어, 잠금, 태그 등의 관리 기능

![image](https://user-images.githubusercontent.com/93996283/205431299-86c510d8-8b52-4112-a410-c92f00461adc.png)

<br>

---

<br>

# Region / AZ

- 중복된 하드웨어 환경 구축이 가능 -> 높은 가용성
- **AZ (Availability Zone; 가용성 영역)**
  - Azure Region(지역) 내에서 물리적으로 분리된 데이터 센터
  - 독립된 전원, 냉각 및 네트워크를 갖춘 하나 이상의 데이터 센터
  - 고속 프라이빗 광 네트워크를 통해 연결된다.

<img width="590" alt="스크린샷 2022-12-03 오후 5 14 21" src="https://user-images.githubusercontent.com/93996283/205431489-b6d7956c-3464-4972-a762-da3475e1d2a7.png">

**2020년 6월 기준 Region의 모습**

![image](https://user-images.githubusercontent.com/93996283/205431448-22208dce-f480-413c-9901-bbf5cc42f627.png)

<br>

## Region Pair

각 지역은 300 mile 이상 떨어져 있는 동일한 지리적 위치 내의 다른 Azure 지역과 항상 쌍을 이룬다.

- 예) 미국 동부 - 미국 서부, 동남 아시아 - 동아시아

일부 서비스는 자동 지역 중복 스토리지를 제공한다.

![image](https://user-images.githubusercontent.com/93996283/205431556-c90b8f12-6c9b-46a0-affc-148430570df8.png)


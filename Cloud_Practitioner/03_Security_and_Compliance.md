```
도메인 2: 보안 (25%)
  2.1 AWS 책임 분담 모델 정의
  2.2 AWS 클라우드의 보안 및 규정 준수 개념 정의
  2.3 AWS 액세스 관리 기능 확인
  2.4 보안 지원 리소스 파악
```

# 공동 책임 모델 (Shared Responsibility Model)

- AWS 책임 '클라우드의 보안' - AWS가 호스트 운영 체제 및 가상화 계층에서 서비스가 운영되는 시설의 물리적 보안에 이르기까지 구성 요소를 운영, 관리 및 제어
- 고객 책임 '클라우드에서의 보안' – 고객은 게스트 운영 체제(업데이트 및 보안 패치 포함) 및 다른 관련 애플리케이션 소프트웨어를 관리하고 AWS에서 제공한 보안 그룹 방화벽을 구성할 책임이 있음

  ![domain](./images/03_Shared_Responsibility_Model.jpg)

> AWS는 Guest OS 레이어 윗부분에 대한 가시성은 제로이다. 절대로 볼수 없다.

## IT 제어에서의 고객/AWS 공동 책임 모델

- 상속된 제어 항목 – 고객이 AWS로부터 전적으로 상속받는 제어 항목 (AWS 젱어)
  - 물리적 및 환경 제어 항목

- 공유된 제어 항목 – 공유된 제어에서는 AWS는 인프라에 대한 요구 사항을 제공하고 고객은 자사의 AWS 서비스 사용 내에서 자체적인 제어 구현을 제공해야 한다.
  - 패치 관리 – AWS는 인프라와 관련된 결함 수정과 패치에 대한 책임이 있으며, 고객은 게스트 OS와 애플리케이션 패치에 대한 책임이 있다.
  - 구성 관리 – AWS는 인프라 디바이스의 구성을 유지 관리하고, 고객은 자체 게스트 운영 체제, 데이터베이스 및 애플리케이션의 구성에 대한 책임이 있다.
  - 인지 및 교육 – AWS는 AWS 직원을 교육하고, 고객은 자사의 직원을 교육해야 한다.

- 고객 특정 – 전적으로 고객의 책임인 제어 항
  - 고객이 특정 보안 환경 내에서 데이터를 라우팅하거나 영역을 지정해야 할 수 있는 서비스 및 통신 보호 또는 영역 보안.

# AWS Security 소개

AWS는 데이터센터와 네트워크에 어떤 고객의 요구사항도 충족시킬 수 있는 보안을 적용하고 있음

## 데이터 보호
- 암호화 기능
- 키 관리 옵션 - AWS key Management Service
- 하드웨어 기반 암호화 키 스토리지 옵션 - AWS CloudHSM
## 자격 증명 및 액세스 관리
- Identity and Access Management (IAM)
- Multi-Factor Authentication (MFA)
- 기업 디렉토리와의 통합 및 연동
- Amazon Cognito
- AWS SSO
## 네트워크 보안을 위해 제공하는 기능
- 기본 제공 방화벽
- 전송 중 암호화
- 비공개/전용 연결
- DDos(Distributed Denial of Service) 완화
## 위협 탐지 및 지속적인 모니터링
- 위험 요소를 줄이기 위한 도구 및 기능
  - API 호출에 대한 심층적인 가시성
  - 로그 집계 및 옵션
  - 알림 제공
-  AWS Market Place 에 보안을 위한 다양한 솔루션이 있음
## 인프라 보호
  AWS는 고객이 생성한 규칙에 따라 트래픽을 필터링하여 웹 애플리케이션을 보호합니다.
  예를 들어 IP 주소, HTTP 헤더, HTTP 본문 또는 URI 문자열을 기준으로 웹 요청을 필터링하면
  SQL 명령어 주입이나 교차 사이트 스크립팅 같은 일반적인 공격 패턴을 차단할 수 있습니다.
## 규정 준수 및 데이터 프라이버시
  AWS에서는 포괄적인 규정 준수 상태를 확인하고 AWS 모범 사례와 조직에서 준수하는 업계 표준을 기반으로
  자동 규정 준수 검사를 사용하여 환경을 지속적으로 모니터링할 수 있습니다.

---

## Identity and Access Management (IAM)
- Policy Docs, Group, Role, User으로 구성
- User : 영구 명명된 운영자(사람, 머신 등..) 영구적인(Permanent) 자격 증명 세트 (id/pw, 엑세스/보안키.. 등)
- Group : User의 모음
- Role : 역할은 권한(Permision)이 아니다. 인증 방법이다. Role에 있는 자격증명은 일시적이다.(temporary) -> Authencication 이다.
- Policy Docs : 권한은 정책문서에서 발생한다. -> Authorization
- 모든 API 동작은 CloudTrail에 기록된다.

## Amazon Inspector
- 보안평가를 수행하는 자동화된 도구
- AWS에서 배포된 애플리케이션에 대하여 취약성, 모범사례와의 차이를 평가하고 평가후 문제 해결을 위한 우선순위 단계가 포함 된 세부 보고서를 작성
- AWS에서는 제공되는 권장사항으로 모든 잠재적 보안 문제가 해결된다고 보장하지 않는다. 보안에 대한 책임은 고객한테 있다. (도구는 제공하지만 최종 책임은 안진다)
- 일반 보안 규정 준수 표준 및 취약성 정의에 대하여 제공하고 있으며, AWS 보안 연구원이 정기적으로 업데이트 하고 있음

## AWS Shield
- AWS에서 실행되는 애플리케이션을 보호하는 관리형 DDoS(Distributed Denial of Service) 보호 서비스

### AWS Shield Standard
추가 비용 없이 모든 AWS 고객이 사용할 수 있는 자동 보호

- 모든 AWS 리소스, 모든 AWS 리전을 자동보호 한다.
- 신속한 탐지 - 상시 네트워크 흐름 모니터링 제공
- 인라인 공격 완화 (기본 제공되는 자동화된 완화 기법, 지연 시간으로 인한 영향 방지)
- 셀프 서비스 옵션 제공 (AWS Support를 사용할 필요 없음)

### AWS Shield Advanced
더 높은 수준의 보호, 기능 및 이점을 위한 유료 서비스, DDoS 대응팀에 24/7 액세스 가능

- 전문적 지원 (DDoS Response Team(DRT)에 24/7 액세스 가능)
- 고급 공격 완화
- 가시성 및 공격 알림
- 상시 모니터링 (Amazon Route 53, Amazon CloudFront, Elastic Load Balancer, 탄력적 IP 에 대한 모니터링)
- 향상된 탐지
- DDoS 비용 보호 (DDoS 공격으로 애플리케이션 사용이 급증한 경우 비용에 대한 서비스 크레딧 제공)

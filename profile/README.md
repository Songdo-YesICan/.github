# Yes I Can - CGV 챗봇 예매
<p align="center">
  <img src="images/Group 33.jpg" width="300">
</p>

## 프로젝트 소개
### 계기
---
아르바이트를 하며 직접 목격한 어르신 분들의 불편함을 해결하고자 챗봇을 이용한 채팅, 음성 예매 서비스를 구현하였습니다.

인식한 문제점
---
**1. 보안 문제**
   * 웹 애플리케이션을 보호하기 위해 WAF 활용
   * IAM 사용자의 Access Key를 순환시키기 위해 Secret Manager 활용
   * 데이터 암호화를 위한 키를 생성 및 관리하기 위해 KMS 활용
   * 사용자를 세분화하고 최소 권한을 부여하기 위해 IAM 활용
     
**2. 비용 문제**
   * Cluster Node의 인스턴스 유형을 최적화하기 위해 t3.medium으로 설정
   * EC2 스팟 인스턴스를 활용해 Jenkins CI를 구축하여 온디맨드 인스턴스 대비 최대 90% 비용 절약

**3. 가용성 문제**
   * 트래픽을 분산시키기 위해 ALB 활용
   * Kubernetes 환경에서의 고가용성을 위해 HPA, Karpenter 활용
   * Database의 고가용성을 위해 Aurora Cluster, Read Replica 활용


## 사용법 및 시나리오
### [예매]
### 채팅을 통한 예매
1.
2.

### 음성을 통한 예매
1.
2.

## 전체 아키텍처
![전체 아키텍처](images/architecture.svg)


아키텍처는 크게 **Production 환경**, **Dev 환경**, 그리고 재난 방지를 위한 **DR** 3종류로 구성되어 있습니다.

![아키텍처 구분](images/segmentations.svg)

### Production 환경
![production 환경](images/production.svg)

사용자가 시스템에 접근하여 서비스를 이용하게 되는 환경입니다. 때문에 아래의 3가지를 중점적으로 신경 썼습니다.

1. 가용성
   - Kubernetes
front, backend 서버를 구성하는 쿠버네티스 환경에서는 **ReplicaSet, HPA, Karpenter** 3가지 리소스로 고가용성을 확보하였습니다. 또한 Karpenter를 사용하여 일반 쿠버네티스 CA보다 약 2배 빠른 Scaling 속도 확보하였습니다.

<img src="https://github.com/user-attachments/assets/1d96660c-12d6-470f-9282-704024165055" width="250" height="400"/>

  - Database
**Aurora Cluster**를 사용하여 장애 발생 시 Read Replica의 빠른 failover를 확보하였습니다.
**Read Replica**로 읽기, 쓰기 작업을 분리하여 부하를 분산시켰습니다.
<img src="https://github.com/user-attachments/assets/1cd0d391-6a5e-43fc-9344-c94ccc54f860" width="400" height="400"/>


3. Monitoring

4. ETL Pipeline

## 기술 스택

## 팀 소개

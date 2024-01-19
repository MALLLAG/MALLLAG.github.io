---
layout: Post
title: 💁🏻 About Me
permalink: /about/
content-type: eg
---

**안녕하십니까. 3년차 백엔드 개발자 김성현입니다.**

- 저는 **조직의 구성원과 함께 성장**하려 합니다.
- 저는 **쌓여있는 기술부채를 해결**하려 합니다.
- 저는 **역할보다는 문제 해결에 집중**합니다.
- 저는 **테스트 코드에 대한 고민을 지속**합니다.

# 💻 Work Experience & Projects

### 📈 **가상자산 거래 기능 리빌딩**

- **확장성 강화**
    - scale-out 불가능하던 기존 구조의 한계 극복을 위해 activeMQ → kafka 전환
    - 거래 종목을 partition key로 활용하여 scale-out 시 주문 순서 보장, 동시성 문제 해결
    - 거래, 호가창 서버를 stand-alone에서 scale-out하여 가용성 향상 및 무중단 배포 가능
- **안정성 강화**
    - Choreography Saga 도입으로 예외/장애 시 보상 트랜잭션 발행
    - 리빌딩 후 장애 및 운영 이슈 인입을 0회로 유지 *(월 평균 운영 이슈 인입 횟수 1~2회 → 0회)*
- **아키텍처 전환**
    - kafka 실시간 데이터 처리 및 이벤트 기반 아키텍처 적용
    - SOA에서 MSA로의 구조 전환
    - 거래, 호가 DB 분리로 독립적인 배포 및 운영 가능성 확보
- **주가 차트 데이터 저장소 최적화**
    - mariaDB, influxDB, documentDB 성능 테스트 진행
    - 읽기 성능 테스트 결과: influxDB *(23ms)* > mariaDB *(56ms)* > documentDB *(120ms)*
    - mariaDB 선택 *(고려: influxDB는 aws 완전 관리 서비스 미지원)*
- **유지보수 용이성 강화**
    - 테스트 코드 미비로 인한 리팩토링 및 기능 개선 어려움 개선 *(test-coverage 0% → 70%)*

### 🧾 **자금 세탁 방지 고도화**

- **고객 알기 제도(KYC) 테이블 개선**
    - 레거시 KYC 테이블 정규화 및 migration으로 기능 확장에 유연한 구조로 개선
- **월별 고객 데이터 배치 프로세스 성능 개선**
    - DB connection 최적화로 약 5000명의 고객 데이터 처리 시간 단축 *(40m → 30s)*
- **아키텍처 전환**
    - 자금 세탁 방지 서비스 monolithic → SOA로의 구조 전환
- **자금 흐름 추적(KYT) 기능 추가**

### 🎥 비디오 템플릿 거래 플랫폼 개발

- **초기 서비스 기획, 설계 참여**
- **회원, 상품, 결제 등의 코어 기능 개발**
- **회원, 매출 관리를 위한 백오피스 서비스 개발**

---

# 🚴‍♂️ Career

### 플랫타이엑스 *(2022.06 ~ 2023.12)*

***가상자산 거래소***

매수매도, 입출금, 자금 세탁 방지 등의 기능을 개발 및 리빌딩하였습니다.

### 세이어바웃 *(2021.10 ~ 2022.06)*

***비디오 템플릿 거래 플랫폼***

이커머스 서비스인 비디오 템플릿 거래 플랫폼을, 초기부터 설계, 개발 및 운영하였습니다.

# ⛏️ Skills

- Kotlin, Java
- Spring
- JPA, Querydsl
- MySQL, MariaDB, Redis
- Kafka, ActiveMQ

---

# ✍🏻 Other Experience

### [kotlin study](https://github.com/flataex/java-to-kotlin-study)

- 사내 코틀린 도입을 위한 백엔드 개발팀 스터디 주최 및 운영
    - 신규 프로젝트는 kotlin 기반으로 개발하는 문화 정착

### [kafka study](https://github.com/flataex/kafka-study)

- 사내 kafka 도입을 위한 SRE, 백엔드 개발팀 스터디 주최 및 운영
    - 가상자산 거래 기능 리빌딩 프로젝트와 함께 kafka 도입 완료

---

# Contact

📞  010-5364-4072

📩  beyool95@naver.com

🌐  https://github.com/MALLLAG

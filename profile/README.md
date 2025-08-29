# Azena Messaging Ecosystem – MQTT Service

**개요**

본 프로젝트는 **Azena 플랫폼 기반 메시징 생태계**를 구축하기 위해 개발된 프레임워크입니다.
내부 메시징 모듈(Publisher, Subscriber, Broker)과 Gateway를 통해, **내부 브로커와 외부 MQTT Broker(Mosquitto)** 간의 메시지 발행/구독을 지원합니다.

---

### 내부 ↔ 내부 통신
<p align="center">
  <img src="https://github.com/user-attachments/assets/5fda5904-9d37-4324-8dae-87ddd36bc08a" width="40%" />
</p>

## 시스템 아키텍처

* **내부 Publisher/Subscriber** : 내부 브로커를 통한 메시지 발행·수신
* **내부 Broker** : 내부 메시징 허브, 구독/발행 관리
* **Gateway** : 내부 Broker ↔ 외부 MQTT Broker 중계 (uplink/downlink 토픽 패턴 기반)
* **외부 MQTT Broker (Mosquitto)** : 외부 Pub/Sub 클라이언트와 통신

---

## 실행 환경 준비

### 1. 개발 환경

* **Android Studio Koala (2024.1.1 Patch 1)**
* Android 버전 **12 이하 (SDK/API Level ≤ 32)**

  * 참고: [Android API Levels](https://apilevels.com/)
* **라즈베리파이 (안드로이드 OS)** + 공유기 연결

### 2. 보조 도구

* **scrcpy** (안드로이드 미러링 도구, 필요 시 설치)

  * 참고: [설치 가이드](https://goharry.tistory.com/39)

### 3. 외부 MQTT Broker

* **Mosquitto** 실행 파일(`mosquitto.exe`) 또는 패키지 설치
* 세부 설치 방법은 \[외부 MQTT 브로커 설치 가이드 문서] 참조

---

## MQTT 서비스 실행 가이드

### 1. 네트워크 연결 확인

* 공유기 연결 확인
* 디바이스 연결:

```bash
adb connect 192.168.0.8
```

### 2. 미러링 실행

```bash
scrcpy -s 192.168.0.8:5555
```

---

### 3. 내부 Broker 실행

Broker 모듈 실행 → 브로커 화면 출력 확인

---

### 4. Subscriber / Publisher 실행

각 모듈 실행 후 메시지 발행/구독 테스트 가능

#### 분할 화면 설정 (Android)

* 탭 바에서 네모 버튼 클릭
* 하단 `분할 화면` 선택 → Sub / Pub 화면 동시 실행

---

### 5. 외부 MQTT Broker 실행

```bash
mosquitto -v
```

로그 출력으로 브로커 실행 상태 확인 가능

---

### 6. Gateway 실행 및 설정

게이트웨이는 내부 ↔ 외부 브로커 간 메시지 라우팅을 수행합니다.

**설정 항목**

* **외부 브로커 URL** : 연결할 MQTT Broker 주소
* **Uplink 토픽 패턴** : 내부 → 외부 메시지 발행 허용 규칙
* **Downlink 토픽 패턴** : 외부 → 내부 메시지 수신 허용 규칙

> 설정 변경 후 반드시 **저장 및 시작 버튼**을 눌러야 Gateway 서비스가 정상 동작합니다.

---

## MQTT 실행 상세 가이드

### 구독하기 (Subscribe)

1. 토픽 입력 후 `구독하기` 버튼 클릭
2. "구독 완료" 메시지 확인

### 구독 해제 (Unsubscribe)

1. 구독 해제 버튼 클릭
2. "구독 해제 완료" 메시지 확인

---

### 내부 메시지 발행/수신

1. 토픽 및 메시지 입력 후 `Publish` 버튼 클릭
2. 메시지 발행 및 수신 확인

**동작 규칙**

* 구독 이전에 발행된 메시지는 수신되지 않음
* 구독하지 않은(또는 해제된) 토픽의 메시지는 수신되지 않음
* 동일 토픽 중복 구독 시 메시지는 1회만 수신됨
* 발행 시점 이전부터 구독 중인 토픽은 자동으로 수신됨

---

### 외부 메시지 발행 (Uplink)

1. 외부 MQTT Broker 실행
2. Gateway 실행 후 **Uplink 토픽 규칙**에 맞춰 Publisher 토픽 설정
3. 메시지 발행 → 외부 MQTT Broker Subscriber에서 수신

**주의사항**

* 토픽이 Uplink 규칙과 다르면 메시지 발행되지 않음
* Gateway의 Uplink/Downlink 패턴은 자유롭게 변경 가능 (단, 동일하면 안 됨)
* 외부 MQTT Broker 로그 → 발행된 토픽과 payload 크기 확인 가능

---

### 외부 메시지 수신 (Downlink)

1. Gateway에서 **Downlink 토픽 규칙**에 맞게 Subscriber 토픽 설정
2. 외부 MQTT Publisher에서 메시지 발행
3. 내부 Subscriber에서 메시지 수신 확인

**주의사항**

* 토픽이 Downlink 규칙과 다르면 메시지가 내부로 전달되지 않음
* 내부 Subscriber는 외부 MQTT 발행 메시지의 **토픽 및 payload 내용** 확인 가능

---

## 개발 현황

* [x] 내부 **Broker** 모듈
* [x] 내부 **Publisher/Subscriber** 모듈
* [x] **Gateway** 모듈
* [x] Mosquitto 기반 **외부 MQTT 연동** 검증 완료

---

**개발 및 유지 관리 기관** : 한국전자기술연구원(KETI)

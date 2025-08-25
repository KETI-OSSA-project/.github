# Azena Messaging Ecosystem

**개요**
본 프로젝트는 **Azena 플랫폼 기반 메시징 생태계**를 구축하기 위해 개발된 프레임워크입니다.
내부 메시징 모듈(Publisher, Subscriber, Broker)과 Gateway를 완성하여, 내부 생태계와 외부 MQTT Broker(Mosquitto) 간의 메시지 라우팅 및 연동을 지원합니다.

---

## Azena Messaging System

* **내부 Publisher/Subscriber** : 내부 브로커를 통해 메시지를 발행·수신
* **내부 Broker** : 내부 생태계의 중심 허브, 구독/발행 관리 및 메시지 라우팅
* **Gateway** : 내부 Broker ↔ 외부 MQTT Broker 간 메시지 변환 및 중계
* **MQTT Broker (Mosquitto)** : 외부 Pub/Sub 클라이언트와 통신

---

## 기술 스택

* **언어** : Java (내부 Publisher/Subscriber/Broker, Gateway)
* **프로토콜** : MQTT (Mosquitto 기반)
* **플랫폼** : Azena Ecosystem
* **환경** : Android/Linux 기반 내부 브로커 + 외부 MQTT 연동

---

## 디렉토리 구조

```
Azena-Messaging/
├─ broker_java/        # 내부 Broker (메시지 라우팅 및 구독/발행 관리)
├─ publisher_java/     # Publisher (메시지 발행 클라이언트)
├─ subscriber_java/    # Subscriber (메시지 구독 클라이언트)
├─ gateway/            # Gateway (내부 Broker ↔ 외부 MQTT Broker 중계)
└─ README.md
```

---

## 설치 및 실행 가이드

### \[1] 필수 환경

* **Java 11+**
* **Gradle** (wrapper 포함)
* **Mosquitto (MQTT Broker)**
* Linux/Android 환경 권장

---

### \[2] 레포지토리 클론

```bash
git clone <repository_url>
cd Azena-Messaging
```

---

### \[3] 내부 메시징 모듈 빌드 및 실행

#### Broker 실행

```bash
cd broker_java
./gradlew build
./gradlew run
```

#### Publisher 실행

```bash
cd publisher_java
./gradlew build
./gradlew run
```

#### Subscriber 실행

```bash
cd subscriber_java
./gradlew build
./gradlew run
```

---

### \[4] Mosquitto 설치 및 실행

#### Ubuntu 설치

```bash
sudo apt update
sudo apt install mosquitto mosquitto-clients
sudo systemctl enable mosquitto
sudo systemctl start mosquitto
```

#### 실행 확인

```bash
mosquitto_sub -t "test/topic" -v
mosquitto_pub -t "test/topic" -m "Hello MQTT"
```

---

### \[5] Gateway 설정 및 실행

Gateway는 내부 Broker와 외부 MQTT Broker를 중계합니다.
환경 설정 파일(`gateway/config.json`)에서 브로커 주소를 지정하세요.

예시:

```json
{
  "internalBroker": "tcp://localhost:1883",
  "externalBroker": "tcp://mqtt.eclipse.org:1883"
}
```

실행:

```bash
cd gateway
./gradlew build
./gradlew run
```

---

### \[6] 전체 실행 흐름 예시

1. 내부 Publisher → 내부 Broker로 메시지 발행

   ```bash
   메시지 발행: {"topic": "azena/test", "payload": "Hello Azena!"}
   ```
2. 내부 Subscriber → 메시지 수신
3. Gateway → 내부 Broker 메시지를 MQTT Broker로 전달
4. 외부 MQTT Subscriber → Mosquitto를 통해 메시지 수신

---

## 개발 현황

* [x] **Broker** 모듈 (메시지 라우팅 및 구독/발행 관리)
* [x] **Publisher / Subscriber** 모듈
* [x] **Gateway** 모듈
* [x] Mosquitto 기반 **외부 MQTT Broker 연동** 검증 완료

---

## 향후 계획

* QoS 및 Payload 옵션 확장
* TLS/인증 기반 보안 기능 강화
* 대규모 트래픽 환경에서의 성능 최적화
* Azena 플랫폼 SDK와의 API 통합

---

**개발 및 유지 관리 기관** : 한국전자기술연구원(KETI)

# KETI(한국전자기술연구원) 정보미디어연구센터

# Azena Messaging Ecosystem

## 📌 프로젝트 개요

본 프로젝트는 **자체 Azena 생태계**를 기반으로 메시징 인프라(Publisher, Subscriber, Broker, Gateway)를 완성하여,
내부 브로커와 외부 MQTT 브로커 간 메시지 중계 시스템을 제공하는 것을 목표로 합니다.

아래 그림은 전체 메시지 흐름을 나타낸 구조입니다.

![서비스 흐름도](./그림6.png)

---

## 🎯 프로젝트 목표

* **내부 메시징 시스템 구축**

  * 내부 Publisher/Subscriber와 Broker 간의 안정적인 메시징 처리
* **게이트웨이 연동**

  * 내부 메시지를 MQTT Broker(Mosquitto)와 연결하는 메시지 중계 역할 수행
* **외부 MQTT 통신 지원**

  * Uplink/Downlink 메시지 라우팅
  * 외부 MQTT Pub/Sub과의 통신 지원
* **표준화된 API 제공**

  * Messaging API 기반의 직관적이고 확장성 있는 인터페이스

---

## 📁 디렉토리 구조

```
root/
├── broker_java/        ← 내부 Broker (메시지 라우팅 및 구독/발행 관리)
├── publisher_java/     ← Publisher (메시지 발행 클라이언트)
├── subscriber_java/    ← Subscriber (메시지 구독 클라이언트)
├── gateway/            ← Gateway (내부 Broker ↔ 외부 MQTT Broker 중계)
└── README.md
```

---

## ⚙️ 서비스 구성 요소

1. **내부 Publisher / Subscriber**

   * 내부 브로커를 통해 메시지 발행 및 수신
   * 구독/해제 관리 지원

2. **내부 Broker**

   * 내부 메시징 허브 역할 수행
   * Publisher/Subscriber 간 메시지 라우팅

3. **Gateway**

   * 내부 Broker와 외부 MQTT Broker 간 메시지 변환 및 중계
   * uplink/downlink 처리

4. **MQTT Broker**

   * Mosquitto 기반 외부 브로커
   * 외부 Pub/Sub 클라이언트와 연동

---

## 🚀 개발 현황

* [x] 내부 **Broker** 모듈 완성
* [x] 내부 **Publisher / Subscriber** 모듈 완성
* [x] **Gateway** 모듈 완성
* [x] 외부 MQTT Broker(Mosquitto)와 연동 검증 완료

---

## 🔮 향후 계획

* QoS 및 payload 옵션 확장
* 보안 기능(TLS, 인증) 추가
* 대규모 트래픽 시뮬레이션 및 성능 최적화
* Azena 플랫폼 기반 **서비스 레벨 API 패키징**




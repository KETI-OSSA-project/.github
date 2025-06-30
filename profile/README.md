# KETI(한국전자기술연구원) 정보미디어연구센터


## Message API - Java 리팩토링 프로젝트

본 프로젝트는 기존 MQTT 기반의 Kotlin 구현 코드를 Java로 리팩토링하고,  
공식 API 명세를 기반으로 표준화된 메시지 API 시스템을 구축하기 위한 작업입니다.

---

## 🔧 프로젝트 목적

- 기존의 Kotlin 기반 MQTT 앱(브로커, 퍼블리셔, 서브스크라이버)을 Java로 단계적으로 이관
- 공식 문서에 정의된 message API와 최대한 호환되는 형태로 코드 리디자인
- 시스템 간 연동 시 **사용성과 직관성을 높이는 API 구조 확보**

---

## 📁 디렉토리 구조

```
root/
├── kotlin_legacy/         ← 기존 MQTT 앱 3종 (Kotlin)
│   ├── broker/
│   ├── publisher/
│   └── subscriber/
│
├── java_refactor/         ← 새롭게 개발할 Java 코드
│   ├── broker/            ← 브로커 중심부터 시작
│   ├── publisher/
│   └── subscriber/
│
├── api_docs/              ← 공식 API pdf 또는 정리 자료
│   └── api_mapping.md
│
├── README.md
└── settings.gradle (optional, if multi-module)
```

---

## ✅ 개발 우선순위

1. **브로커 모듈(Java)** 개발
    - MQTT 메시지 수신, topic 관리, 클라이언트 등록
    - 공식 API 기준에 맞춘 인터페이스 구성

2. **퍼블리셔(Publisher) 모듈(Java)**
    - 메시지 전송 API(`sendMessage()`) 호출
    - QoS, payload, correlation 설정 등 적용

3. **서브스크라이버(Subscriber) 모듈(Java)**
    - 구독 요청, 메시지 수신 API 구성

---

## 🔄 API 매핑 진행 현황

`/api_docs/api_mapping.md`에서 공식 API와 현재 구현의 매핑 상태를 확인할 수 있습니다.

---

## 📌 기타 참고 사항

- 현재는 **필수 API 10개를 선별**하여 우선 구현 중입니다.
- 브로커 기능이 먼저 구현된 후, 퍼블리셔/서브스크라이버 순으로 연동 예정입니다.
- 본 프로젝트는 내부 시스템 연동 및 테스트 목적으로 구성되며, 확장성 있는 구조를 목표로 합니다.

---


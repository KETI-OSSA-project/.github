# Azena Messaging Ecosystem – MQTT Service
<p align="center">
  <img src="https://github.com/user-attachments/assets/d15b5f1f-2052-4b2e-b914-270107ee7431" alt="<프로젝트명> Banner" width="70%" />
</p>

<p align="center">
  <b>Validate and integrate MQTT messaging services and brokers with a unified tool.</b>
</p>

<div align="center">

  <!-- 윗줄: Android 관련 2개 -->
  <img src="https://img.shields.io/badge/Android_Studio-Koala-3DDC84?logo=androidstudio&logoColor=white" />
  <img src="https://img.shields.io/badge/Android-12_(API_32)-3DDC84?logo=android&logoColor=white" />
  <!-- 아랫줄: 나머지 3개 -->
  <img src="https://img.shields.io/badge/Java-11-007396?logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/Mosquitto-2.0.22-3C5280?logo=eclipseide&logoColor=white" />

</div>


## Highlights

- **공식 azena MQTT 표준 문법 기반 서비스 제공**  
  azena 플랫폼에서 정의한 공식 Android MQTT 서비스 문법을 기반으로, 표준화된 방식으로 메시징 기능을 제공합니다.  
  다른 개발자도 동일한 문법으로 손쉽게 브로커·퍼블리셔·서브스크라이버를 연동할 수 있습니다.

- **안드로이드 기반 독립 실행형 메시징 허브**  
  하나의 Android 앱 안에서 브로커, 퍼블리셔, 서브스크라이버를 모두 실행할 수 있는 독립형 허브를 구현했습니다.  
  별도의 외부 장비 없이도 로컬 테스트 및 메시지 라우팅이 가능합니다.

- **내부 ↔ 외부 MQTT 브로커 연동 (Mosquitto 지원)**  
  내부 브로커와 외부 Mosquitto 브로커 간 메시지 교환을 지원하여, 실제 IoT 환경과 동일한 구조로 테스트할 수 있습니다.

- **Gateway를 통한 uplink/downlink 토픽 패턴 관리**  
  Gateway 역할을 통해 업링크/다운링크 토픽을 일관성 있게 관리하고, 확장 가능한 토픽 패턴 설계를 지원합니다.

---

## Demo
### 내부 ↔ 내부 통신
<p align="center">
  <img src="https://github.com/user-attachments/assets/5fda5904-9d37-4324-8dae-87ddd36bc08a" width="40%" />
</p>

### 내부 ↔ 외부 통신
<table>
<tr>
    <td><img src="https://github.com/user-attachments/assets/3372b3b6-22df-4a4c-b832-d55950039a4c" alt="uplink-broker"></td>
    <td><img src="https://github.com/user-attachments/assets/e029e60a-968f-4e0d-9743-4cc5d612e071" alt="downlink-subscriber"></td>
</tr>
</table>
<p align="center">
  <a href="https://drive.google.com/file/d/1_TukQ0CwD708QUjqD8ZCfM2t8XZdoEBp/view?usp=drive_link">
    <b>📽️ MQTT Demo</b>
  </a>
</p>

---

## Getting Started

### Setup
- **Android Studio Koala (2024.1.1 Patch 1)**  
- Android 버전 **12 이하 (SDK/API Level ≤ 32)**  
- 안드로이드 디바이스: **라즈베리파이 (Android OS)** + 공유기 연결  
- 보조 도구: [scrcpy](https://goharry.tistory.com/39) (안드로이드 화면 미러링)

---

### Running
1. **[실행 문서 참고](https://docs.google.com/document/d/1I74fBEl-GEGYGJwbT1mKgXR2QVihajx3eY7xqVxtmNs/edit?tab=t.0)**  

2. **[외부 브로커 실행 (mosquitto)](https://docs.google.com/document/d/1L3uAyofZ-PSXeE4_AYlj9fvegXYk_N6T/edit)**
- publish
   ```bash
  mosquitto_pub -h localhost -p 1883 -t "downlink/app/+/in" -m "Hello from Mosquitto"
   ```

- subscribe
   ```bash
   mosquitto_sub -h localhost -p 1883 -t “uplink/app/+/out”
   ```
---

## Corresponding Author 
**개발 및 유지 관리 기관** : 한국전자기술연구원(KETI)

※ 본 연구는 2025년도 정부(과학기술정보통신부)의 재원으로 정보통신기획평가원의 지원을 받아 수행된 연구임(No. RS-2024-00394190, 온-디바이스 자율보호가 내재화된 개방형 영상보안플랫폼 기술 개발).

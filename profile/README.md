# Azena Messaging Ecosystem – MQTT Service
<p align="center">
  <img src="https://github.com/user-attachments/assets/d15b5f1f-2052-4b2e-b914-270107ee7431" alt="<프로젝트명> Banner" width="70%" />
</p>

<p align="center">
  <b>Validate and integrate MQTT messaging services and brokers with a unified tool.</b>
</p>

<p align="center">
<!-- Android Studio -->
<img src="https://img.shields.io/badge/Android_Studio-Koala_(2024.1.1_Patch_1)-3DDC84?logo=androidstudio&logoColor=white" />

<!-- Android 버전 -->
<img src="https://img.shields.io/badge/Android-12_(API_32)-3DDC84?logo=android&logoColor=white" />

<!-- Raspberry Pi -->
<img src="https://img.shields.io/badge/Raspberry_Pi-Device-A22846?logo=raspberrypi&logoColor=white" />

<br> <!-- 줄바꿈 -->

<!-- Java version -->
<img src="https://img.shields.io/badge/Java-11-007396?logo=openjdk&logoColor=white" />

<!-- MQTT (Eclipse Paho) -->
<img src="https://img.shields.io/badge/MQTT-Eclipse_Paho_v1.2.5-2C2255?logo=eclipseide&logoColor=white" />

</p>

### Highlights
- **내부 ↔ 외부 MQTT 브로커 연동** (Mosquitto 지원)  
- **안드로이드 기반 독립 실행형 메시징 허브** (Broker, Publisher, Subscriber 포함)  
- **Gateway를 통한 uplink/downlink 토픽 패턴 관리**  
- **라즈베리파이 + 안드로이드 환경에서 검증 완료**  
---

## Architecture

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

- **내부 Publisher/Subscriber** : 내부 브로커를 통한 메시지 발행·수신  
- **내부 Broker** : 내부 메시징 허브, 구독/발행 관리  
- **Gateway** : 내부 Broker ↔ 외부 MQTT Broker 중계 (uplink/downlink 토픽 기반)  
- **외부 MQTT Broker (Mosquitto)** : 외부 Pub/Sub 클라이언트와 통신  
---

## Getting Started

### Setup
개발 환경 준비:
- **Android Studio Koala (2024.1.1 Patch 1)**  
- Android 버전 **12 이하 (SDK/API Level ≤ 32)**  
- **라즈베리파이 (Android OS)** + 공유기 연결  
- 보조 도구: [scrcpy](https://goharry.tistory.com/39) (안드로이드 화면 미러링)  

---

1. **내부 Broker 실행**
   
   ```bash
   ./broker_start.sh
   ```

3. **Publisher 실행**

   ```bash
   ./publisher_start.sh --topic test/topic --message "hello world"
   ```

4. **Subscriber 실행**

   ```bash
   ./subscriber_start.sh --topic test/topic
   ```

5. **Gateway 실행 (내부 ↔ 외부 브로커 연동)**

   ```bash
   ./gateway_start.sh --uplink "uplink/#" --downlink "downlink/#"
   ```

---

**개발 및 유지 관리 기관** : 한국전자기술연구원(KETI)

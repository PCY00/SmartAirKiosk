# SmartAirKiosk

## 언어 선택

[English](README.md) | [한국어](README_KR.md)

<br><br>

## 개요

- 요즘 미세먼지로 인하여 마스크의 수요가 점점 늘고있음
- 매장에서 마스크를 끼고 음식 섭취가 어려움
- 그로 인해 알바생 및 직원이 매장을 관리해야함
- 매장이 바쁠 경우 실시간으로 매장 관리가 어려워짐
- 따라서 온도 및 습도를 조절하고 미세먼지를 완화하기 위해
  매장을 쾌적하게 관리하는 무인 키오스크를 개발함

<br><br>

## 고려한 부분

- 요즘 미세먼지의 심각성
- 매장의 쾌적성 실시간 유지
- 매장에 키오스크의 필요성 ( 경제성 -> 요즘은 키오스크는 필수적 따라서 키오스크에 추가 기능 구현함)

<br><br>


## 설치 사진
<div align="center">
  
  | 실제 |
  |:---:|
  | <img src="https://github.com/user-attachments/assets/314c94d4-e6bc-4acf-934e-5a8bf56400b1" width="350px" height="470px" alt="실제"> |
</div>

<br><br>

## SmartAirKiosk 구동 영상

[SmartAirKiosk 구동 영상 보기](https://youtu.be/KF5rC-BnxO0)

<br><br>

## 디렉토리 형식

```
SmartAirKiosk/
├── APP/
│   ├── APP.jpg
│   ├── PMS_Alarm.jpg
│   │
├── GUI/
│   ├── gui.py
│   │
├── Sensor/
│   ├── RaspberryPi_3_PMS.py
│   ├── Temp_relay.cpp
│   ├── 초음파_PIR.cpp
│ 
├── Wiring/
│   ├── Wiring.jpg
│   │
├── modeling/
│   ├── SmartAir.png
│   ├── modeling.step

```

<br><br>

## 사용된 하드웨어 장비

| 장비명                | 사양                                                                                                                                                                                                                                                                                                                                                                     | 수량 | 비고                         |
|:------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---:|:--------------------------:|
| Raspberry Pi 3B+   | Quad-core ARM® Cortex-A53 64-bit SoC @ 1.4GHz                                                                                                                                                                                                                                                                                                                                    | 3  |                            |
| HC-SR501  |                                                                                                                                                                                                                                                                                                                                                              | 1  | 인체 감지 센서       |
| HC-SR04        |                                                                                                                                                                                                                                                                                                                                                              | 1  |          초음파 센서                  |
| PMS7003            | 광산란 방식                                                                                                                                                                                                                                                                                                                                              | 1  | 미세먼지 센서                    |
| D06A0 쿨젠 써큘레이터              |                         5V, 0.5A                                                                     |  1  | 선풍기 |
| Arduino Relay Module            |                                                                                                                                                                                                                                                                                                                                                                     | 1  | 릴레이                     |
| 디스플레이 7인치                 |   5V  |  1  |                 터치용           |


<br><br>

## 시스템 아키텍처

![시스템 아키텍처](https://github.com/user-attachments/assets/4c321007-3b18-4ea9-813b-6ff5827f3be3)

<br><br>

## 배선도

<div align="center">

  | 센서 배선 | 
  |:---:|
  | <img src="https://github.com/user-attachments/assets/54dacca4-ecc6-4a91-9701-8f52dfa73992"  alt="센서 배선도"> |
</div>

<br><br>

## 앱 구현

### MIT Inventer
- Mobius에서 GET
![2](https://github.com/user-attachments/assets/222d7ba7-0c47-4178-98b9-6ba8fb2832dc)

- Mobius에서 POST
![3](https://github.com/user-attachments/assets/257c163b-d529-4cd9-8b1f-c43a9f388afe)




## 기능

### 카드등록 유무 확인 기능 
- RFID리더기에서 UID값을 읽어와 해당 UID값이 Mobius에 등록되어있는지 확인함
- 등록되어 있다면 카드잔액에서 결제금액을 차감함 (만약 돈이 없다면 돈이 없다고 텍스트를 띄워줌)
- UID 자체가 등록이 되어 있지 않다면 invalid card를 출력함 

### 키오스크 사람 인식
- PIR 과 초음파 센서를 같이 사용하여 사람 인식
- PIR의 성능에 오류가 있어 초음파를 사용함
- 사람이 떠나가는 시간까지 고려하여 5초의 딜레이 시간을 줌

### 선풍기 (가상에선 에어컨) 제어
- 주변 온도가 25도 이상이 되면 자동으로 선풍기를 킴
- 만약 온도가 25도 이하로 내려가면 선풍기를 끔

### 미세먼지 관리기능
- 에어코리아 API를 활용하여 외부 미세먼지 농도와 내부 미세먼지 농도를 비교
- 내부 미세먼지 농도가 외부보다 높을 경우만 창문을 열으라고 어플로 알림



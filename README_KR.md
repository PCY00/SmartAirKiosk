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


### 모델링 및 설치 사진
<div align="center">
  
  | 실제 |
  |:---:|
  | <img src="https://github.com/user-attachments/assets/314c94d4-e6bc-4acf-934e-5a8bf56400b1" width="350px" height="470px" alt="실제"> |
</div>

<br><br>

### SmartAirKiosk 구동 영상

[SmartAirKiosk 구동 영상 보기](https://youtu.be/KF5rC-BnxO0)

<br><br>

### 디렉토리 형식

```
APM_v2/
├── Document/
│   ├── Guide_KR
│   └── Guide_EN
│ 
├── src/
│   ├── DAQ/
│   │   └── DAQ.py
│   │
│   ├── Mobius_server_mqtt/
│   │   └── nCube-Thyme-Nodejs.zip
│   │
│   ├── Sensor/
│   │   ├── Environmental_Sensor/
│   │   │   ├── DFRobot_OzoneSensor.cpp
│   │   │   ├── DFRobot_OzoneSensor.h
│   │   │   └── Environmental_Sensor.ino
│   │   ├── Module_Floor_1/
│   │   │   └── Module_Floor_1.ino
│   │   ├── Module_Floor_2/
│   │   │   └── Module_Floor_2.ino
│   │   ├── Module_Floor_3/
│   │   │   └── Module_Floor_3.ino
│   │   ├── NPM
│   │   │   └── NPM.ino

```

<br><br>

### 사용된 하드웨어 장비

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

### 배선도

<div align="center">

  | 센서 배선 | 
  |:---:|
  | <img src="https://github.com/user-attachments/assets/54dacca4-ecc6-4a91-9701-8f52dfa73992"  alt="센서 배선도"> |
</div>

<br>

### 시스템 아키텍처

![시스템 아키텍처](https://github.com/user-attachments/assets/4c321007-3b18-4ea9-813b-6ff5827f3be3)

<br><br>

## Fan 파라미터 조정

<table border="1" align="center">
  <tr>
    <th>Container</th>
    <th>Module</th>
    <th>note</th>
  </tr>
  <tr>
    <td>Container 1</td>
    <td>M1_P1_? <br> M1_P2_? <br> M1_P3_?</td>
    <td rowspan="3">각 컨테이너의 각 모듈의 원하는 Fan 속도를 입력하면 그 Fan 속도로 Fan을 움직임 <br> (?: Fan RPM 값, Mx_Py : x는 각 컨테이너를 가리키고, y는 각 모듈을 가리킴)</td>
  </tr>
  <tr>
    <td>Container 2</td>
    <td>M2_P1_? <br> M2_P2_? <br> M2_P3_?</td>
  </tr>
  <tr>
    <td>Container 3</td>
    <td>M3_P1_? <br> M3_P2_? <br> M3_P3_?</td>
  </tr>
</table>




<br><br>

## Server (OneM2M)

### Mobius 플랫폼
- URL: 필요시 제공해주겠음
- [Mobius 플랫폼 접속 링크](http://114.71.220.59:7575/#!/monitor)

![server](https://github.com/user-attachments/assets/3d25239d-c8fb-4218-8019-f742800bbce3)

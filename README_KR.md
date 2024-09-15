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

### APM_v2 Mqtt(모터) 구동 영상

- 모터는 필요없다고 생각되어 현재 탈거하였음

[APM_v2 Mqtt 구동 영상 보기](https://youtu.be/hN8SpTdIn4Q?feature=shared)

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
| Jetson Nano B 01   | Quad-core ARM® Cortex-A57@ 1.43 GHz                                                                                                                                                                                                                                                                                                                                    | 1  |                            |
| Arduino Mega 2560  | ATmega2560                                                                                                                                                                                                                                                                                                                                                             | 4  | 미세먼지 데이터 3, 환경 데이터 1       |
| Arduino Uno        | ATmega328P                                                                                                                                                                                                                                                                                                                                                             | 1  |                            |
| PMS7003            | 광산란 방식 <br> (fan 유무 : 무)                                                                                                                                                                                                                                                                                                                                               | 9  | 미세먼지 센서                    |
| 환경 센서              | CO, NO2, SO2 each 1 (AllSensing AGSM series)<br> Ozone 1 (sen0321) - I2C communication<br> WindSpeed 1 (sen0170) - Analog communication<br> WindDirection 1 (WS5029) - Analog communication<br> Temperature and Humidity (DHT22) - Digital                                                                                                             |    | UART, I2C, Digital, Analog |
| 구동부 센서             | Fan                                                                                                                                                                                                                                                                                                                                                                    | 9  | 4선 Fan                     |
| 기타                 | 파워서플라이 1개 (방수) <br>전기박스 358 x 270 x 152 1개 <br>전기박스 500 x 400 x 160 1개 <br>프로파일 40 x 40 x 500 6개 <br>프로파일 40 x 40 x 250 16개 <br>프로파일 20 x 80 x 400 8개 <br>프로파일 20 x 40 x 400 11개 <br>프로파일 20 x 40 x 360 8개 <br>프로파일 20 x 20 x 400 8개 <br>프로파일 20 x 20 x 470 10개 <br>SSEBL420 8개 <br>4선 실드 케이블 (약 1.5M) 9개 <br>2선 실드 케이블 (1.5M) 8개 <br>3D 프린터로 나머지 재료 제작 (PLA+ 재질)  |    |                            |


<br><br>

### 배선도

<div align="center">

  | 센서 배선 | 
  |:---:|
  | <img src="https://github.com/user-attachments/assets/c789b326-338c-4222-890a-6d37527918c3" width="600px" height="550px" alt="센서 배선도"> |
</div>

<br>

### 센서 배선도

<div align="center">
  <table>
    <tr>
      <td>
        <table border="1">
          <tr>
            <th><strong>Arduino Mega 2560 (환경센서)</strong></th>
            <th><strong>온습도, CO, NO2, SO2, O₃</strong></th>
          </tr>
          <tr>
            <td>5V</td>
            <td><strong>VCC</strong></td>
          </tr>
          <tr>
            <td>GND</td>
            <td><strong>GND</strong></td>
          </tr>
          <tr>
            <td>D6</td>
            <td><strong>온습도_OUT</strong></td>
          </tr>
          <tr>
            <td>D19</td>
            <td><strong>CO_Tx</strong></td>
          </tr>
          <tr>
            <td>D18</td>
            <td><strong>CO_Rx</strong></td>
          </tr>
          <tr>
            <td>D17</td>
            <td><strong>NO2_Tx</strong></td>
          </tr>
          <tr>
            <td>D16</td>
            <td><strong>NO2_Rx</strong></td>
          </tr>
          <tr>
            <td>D15</td>
            <td><strong>SO2_Tx</strong></td>
          </tr>
          <tr>
            <td>D14</td>
            <td><strong>SO2_Rx</strong></td>
          </tr>
          <tr>
            <td>D20</td>
            <td><strong>O₃_SDA</strong></td>
          </tr>
          <tr>
            <td>D21</td>
            <td><strong>O₃_SCL</strong></td>
          </tr>
          <tr>
            <td> </td>
            <td><strong>WindSpeed</strong></td>
          </tr>
          <tr>
            <td>Power Supply 12V</td>
            <td><strong>VCC</strong></td>
          </tr>
          <tr>
            <td>Power Supply GND <br> Arduino Mega 2560 GND</td>
            <td><strong>GND</strong></td>
          </tr>
          <tr>
            <td>A1</td>
            <td><strong>OUT</strong></td>
          </tr>
          <tr>
            <td> </td>
            <td><strong>WindDirection</strong></td>
          </tr>
          <tr>
            <td>5V</td>
            <td><strong>VCC</strong></td>
          </tr>
          <tr>
            <td>GND</td>
            <td><strong>GND</strong></td>
          </tr>
          <tr>
            <td>A0</td>
            <td><strong>OUT</strong></td>
          </tr>
        </table>
      </td>
      <td>
        <table border="1">
          <tr>
            <th><strong>Arduino Mega 2560 (3개 동일)</strong></th>
            <th><strong>PM1, PM2, PM3</strong></th>
          </tr>
          <tr>
            <td>5V</td>
            <td><strong>VCC</strong></td>
          </tr>
          <tr>
            <td>GND</td>
            <td><strong>GND</strong></td>
          </tr>
          <tr>
            <td>D19</td>
            <td><strong>PM1_Tx</strong></td>
          </tr>
          <tr>
            <td>D17</td>
            <td><strong>PM2_Tx</strong></td>
          </tr>
          <tr>
            <td>D15</td>
            <td><strong>PM3_Tx</strong></td>
          </tr>
          <tr>
            <td>Power Supply 5V</td>
            <td><strong>Fan1, Fan2, Fan3 VCC</strong></td>
          </tr>
          <tr>
            <td>Power Supply GND <br> Arduino Mega 2560 GND</td>
            <td><strong>GND</strong></td>
          </tr>
          <tr>
            <td>D8</td>
            <td><strong>Fan1 PWM</strong></td>
          </tr>
          <tr>
            <td>D9</td>
            <td><strong>Fan2 PWM</strong></td>
          </tr>
          <tr>
            <td>D10</td>
            <td><strong>Fan3 PWM</strong></td>
          </tr>
          <tr>
            <td>D2</td>
            <td><strong>Fan1 Tach</strong></td>
          </tr>
          <tr>
            <td>D3</td>
            <td><strong>Fan2 Tach</strong></td>
          </tr>
          <tr>
            <td>D21</td>
            <td><strong>Fan3 Tach</strong></td>
          </tr>
        </table>
      </td>
    </tr>
  </table>
</div>


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

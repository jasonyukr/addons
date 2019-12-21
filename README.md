# Hass.io Add-on: Korean Wallpad Controller with RS485 

![Supports aarch64 Architecture][aarch64-shield] ![Supports amd64 Architecture][amd64-shield] ![Supports armhf Architecture][armhf-shield] ![Supports armv7 Architecture][armv7-shield] ![Supports i386 Architecture][i386-shield]

## About
랜이님이 만든 월패드 프로그램을 애드온으로 만든 것입니다.

## Installation

1. [github][github]에서 소스코드를 다운받습니다.
2. Samba로 Hassio가 설치된 곳으로 접속하여 addons 폴더 안에 wallpad 라는 폴더를 만들고 소스코드를 업로드합니다.
3. 홈어시스턴트의 Hass.io > ADD-ON STORE 오른쪽 상단의 refresh 버튼을 누릅니다.
4. Local add-ons 에서 "Korean Wallpad Controller with RS485" 클릭합니다.
5. "INSTALL" 버튼을 누르면 애드온이 설치됩니다. 최대 약 10분 정도 소요. 
6. 애드온 페이지에서 Config을 본인의 환경에 맞게 수정합니다.
7. "START" 버튼으로 애드온을 실행합니다.

## Configuration

Add-on configuration:

```json
{
  "RS485": {
    "type": "Serial"
  },
  "Socket": {
    "server": "192.168.x.x",
    "port": "xx"
  },
  "SocketDevice": {
    "device": "kocom"
  },
  "Serial": {
    "port1": "/dev/ttyUSB0"
  },
  "SerialDevice": {
    "port1": "kocom"
  },
  "MQTT": {
    "anonymous": false,
    "server": "192.168.x.x",
    "username": "id",
    "password": "pw"
  },
  "Wallpad": {
    "light": false,
    "plug": false,
    "thermostat": false,
    "fan": false,
    "gas": false,
    "elevator": false
  },
  "Advanced": {
    "INIT_TEMP": 22,
    "SCAN_INTERVAL": 300,
    "SCANNING_INTERVAL": 0.8
  },
  "KOCOM_LIGHT_SIZE": [
    {
      "name": "livingroom",
      "number": 3
    },
    {
      "name": "bedroom",
      "number": 2
    },
    {
      "name": "room",
      "number": 2
    }
    {
      "name": "kitchen",
      "number": 3
    }
  ],
  "KOCOM_PLUG_SIZE": [
    {
      "name": "livingroom",
      "number": 3
    },
    {
      "name": "bedroom",
      "number": 2
    },
    {
      "name": "room",
      "number": 2
    },
    {
      "name": "kitchen",
      "number": 3
    }
  ],
  "KOCOM_ROOM": [
    "livingroom",
    "bedroom",
    "room1",
    "room2",
    "kitchen"
  ],
  "KOCOM_ROOM_THERMOSTAT": [
    "livingroom",
    "bedroom",
    "room1",
    "room2"
  ]
}
```

### Option: `RS485` (required)

type = Serial                    // Serial 혹은 Socket

### Option: `Socket` (required)

server = 192.168.x.x           // Socket 쓸 경우 socket IP주소
port = xx                        // Socket 쓸 경우 socket PORT

### Option: `SocketDevice` (required)

device = kocom               // socket 쓸 경우 월패드 이름{{장치이름}}

### Option: `Serial` (required)

port1 = /dev/ttyUSB0        // serial 쓸 경우 (월패드 혹은 그렉스)의 장치경로 작성
port2 = /dev/ttyUSB1        // serial 쓸 경우 (월패드 혹은 그렉스)의 장치경로 작성
port3 = /dev/ttyUSB2        // serial 쓸 경우 (월패드 혹은 그렉스)의 장치경로 작성

port2, port3는 추가,삭제 가능

### Option `SerialDevice` (required)

[SerialDevice]
port1 = kocom               // serial 쓸 경우 (월패드 이름 혹은 그렉스 이름) 작성{{장치이름}}
port2 = grex_ventilator     // serial 쓸 경우 (월패드 이름 혹은 그렉스 이름) 작성{{장치이름}}
port3 = grex_controller     // serial 쓸 경우 (월패드 이름 혹은 그렉스 이름) 작성{{장치이름}}

port2, port3는 추가,삭제 가능

{{장치이름}}
kocom = 코콤월패드
grex_ventilator = 그렉스 환기장치
grex_controller = 그렉스 환기장치의 리모콘(환기모드, 정지 등)

### Option `MQTT` (required)

anonymous = False           // MQTT 설정
server = 192.168.x.xx         // MQTT 서버
username = id                 // MQTT ID
password = pw                // MQTT PW


### Option `Wallpad` (required)

light = true                    // 조명 
plug = true                    // 플러그 
thermostat = true            // 난방 
fan = true                     // 환기팬 
gas = true                     // 가스 
elevator = true               // 엘레베이터 

true 혹은 false 대소문자 주의

### Option `Advanced` (required)

INIT_TEMP = 22 // 보일러 초기값
SCAN_INTERVAL = 300 // 월패드의 상태값 조회 간격
SCANNING_INTERVAL = 0.5 // 상태값 조회 시 패킷전송 간격

### Option `KOCOM_LIGHT_SIZE` (optional)
 name은 방이름, number는 조명 개수. 본인의 집 수량만큼 추가 가능.
{
  "name": "livingroom",
  "number": 3
}

### Option `KOCOM_PLUG_SIZE` (optional)
name은 방이름, number는 플러그 개수. 본인의 집 수량만큼 추가 가능.
{
  "name": "livingroom",
  "number": 3
}
### Option `KOCOM_ROOM` (optional)
방이름을 배열로 개수만큼 추가
"KOCOM_ROOM": [
  "livingroom",
  "bedroom",
  "room1",
  "room2",
  "kitchen"
]

방 패킷에 따른 방이름 패킷 이름은 00부터 01, 02로 시작하는 순서와 방이름이 매칭되어야 함
월패드에서 장치를 작동하며 방이름(livingroom, bedroom, room1, room2, kitchen 등)을 확인하여 본인의 상황에 맞게 바꾸세요

### Option `KOCOM_ROOM_THERMOSTAT` (required)
"KOCOM_ROOM_THERMOSTAT": [
    "livingroom",
    "bedroom",
    "room1",
    "room2"
  ]
조명/콘센트와 난방의 방패킷이 달라서 두개로 나뉘어있습니다.
방 패킷에 따른 방이름 패킷 이름은 00부터 01, 02로 시작하는 순서와 방이름이 매칭되어야 함
월패드에서 장치를 작동하며 방이름(livingroom, bedroom, room1, room2, kitchen 등)을 확인하여 본인의 상황에 맞게 바꾸세요

## Support

Got questions?

You have several options to get them answered:

- The [Korea Wallpad Controller][github].
- The [Home Assistant 네이버카페][forum].

버그신고는 카페나 깃허브로 해주세요 [open an issue on our GitHub][issue].

## Version : 0.4b

[forum]: https://cafe.naver.com/koreassistant
[github]: https://github.com/zooil/wallpadRS485
[issue]: https://github.com/zooil/wallpadRS485/issues
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg


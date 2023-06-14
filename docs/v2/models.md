---
layout: default
title: JSON Objects and Enums
nav_order: 5
parent: v2
has_children: false
# permalink: /docs/v2
---


REST API 파라메터로 사용되는 JSON 오브젝트와 Enum들입니다.

------------------------

# Channel

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | string | 채널 ID |
| inputUri | string | 입력 영상 주소 |
| channelName | string | 채널 이름 |
| inputType | int | 입력 영상 종류(**[InputType](models.md#inputtype)**) |
| status | Enum | 채널 상태 (**[ChannelStatus](#channelstatus)**)|

<br><br>

# ChannelStatus

| Enum | Description |
| :---- | :---- |
| CH_STATUS_NORMAL | 정상 |
| CH_STATUS_INPUT_DEVICE_CONNECTION_LOST | 입력장치 연결 끊김 |

<br>

# ObjectType

| Enum | Description |
| :---- | :---- |
| PERSON | 사람 |
| Vehicle | 차량 |
| Face | 얼굴 |
| Fire | 화재 |
| Head | 해드 |

<br>

# Roi Feature  

| Enum | Description |
| :---- | :---- |
| ALL | 내부/외부 객체 감지 |
| INSIDE | 내부 발생 감지 |
| OUTSIDE | 외부 발생 감지 |
| IGNORE | 비감지 |

<br>

# EventType

| Enum | Description |
| :---- | :---- |
| Unknown | 이벤트 미발생 |
| AllDetect | 모두 검출 |
| Loitering | 배회 |
| Intrusion | 침입 |
| ~~RoiEnter~~  | ~~영역 진입~~ |
| ~~AbnormalPosture~~  | ~~자세이상(앉음, 쓰러짐)~~ |
| Falldown | 쓰러짐 |
| Violence | 싸움 |
| ~~RoiExit~~ | ~~영역 ROI 개체진출(사라짐)~~ |
| ~~AbnormalCongestion~~  | ~~영역 ROI 내 이동흐름 정체 (정상흐름 대비 상대적 정체도)~~ |
| ~~AbandonedObject~~  | ~~유기물~~ |
| IllegalParking | 불법 주정차 |
| AbnormalObjectCount | 영역 ROI 내 개체밀집 (정의된 개체수 이상의 객체 존재) |
| Longstay | 영역 ROI 내 장시간 체류(주정차) |
| LineEnter | Line ROI를 지나가는 객체감지 (Enter 방향) |
| ~~LineExit~~ | ~~Line ROI를 지나가는 객체감지 (Exit 방향)~~ |
| LineCrossing | 양방향 라인 통과 |
| Direction | 방향성 이동 카운트 (좌, 우, 유턴 등) |
| LeftTurn | 차량 좌회전 |
| RightTurn | 차량 우회전 |
| UTurn | 차량 유턴 |
| ~~CongestionIndex~~ | ~~사람 혼잡도 레벨~~ |
| ~~VehicleDensity~~ | ~~차량 밀도~~ |
| ~~StopVehicleCount~~ | ~~정차 중인 차량 수 카운트~~ |
| Smoke | 화재 연기 |
| Flame | 화재 불꽃 |
| MatchingFace | 등록 얼굴 매칭 |
| NotWearingMask | 얼굴 마스크 미착용 |
| NoHelmet | 헬멧 미착용 |
| TrafficActuatedSignal | 차량 감응 신호 |
| ~~Weapon~~ | ~~무기~~ |
| NonDetectionArea | 비감지 영역 |

<br><br>

# ClassId

| Value | Name |
| :---- | :---- |
| 0 | Person |
| 2 | Falldown |
| 3 | Violence |
| 4 | Helmet |
| 5 | Head |
| 100 | Bike |
| 102 | Vehicle |
| 103 | Motorcycle |
| 104 | Bus |
| 105 | Truck |
| 106 | Excavator |
| 107 | TankTruck |
| 108 | Forklift |
| 109 | Lemicon |
| 110 | Cultivator |
| 111 | Tractor |
| 112 | ElectricCar |
| 200 | Fire Smoke |
| 201 | Fire Flame |
| 300 | Face |
| 500 | Bag |

<br><br>

# Functions

컴퓨팅 노드가 사용 가능한 기능들

| Enum | Description |
| :---- | :---- |
| FNC_CORE | 핵심 기능 |

<!-- | FNC_ITS | 지능형 교통 시스템 | -->


# InputType
입력 비디오 타입

| Enum | Description |
| :---- | :---- |
| SRC_IPCAM_NORMAL | 일반 카메라 (Default) 영상 |
| SRC_IPCAM_THERMAL | 열화상 카메라 영상 |
| SRC_IPCAM_DEPTH | 깊이센서 카메라 영상 |
| SRC_ETC | 기타 영상 |

<br><br>

# SystemWarnings

| Enum | Description |
| :---- | :---- |
| SYS_RESOURCE_FULL | 시스템 리소스 한계 사용 중 |
| SYS_UNSTABLE_NETWORK | 네트워크 불안정 |
| SYS_NO_LICENSE | 라이센스 없음 |
| SYS_LICENSE_EXPIRED | 라이센스 만료 |

<br>

# Performance

| Name | Type | Description |
| :---- | :---- |:---- |
| cpuUsage | Double | CPU 사용률 |
| gpuUsage | Double | GPU 사용률 |
| memoryUsage | Double | Memory 사용률 |
| diskUsage | Double | Disk 사용률 |


<br>

# Version

| Name | Type | Description |
| :---- | :---- |:---- |
| software | String | NK 프로그램 버전 |
| detectorModel | Dynaimc Dictionary | model version |
| firmware | String | 펌웨어 버전 (OS) |
| gpuModel | String | GPU 모델 |
| gpuVersion | String | GPU 버전 |


<br>

# Calibration
| Name | Type | Description |
| :---- | :---- |:---- |
| focalLengthX | Double | 초첨거리 X | 
| focalLengthY | Double | 초첨거리 Y |
| principalX | Double | 원리좌표 X |
| principalY | Double | 원리좌표 Y |
| fov         | Double | 화각 |
| imageWorldX | Double | 이미지 월드좌표 X|
| imageWorldY | Double | 이미지 월드좌표 Y|
| imageWorldZ | Double | 이미지 월드좌표 Z|
| cameraPanDegree | Double | 카메라 Pan 각도 |
| cameraTiltDegree | Double | 카메라 Pan 각도 |
| cameraHorizontalAngle | Double | 카메라 수평각 |

<br>


<!-- # RecentCrashLogs
최근 비정상 종료 된 컴퓨팅 노드 기록정보

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| crashTime | String | 비정상 종료 시각 |

<br><br> -->



# Operations

비디오 분석 제어 명령들

| Enum | Description |
| :---- | :---- |
| VA_START | 비디오 분석 시작/재개 |
| VA_STOP | 비디오 분석 중지 |
| VA_RESET | 비디오 분석 중 누적 집계된 값들을 모두 초기화 (즉, ROI 설정 직후 상태로 초기화) |


# Error code

| Value | Description |
| :---- | :---- |
| 0 | 성공 |
| 10 | api uri path 문제 |
| 11 | api 요청 데이터 포맷 문제 |
| 12 | 지원하지 않는 기능 |
| 20 | 라이선스 비활성화 |
| 21 | 라이선스 기간 만료 |
| 22 | 지원하지 않는 API 버전 |
| 23 | RPC 포트 문제 |
| 24 | HTTP 포트 문제 |
| 100 | 컴퓨팅 노드 생성 실패|
| 200 | 채널 영상 수신 실패|
| 201 | 채널 생성 실패 |
| 210 | 캘리브레이션 실패 |
| 220 | 스냅샷 생성 실패 |
| 300 | ROI 설정 실패 |
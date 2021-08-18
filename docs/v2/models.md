---
layout: default
title: 모델
nav_order: 7
parent: v2
has_children: false
# permalink: /docs/v2
---


REST API에서 사용 되는 내부 클래스와 Enum 구조들입니다.

------------------------

# Channel Model

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| nodeId | String | 컴퓨팅 노드 ID |
| inputUri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) |
| channelName | String | 채널 별칭 |
| inputType | enum([InputType](models.md#inputtype)) | 입력 비디오 타입 |
| siblings | [String] | 연결된 채널 id 목록 |
| status | enum([ChannelStatus](#channelstatus)) | 채널 상태 |

<br><br>

# ChannelStatus

| Enum | Description |
| :---- | :---- |
| CH_STATUS_NORMAL | 정상 |
| CH_STATUS_INPUT_DEVICE_CONNECTION_LOST | 입력장치 연결 끊김 |

<br><br>

# Distortion Point

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| startPoint | [Double] |  첫 번째 점의 X, Y 좌표 비율 (0 ~ 1)| O |
| middlePoint | [Double] |  중간 점의 X, Y 좌표  비율 (0 ~ 1)| O |
| endPoint | [Double] |  마지막 점의 X, Y 좌표  비율 (0 ~ 1)| O |


<br><br>

# Calibration Point

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| verticalPoint1 | [Double] |  세로로 된 직선 1의 시작, 끝 X, Y 좌표 비율 (0 ~ 1)| O |
| verticalPoint2 | [Double] |  세로로 된 직선 2의 시작, 끝 X, Y 좌표 비율 (0 ~ 1)| O |
| horizontalPoint1 | [Double] |  가로로 된 직선 1의 시작, 끝 X, Y 좌표 비율 (0 ~ 1)| O |
| horizontalPoint2 | [Double] |  가로로 된 직선 2의 시작, 끝 X, Y 좌표 비율 (0 ~ 1)| O |

<br><br>

# Object Type

| Enum | Description |
| :---- | :---- |
| PERSON | 사람 |
| CAR | 일반 차량 |
| MOTOCYCLE | 오토바이 |
| BUS | 대형 버스 |
| TRUCK | 트럭 |
| FLAME | 불꽃 |
| SMOKE | 연기 |

# EventType

| Enum | Description |
| :---- | :---- |
| EVT_LOITERING | 배회 |
| EVT_INTRUSION | 침입 |
| EVT_QUEUEING | 대기열 |
| EVT_ABNORMAL_CONGESTION | 영역 ROI 내 이동흐름 정체 (정상흐름 대비 상대적 정체도) |
| EVT_ABNORMAL_OBJ_COUNT | 영역 ROI 내 개체밀집 (정의된 개체수 이상의 객체 존재) |
| EVT_ROI_COUNT | 영역 ROI 카운팅 |
| EVT_LINE_COUNT | ROI 카운팅 |
| EVT_ILLEGAL_PARKING | 불법 주정차 |
| EVT_WRONG_WAY | 역주행 |
| EVT_DIRECTION_COUNTING | 방향성 이동(직전, 좌/우회전, 유턴) 카운팅 |
| EVT_VEHICLE_SPEED | 차량 속도 |
| EVT_VEHICLE_DENSITY | 차량 밀도 |
| EVT_STOP_VEHICLE_COUNTING | 정지 차량 카운팅 |
| EVT_SIGNAL_WAITING_TIME | 신호 대기 시간 |
| EVT_PARKING_SPACE | 주차공간 점유 여부 검출 |
| EVT_TRAFFIC_ACTUATED_SIGNAL | 교통 감응신호 (rs232 통신으로 옵션보드로 차량 유무 신호 전송) |
| EVT_CROSSWALK_QUEUEING | 횡단보도 대기열 카운팅 |

<br><br>

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


<br><br>


# RecentCrashLogs
최근 비정상 종료 된 컴퓨팅 노드 기록정보

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| crashTime | String | 비정상 종료 시각 |

<br><br>

# error code

| Value | Description |
| :---- | :---- |
| 0 | 성공 |
| 100 | 등록되지 않은 채널 |
| 101 | RTSP 포멧이 정확하지 않음 |
| 102 | 카메라 접근 계정 인증 오류 |
| 103 | 카메라에 연결 할 수 없음 (포멧은 정확하나 카메라가 정상 동작 중이지 않는 상태) |
| 110 | 캘리브레이션 실패 |
| 111 | 스냅샷 생성 실패 |
| 200 | 노드에 연결 할 수 없음 |
| 201 | 노드에 연결 할 수 없음 |
| 300 | 분석이 이미 실행 중  |
| 301 | 분석이 미동작 상태 |
| 302 | 분석을 시작 할 수 없는 상태 (카메라 등록 안됨) |
| 303 | 분석을 시작 할 수 없는 상태 (등록은 되어있으나 카메라에 연결 할 수 없는 상태) |
| 310 | ROI 설정이 알 맞지 않음 (point가 3개 일 순 없음) |

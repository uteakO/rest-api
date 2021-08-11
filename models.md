REST API에서 사용 되는 내부 클래스와 Enum 구조들입니다.

------------------------

### Channel Model
| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| nodeId | String | 컴퓨팅 노드 ID | X |
| inputUri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) |
| channelName | String | 채널 별칭 |
| inputDeviceType | enum([InputType](models.md#inputtype)) | 입력장치 타입|
| siblings | [String] | 연결된 채널 id 목록 |
| status | enum([ChannelStatus](#channelstatus)) | 채널 상태 |

<br><br>

### ChannelStatus

| Enum | Description |
| :---- | :---- |
| CH_STATUS_NORMAL | 정상 |
| CH_STATUS_INPUT_DEVICE_CONNECTION_LOST | 입력장치 연결 끊김 |
| CH_STATUS_INPUT_DEVICE_CONNECTION_LOST | 입력장치 연결 끊김 |

<br><br>

### EventType

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

### InputType

| Enum | Description |
| :---- | :---- |
| SRC_IPCAM_NORMAL | 일반 카메라 (Default) 영상 |
| SRC_IPCAM_THERMAL | 열화상 카메라 영상 |
| SRC_IPCAM_DEPTH | 깊이센서 카메라 영상 |
| SRC_ETC | 기타 영상 |

<br><br>

### RecentCrashLogs

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| crashTime | String | 비정상 종료 시각 |
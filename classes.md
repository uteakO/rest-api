REST API에서 사용 되는 내부 클래스와 Enum 구조들입니다.

------------------------








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



### DeviceType

| Enum | Description |
| :---- | :---- |
| IPCAM_NORMAL | 일반 카메라 (Default)|
| IPCAM_THERMAL | 열화상 카메라 |
| IPCAM_DEPTH | 깊이센서 카메라 |
| ETC | 기타 장치 |

비디오 분석 설정에 대한 API입니다.

------------------------
# 비디오 분석 제어
이 API를 이용하여 지정 채널에 대해 비디오 분석을 시작하거나 중지할 수 있습니다.
또한, ROI 영역의 검출객체 카운팅 상태들을 초기화할 수 있습니다.
```
POST /v2/va/control
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| operation | [[Operations](#enum-operations)] | 제어 명령 | O |


#### Enum Operations

| Enum | Description |
| :---- | :---- |
| VA_START | 비디오 분석 시작 |
| VA_STOP | 비디오 분석 중지 |
| ROI_RST_ENTER | 진입 카운트 초기화 |
| ROI_RST_EXIT | 진출 카운트 초기화 |
| ROI_RST_PASS | 통과 카운트 초기화 |
| ROI_RST_AVG_STAYING_TIME | 평균 대기 시간 초기화 |
| ROI_RST_ALL | 전체 초기화 |




<br><br>
# ROI 설정

## ROI 생성
지정한 채널에 대해 ROI 영역을 정의하고, 분석 알고리즘을 설정합니다.
```
POST /v2/va/create-roi
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | string | 채널 ID | O |
| description | string | 설명 | X |
| points | [Double] | ROI 좌표 리스트 (0.0~1.0으로 정규화) | O |
| analysisConfigs | object ([AnalysisConfig](#analysisconfigs)) | 분석 설정 | X |

#### JSON sample
```
{
    "channelId": "X1ashF0t",
    "analysisType": "EVT_LOITERING",
    "description": "Loitering and intrusion detection for CCTV #3",
    "roi": [0.2, 0.2, 0, 0.5, 0.7, 0.1],
    "analysisConfigs": {
        "loiteringConfig": {
            abnormalStayTime: 1.0,
            abnormalCi: 1.0
        },
        "intrusionConfig": {
            abnormalStayTime: 1.0,
            abnormalCi: 1.0
        }
    }
}
```
<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | ROI ID |

#### JSON sample
```
{
    "roiId": "Vif7f02j"
}
```




<br><br>






----------------
# AnalysisConfigs

#### JSON 표현

```
{
    "loiteringConfig": object (LoiteringConfig),
    "intrusionConfig": object (IntrusionConfig)
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| loiteringConfig | object (LoiteringConfig) | 배회 감지 설정 | X |


<br><br>
## 일반 분석 설정
### LoiteringConfig

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| abnormalStayTime | Double | 배회 감지 시간 | O |
| abnormalCi | Double | 영역 ROI 내 이동흐름 정체: 정체도 기준값 | O |


### IntrusionConfig

### QueueingConfig

### AbnormalCongestionConfig

### AbnormalObjCountConfig

### RoiCountConfig

### LineCountConfig


<br><br>

## ITS 전용 분석 설정

### IllegalParkingConfig

### WrongWayConfig

### DirectionCountingConfig

### VehicleSpeedConfig

### VehicleDensityConfig

### StopVehicleCountingConfig

### SignalWaitingTimeConfig

### ParkingSpaceConfig

### TrafficActivatedSignalConfig

### CrosswalkQueueingConfig
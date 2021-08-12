비디오 분석 설정에 대한 API입니다.

__목차__
- [비디오 분석 제어](#비디오-분석-제어)
- [ROI 생성](#roi-생성)
- [ROI 조회](#roi-조회)
- [채널 내 ROI 목록 조회](#채널-내-roi-목록-조회)
- [ROI 수정](#roi-수정)
- [ROI 삭제](#roi-삭제)
- [AnalysisConfigs](#analysisconfigs)

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
| ROI_RST_COUNT | 이벤트 카운트 초기화 |
| ROI_RST_AVG_STAYING_TIME | 평균 대기 시간 초기화 |
| ROI_RST_ALL | 전체 초기화 |




<br><br>

# ROI 설정

ROI(Region of interest; 관심영역)은 비디오 분석을 실행할 화면 내 영역이며, 분석 종류에 따라 선 또는 폴리곤 형태가 필요합니다.

한 개 채널에 여러 개의 ROI가 존재할 수 있습니다.

<!-- 
- line, polygon을 구분하여 가독성을 높일 수 있는 파라메터 정의방식이 필요할 듯...
-->

## ROI 생성
지정한 채널에 대해 ROI를 정의하고, 분석 알고리즘을 설정합니다.
```
POST /v2/va/create-roi
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | string | 채널 ID | O |
| description | string | ROI 설명 | X |
| shape | [RoiShape](#roishape) | ROI 형태 | O |
| analysisConfigs | object ([AnalysisConfig](#analysisconfigs)) | 분석 설정 | X |


#### RoiShape

ROI 영역을 정의합니다. 선 또는 폴리곤으로 구성될 수 있으며 모든 값들은 0.0~1.0으로 정규화 된 좌표로 구성 됩니다.

| Name | Type | Description |
| :---- | :---- |:---- |
| polygon | [Integer] | 폴리곤을 구성하는 점의 좌표들|
| line0 | [Integer] | 0 번째 라인을 구성하는 두 점의 좌표들 |
| line1 | [Integer] | 1 번째 라인을 구성하는 두 점의 좌표들 |

<!-- 
비디오 분석 기능을 제공하기 위해 line이 2개 넘게 필요한 것이 있다면 line2, 3 ... 더 추가하기 
-->

#### JSON sample
```
{
    "channelId": "X1ashF0t",
    "description": "Loitering and intrusion detection for CCTV #3",
    "shape": {
        "polygon": [0.2, 0.2, 0, 0.5, 0.7, 0.1]
    },
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

<!-- 
RoiShape와 호환되지 않는 분석기능이 파라메터로 들어와서 호출 된 경우, 실패 응답하기 
-->

#### JSON sample
```
{
    "roiId": "Vif7f02j"
}
```




<br><br>



## ROI 조회
ROI를 조회합니다.
```
POST /v2/va/get-roi
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiId | string | ROI ID | O |

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | ROI ID |
| channelId | string | 채널 ID |
| description | string | 설명 |
| shape | [RoiShape](#roishape) | ROI 형태 |
| analysisConfigs | object ([AnalysisConfig](#analysisconfigs)) | 분석 설정 |


<br><br>



## 채널 내 ROI 목록 조회
지정한 채널에 추가 된 모든 ROI들을 조회합니다.
```
POST /v2/va/list-roi
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | string | 채널 ID | O |

<br>

### Response

[ROI 조회](roi-조회) 응답의 배열입니다.

<br><br>


## ROI 수정
ROI 설정을 수정합니다.
```
POST /v2/va/update-roi
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiId | string | 채널 ID | O |
| channelId | string | 채널 ID | X |
| description | string | ROI 설명 | X |
| shape | [RoiShape](#roishape) | ROI 형태 | X |
| analysisConfigs | object ([AnalysisConfig](#analysisconfigs)) | 분석 설정 | X |


<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | ROI ID |


<br><br>


## ROI 삭제
ROI 설정을 삭제합니다.
```
POST /v2/va/remove-roi
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiId | string | 채널 ID | O |


<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | ROI ID |


<br><br>

----------------
# AnalysisConfigs

<!-- 
- 빠진 기능 추가하기 (연기, 불꽃, 싸움, 쓰러짐)
- 적절히 네이밍 변경하기
- 기능마다 달라지는 설정 파라메터 반영하기 
- 세부 설정 파라메터(threshold) 추가하고 기본 값 정의하기
-->

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

폴리곤 영역 내 배회 객체를 감지합니다.

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
line0를 통과하는 객체들을 카운팅합니다.


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
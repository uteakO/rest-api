비디오 분석 설정에 대한 API입니다.

------------------------
# 비디오 분석 상태 제어
### 비디오 분석 시작

```
POST /v2/va/channels/start-analysis
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |

<br><br>
### 비디오 분석 중지

```
POST /v2/va/channels/stop-analysis
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |

<br><br>

# 누적 값 초기화

채널 내 설정 된 ROI들에 대해, 현재까지 검출 된 객체들의 누적 값을 초기화 시키는 기능입니다.

### 진입 카운트 초기화

```
POST /v2/va/channels/reset-enter-count
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |

<br><br>
### 진출 카운트 초기화

```
POST /v2/va/channels/reset-exit-count
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |

<br><br>
### 통과 카운트 초기화

```
POST /v2/va/channels/reset-pass-count
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |


<br><br>
### 평균 대기 시간 초기화

```
POST /v2/va/channels/reset-average-staying-time
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |

<br><br>
### 전체 초기화

```
POST /v2/va/channels/reset-all
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |


<br><br>


# 비디오 분석 기능 설정

```
POST /v2/va/channels/{channel_id}/analysis/register
```


| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |
| event_type | enum([EventType](classes.md#EventType)) | 이벤트 타입 | O |
| description | String | 이벤트 설명 | X |
| configs | {AnalysisConfigs} | 이벤트 설명 | X |

<br><br>
----------------
# AnalysisConfigs

## 일반 분석 설정
### LoiteringConfig

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roi | [Double] | ROI 좌표 리스트 (0.0~1.0으로 정규화) | O |
| abnormal_stay_time | Double | 배회 감지 시간 | O |
| abnormal_ci | Double | 영역 ROI 내 이동흐름 정체: 정체도 기준값 | O |


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
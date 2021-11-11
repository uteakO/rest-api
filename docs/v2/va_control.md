---
layout: default
title: 비디오 분석 설정
nav_order: 4
parent: v2
has_children: false
# permalink: /docs/v2
---


비디오 분석 설정에 대한 API입니다.

------------------------

# ROI 생성
지정한 채널에 관심 영역을 정의하고, 관심 영역 내 분석 알고리즘을 설정합니다.
(다각형 영역만을 지원)

<br>

### Request
```
POST /v2/va/create-roi

{
  "nodeId": "184fcb3c",
  "channelId": "72040f36",
  "roiName": "ROI_NAME",
  "description": "Loitering Event",
  "eventtype": "EVT_LOITERING",
  "roiDots": [
    {
      "X": 0.0,
      "Y": 0.0
    },
    {
      "X": 1.0,
      "Y": 0.0
    },
    {
      "X": 1.0,
      "Y": 1.0
    },
    {
      "X": 0.0,
      "Y": 1.0
    }
  ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiName | String | 이벤트 이름 | O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| eventType | Enum | 영역 속성([InputType](models.md#EventType))| O |
| description | String | 관심 영역 설명 | X |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |

<br/>

### Response
```
// Ok
{
  "roiId": "88e2a515",
  "code": 0
}
// Fail
{
    "code" : 300,
    "message" : "Failed Create Roi"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br/>

### Roi Dot

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| X | Integer | X 좌표 | O |
| Y | Integer | Y 좌표 | O |
| lineUntilNextDot | JsonObject[] | 검출 객체([RoiLine](#roi-line)) | O |

<br/>

### Roi Line

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| disable | boolean | 비활성화 | O |
| direction | String | 방향 설정 | O |
| target | JsonObject[] | 검출 객체([ObjectType](#object-type)) | O |

<br><br>

# ROI 조회
ROI를 조회합니다.
<br>

### Request
```
POST /v2/va/get-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiId": "88e2a515"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |

<br>

### Response
```
{
  "roiId": "88e2a515",
  "name": "ROI_NAME",
  "description": "Loitering Event",
  "stayTime": 0.0,
  "numberOf": 0,
  "eventType": "EVT_LOITERING",
  "roiDots": [
    {
      "x": 0.0,
      "y": 0.0
    },
    {
      "x": 1.0,
      "y": 0.0
    },
    {
      "x": 1.0,
      "y": 1.0
    },
    {
      "x": 0.0,
      "y": 1.0
    }
  ],
  "code": 0
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiNmae | String | 이벤트 이름 | O |
| description | String | 관심 영역 설명 | O |
| stayTime | Integer | 발생 지연 시간 | O |
| numberOf | Integer | 최소 발생 객체수 조건 | O |
| eventType | Enum | 영역 속성([InputType](models.md#EventType))| O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) | O|
| message | String | 오류 메시지 |X|

<br><br>

# 채널 내 ROI 목록 조회
지정한 채널에 추가 된 모든 ROI들을 조회합니다.

<br>

### Request
```
POST /v2/va/list-roi

{
    "nodeId":"c6a45bc6"
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |

<br>

### Response
```
{
  "channels": [
    {
      "channelId": "e84fcac4",
      "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
      "channelName": "TEST_CHANNEL_NAME",
      "inputType": 0,
      "status": 0
    }
  ],
  "code": 0
}
```

[ROI 조회](#roi-조회) 응답의 배열입니다.

<br><br>

# ROI 수정
(추적기 리셋 오류 발생중..)
ROI 설정을 수정합니다.
```
POST /v2/va/update-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiId": "88e2a515",
  "roiNmae" : "UPDATE_ROI",
  "roiDots": [
    {
      "x": 0.0,
      "y": 0.0
    },
    {
      "x": 0.84,
      "y": 0.0
    },
    {
      "x": 0.84,
      "y": 0.22
    },
    {
      "x": 0.0,
      "y": 0.5
    }
  ],
}
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |
| roiNmae | String | 이벤트 이름 | X |
| description | String | 관심 영역 설명 | X |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| feature | string | 영역 속성([RoiFeature](#roi-feature)) | X |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | X |



<br>

### Response
```
{
    "roiId": "88e2a515",
    "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

# ROI 삭제
ROI 설정을 삭제합니다.

<br>

### Request
```
POST /v2/va/remove-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiIds": [
       "88e2a515",
       "19389bdc"
    ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String[] | 관심 영역 ID | O |


<br>

### Response
```
{
  "roiId": "e84fcac4",
  "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Remarks
링크되어있는 ROI는 VA를 중지 후 삭제 해야합니다.

<br><br>

# Link
사용자가 직접 설정한 Roi 간의 이벤트 조건을 만드는 기능

# ROI Link 생성
영역 간의 이벤트 연계 기능을 추가할수 있습니다.

<br>

### Request
```
POST /v2/va/create-link
{
  "nodeId": "c6a45bc6",
  "channelId": "b501189c",
  "name": "link0_0"
  "roiLink": [
      "e84fcac4", 
      "asdasd11"
    ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| name | String | 연계 이벤트 이름 | O |
| roiLink | String[] | 연계 영역 설정 | O |

### Link

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiId | String | ROI ID | O |
| nextRoiRealDistance | Integer | 다음 영역까지 실제 거리 | X |
| nextRoiArrivalWaitingTime | Integer | 다음 영역까지 도착 대기 시간 | X |

<br>

### Response
```
{
  "linkId": "bascd123be",
  "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| linkId | String | 링크 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

# ROI Link 조회
ROI를 조회합니다.

<br>

### Request
```
POST /v2/va/get-link

{
    "nodeId": "c6a45bc6",
    "channelId": "b501189c",
    "linkId" : "bascd123be"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| linkId | String | 연계 이벤트 ID | O |

<br>

### Response
```
{
    "linkId" : "bascd123be",
    "name": "link0_0",
    "roiLink": [
      "e84fcac4", 
      "asdasd11"
    ],
    "code" : 0
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| linkId | String | 연계 이벤트 ID | O |
| channelId | String | 채널 ID | O |
| name | String | 연계 이벤트 이름 | O |
| roiLink | String[] | 연계 영역 설정 | O |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |
<!--| shape | [RoiShape](#roishape) | ROI 형태 |-->
<br><br>

# 채널 내 Roi Link 조회
ROI 설정을 조회합니다.

<br>

### Request
```
POST /v2/va/list-link
{
    "nodeId": "c6a45bc6",
    "channelId": "b501189c",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

# Roi Link 수정
ROI 설정을 수정합니다.


<br>

### Request
```
POST /v2/va/update-link
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| linkId | String | 연계 이벤트 ID | O |
| name | String | 연계 이벤트 이름 | X |
| roiLink | JsonObject[] | 연계 영역 설정 ([Link](#link)) | X |


<br>

### Response
```
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

# Roi Link 삭제
ROI 설정을 삭제합니다.

<br>

### Request
```
POST /v2/va/remove-link
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| linkId | String[] | 연계 이벤트 ID 리스트 | O |


<br>

### Response
```
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>


# 비디오 분석 제어
이 API를 이용하여 지정 채널에 대해 비디오 분석을 시작하거나 중지할 수 있습니다.
또한, ROI 영역의 검출객체 카운팅 상태들을 초기화할 수 있습니다.

<br>

#### Request

```
POST /v2/va/control

# VA_START
{
    "nodeId":"a46147f4",
    "channelId": "19fa5688",
    "operation": "VA_START"
}

# VA_STOP
{
    "nodeId":"a46147f4",
    "channelId": "19fa5688",
    "operation": "VA_STOP"
}

# VA_RST
{
    "channelId" : "X1ashF0t",
    "operation" : "VA_RST",
    "parameter" : ["roiId1", "roiId2", "roiId3"]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 채널 ID | O |
| channelId | String | 채널 ID | O |
| operation | String | 제어 명령 ([Operations](models#enum-operations)) | O |
| parameter | String[] | 필요시 파라미터 전달 | X |

<br>

#### Response
```
//VA_START
{
  "sourceIp": "192.168.0.36",
  "sourcePort": 33300,
  "code": 0
}
//VA_STOP
{
  "code": 0
}
//VA_RESET

```

| Name | Type | Description |
| :---- | :---- |:---- |
| sourceIp | String | Channel GRPC IP |
| sourcePort | Integer | Channel GRPC Port |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

#### Remarks

parameter는 Reset에서 사용되는 ROI 리스트 등 그외에도 사용될 수 있으며, 추후 확장성을 위함..
VA_START를 하기 위해서는 ROI가 먼저 생성 되어있어야함.


```
## 성공
# VA_START
{
    "sourceIp" : "192.168.0.30",
    "sourcePort" : "40400"
    "code" : 0
}

# VA_STOP, VA_RST
{
    "code" : 0
}

## 실패
{
    "code" : 300,
    "message" : "fail"
}
```

<br><br>

# Roi Feature  

| Enum | Description |
| :---- | :---- |
| ALL | 내부/외부 객체 감지 |
| INSIDE | 내부 발생 감지 |
| OUTSIDE | 외부 발생 감지 |
| IGNORE | 비감지 |

<br>

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

<br><br>
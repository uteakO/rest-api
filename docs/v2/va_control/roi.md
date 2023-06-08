---
layout: default
title: ROI
nav_order: 2
parent: 영상 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/roi
---


영상 내 ROI(Region of interest) 설정 API입니다.

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
  "eventType": "EVT_LOITERING",
  "roiName": "ROI_NAME",
  "roiType": 2,
  "feature": 0,
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
  ],
  "EventFilter":
    {
      "minDetectSize": 1,
      "maxDetectSize": 100,
      "objectsTarget": [0]
    },
  "stayTime": 0,
  "numberOf": 0,
  "roiNumber": 0
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| eventType | Enum | 영역 속성([EventType](/docs/v2/models.md#event-type))| O |
| roiName | String | 이벤트 이름 | O |
| roiType | Enum | ROI 타입([DrawingType](#drawing-type)) | O |
| feature | Enum | ROI 감지([ROI Feature](/docs/v2/models.md#roi-feature)) | O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| EventFilter | Enum | 객채 검출 사이즈 필터([EventFilter](#event-filter))| O |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| roiNumber | Enum | 차선 종류 | O |

<br>

### Response
```
// Ok
{
  "roiId": "88e2a515",
  "code": 0,
  "message": ""
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
| code | Integer | 오류 코드 ([Error Code](/docs/v2/models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Roi Dot

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| X | Integer | X 좌표 | O |
| Y | Integer | Y 좌표 | O |
| lineUntilNextDot | JsonObject[] | 검출 객체([RoiLine](#roi-line)) | O |

<br>

<br>

### Drawing Type

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| None | Integer | 없음 | O |
| Polygon | Integer | 다각형 | O |
| Rect | Integer | 사각형 | O |
| Line | Integer | 라인 | O |
| MultiLine | Integer | 멀티 라인 | O |
| All | Integer | 전체 영역 | O |


<br>

<br>

### Event Filter

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| minDetectSize | Integer | 최소 객체 크기 | O |
| maxDetectSize | Integer | 최대 객체 크기 | O |
| objectsTarget | enum | 검출 객체([RoiLine](#roi-line)) | O |

<br>


### Roi Line

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| disable | boolean | 비활성화 | O |
| direction | String | 방향 설정 | O |
| target | JsonObject[] | 검출 객체([ObjectType](#object-type)) | O |

<br><br>

# ROI 조회
지정한 채널에 추가 된 모든 ROI들을 조회합니다.

<br>

### Request
```
POST /v2/va/list-roi

{
    "nodeId":"c6a45bc6",
    "channelId":"svb90sc5"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |

<br>

### Response
```
{
  "rois": [
	  {
      "EventFilter": 
        {
          "minDetectSize": 0
          "maxDetectSize": 0,
          "objectsTarget": [0]
        },
      "description": "", 
      "eventType": "AllDetect", 
      "feature": -3689348814741910324, 
      "name" : "test name",
      "numberOf": 0, 
	    "objectTypes": [0], 
	    "roiDots": [
		    {
          "x": 0.4, 
          "y": 0.1
        }, 
  		  {
          "x": 0.9, 
          "y": 0.1
        }, 
		    {
          "x": 0.9, 
          "y": 0.6
        }, 
		    {
          "x": 0.4, 
          "y": 0.6
        }
		  ], 
	    "roiId": "3aa26e5979b14636", 
	    "roiNumber": 0, 
	    "roiType": 2, 
	    "stayTime": 0
	  }
  ]
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| rois | Array | ROI 영역 배열 | O |
| EventFilter | Enum | 객채 검출 사이즈 필터([EventFilter](#event-filter))| X |
| description | String | 관심 영역 설명 | X |
| eventType | Enum | 영역 속성([EventType](/docs/v2/models.md#event-type))| O |
| feature | Enum | ROI 감지([ROI Feature](/docs/v2/models.md#roi-feature)) | X |
| name | String | 영역 이름 | O |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| objectTypes | Enum | 객체 종류([ClassId](/docs/v2/models.md#ClassId)) | O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| roiId | String | 관심 영역 ID | O |
| roiNumber | Enum | 차선 종류 | O |
| roiType | Enum | ROI 타입([DrawingType](#drawing-type)) | O |
| stayTime | Integer | 발생 지연 시간 | X |

<br><br>

# ROI 수정

(추적기 리셋 오류 발생중..)
ROI 설정을 수정합니다.

<br>

### Request

```
POST /v2/va/update-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiId": "88e2a515",
  "eventType":"AllDetect",
  "roiNmae" : "UPDATE_ROI",
  "description": "",
  "stayTime": 0,
  "numberOf": 0,
  "feature": 0,
  "roiType": 2,
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
  "EventFilter":
    {
      "minDetectSize": 1,
      "maxDetectSize": 100,
      "objectsTarget": [0]
    },
  "roiNumber": 0
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |
| eventType | Enum | 영역 속성([EventType](/docs/v2/models.md#event-type))| O |
| roiName | String | 이벤트 이름 | O |
| description | String | 관심 영역 설명 | X |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| feature | string | 영역 속성([RoiFeature](#roi-feature)) | X |
| roiType | Enum | ROI 타입([DrawingType](#drawing-type)) | O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| EventFilter | Enum | 객채 검출 사이즈 필터([EventFilter](#event-filter))| O |


<br>

### Response
```
{
    "code": 0
    "message" : ""
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
  "code": 0,
  "message" : ""
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

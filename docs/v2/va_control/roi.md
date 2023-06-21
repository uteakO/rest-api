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
    "eventType": "Loitering",
    "roiName": "ROI_NAME",
    "roiType": 2,
    "feature": 0,
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
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| eventType | Integer | 이벤트 종류 (**[EventType](/docs/v2/models.md#eventtype)**)| O |
| roiName | String | ROI 이름 | O |
| roiType | Integer | ROI 타입 (**[DrawingType](#drawing-type)**) | O |
| ~~feature~~ | ~~Integer~~ | [unsupported] ~~ROI 감지~~ (**[ROI Feature](/docs/v2/models.md#roi-feature)**) | O |
| roiDots | JsonObject[] | ROI 라인 설정 (**[RoiDot](/docs/v2/models.md#roi-dot)**) | O |
| EventFilter | JsonObject | 객채 검출 사이즈 필터 (**[EventFilter](/docs/v2/models.md#event-filter)**)| O |
| ~~stayTime~~ | ~~Integer~~ | [unsupported] ~~발생 지연 시간~~ | X |
| ~~numberOf ~~ | ~~Integer~~ | [unsupported] ~~최소 발생 객체수 조건~~ | X |
| roiNumber | Integer | 차선 번호 | O |

<br>

### Response
```
// SUCCESS
{
    "roiId": "88e2a515",
    "code": 0,
    "message": ""
}
// REQUEST_TIMTOUT
{
    "roiId": "",
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "roiId": "",
    "code": 503,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| roiId | String | 관심 영역 ID | O |
| code | Integer | 응답 코드 (**[Error Code](/docs/v2/models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

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
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |

<br>

### Response
```
// SUCCESS
{
    "rois": [
	    {
          "EventFilter": 
              {
                  "minDetectSize": 0,
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
    ],
    "code": 0,
    "message": ""
}
// REQUEST_TIMTOUT
{
    "rois": [],
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "rois": [],
    "code": 503,
    "message": ""
}
// NOT_FOUND_CHANNEL_UID
{
    "rois": [],
    "code": 505,
    "message": ""
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| rois | Array | ROI 영역 배열 | O |
| EventFilter | JsonObject | 객채 검출 사이즈 필터(**[EventFilter](/docs/v2/models.md#event-filter)**)| X |
| description | String | 관심 영역 설명 | X |
| eventType | Integer | 이벤트 종류 (**[EventType](/docs/v2/models.md#eventtype)**)| O |
| ~~feature~~ | ~~Integer~~ | [unsupported] ~~ROI 감지~~(**[ROI Feature](/docs/v2/models.md#roi-feature)**) | X |
| name | String | 영역 이름 | O |
| ~~numberOf~~ | ~~Integer~~ | [unsupported] ~~최소 발생 객체수 조건~~ | X |
| objectTypes | Integer[] | 객체 종류(**[ClassId](/docs/v2/models.md#ClassId)**) | O |
| roiDots | JsonObject[] | ROI 라인 설정(**[RoiDot](/docs/v2/models.md#roi-dot)**) | O |
| roiId | String | 관심 영역 ID | O |
| roiNumber | Integer | 차선 종류 | O |
| roiType | Integer | ROI 타입(**[DrawingType](#drawing-type)**) | O |
| ~~stayTime~~ | ~~Integer~~ | [unsupported] ~~발생 지연 시간~~ | X |

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
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |
| eventType | Integer | 이벤트 종류 (**[EventType](/docs/v2/models.md#eventtype)**)| O |
| roiName | String | 이벤트 이름 | O |
| description | String | 관심 영역 설명 | X |
| ~~stayTime~~ | ~~Integer~~ | [unsupported] ~~발생 지연 시간~~ | X |
| ~~numberOf~~ | ~~Integer~~ | [unsupported] ~~최소 발생 객체수 조건~~ | X |
| ~~feature~~ | ~~string~~ | [unsupported] ~~영역 속성~~ (**[RoiFeature](/docs/v2/models.md#roi-feature)**) | X |
| roiType | Integer | ROI 타입 (**[DrawingType](#drawing-type)**) | O |
| roiDots | JsonObject[] | ROI 라인 설정 (**[RoiDot](/docs/v2/models.md#roi-dot)**) | O |
| EventFilter | JsonObject | 객채 검출 사이즈 필터 (**[EventFilter](/docs/v2/models.md#event-filter)**)| O |


<br>

### Response
```
// SUCCESS
{
    "code": 0
    "message" : ""
}
// REQUEST_TIMTOUT
{
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "code": 503,
    "message": ""
}
// NOT_FOUND_ROI_ID
{
    "code": 504,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| roiId | String | 관심 영역 ID | O |
| code | Integer | 응답 코드 (**[Error Code](/docs/v2/models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

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
         "88e2a515"
    ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String[] | 관심 영역 ID | O |


<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message" : ""
}
// REQUEST_TIMTOUT
{
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "code": 503,
    "message": ""
}
// NOT_FOUND_ROI_ID
{
    "code": 504,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| code | Integer | 응답 코드 (**[Error Code](/docs/v2/models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

### Drawing Type

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| None | Integer | 없음 | O |
| Polygon | Integer | 다각형 | O |
| Rect | Integer | 사각형 | O |
| Line | Integer | 라인 | O |
| MultiLine | Integer | 멀티 라인 | O |
| All | Integer | 전체 영역 | O |

<br>
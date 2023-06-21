##  메타데이터 조회를 위한 API입니다. 

----

<br><br>

# 메타데이터 조회하기

<br>

### Request
```
POST /v2/va/metadata

{
    "nodeId": "813ee7995af2e8cd",
    "channelIds": ["cce679532768e7c5"],
    "eventTypes": [
      "AllDetect","Loitering","Intrusion","Falldown","Violence",
      "IllegalParking","AbnormalObjectCount","Longstay","LineEnter","LineCrossing","Direction","LeftTurn","RightTurn","UTurn",
      "Smoke","Flame","MatchingFace","NotWearingMask","NoHelmet","TrafficActuatedSignal","NonDetectionArea"
    ],
    "progressFilter": [0],
    "classIdFilter": [
        0,100,102,103,104,105,106,107,108,109,110,111,112,300,200,201,4,5
    ],
    "startTime": "2023-06-09T17:42:34",
    "endTime": "2023-06-09T17:42:35",
    "includeThumbnail": true
}
```


| Name | Type | Description | Required |
| :---- | :---- |:---- | :----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelIds | String[] | 채널 ID | O |
| eventTypes | String[] | 해당 이벤트 타입 조회 (**[EventType](models.md#eventtype)**) | O |
| progressFilter | Integer[] | 진행 필터 (**[Progress](#progress)**) | O |
| classIdFilter | Integer[] | 해당 classId 조회 (**[ClassId](models.md#classid)**) | O |
| startTime | String | 영상 재생 시작시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| endTime | String | 영상 재생 끝나는시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| includeThumbnail | bool | 썸네일 조회 여부 | O |


<br>

### Response
```
// SUCCESS
{
    "code": 0
    "message": "SUCCESS"
    "objectMetas" : {
        "CameraName" : "NEXTK Channel",
        "CameraUID" : "9cea1c46176b8262",
        "EventList" : [],
        "FrameHeight" : 1920,
        "FrameNumber" : 9254,
        "FrameWidth" : 1080,
        ...
    }
}
// NOT_FOUND_CHANNEL_UID
{
   "code": 505,
   "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----: |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| objectMetas | JsonObject[] | 메타 데이터 (**[ObjectMeta](va_results.md#objectmeta)**) | O |
| message | String | 오류 메시지 | X |

<br>

# 메타데이터 타임리스트 조회
각 메타데이터의 이벤트 발생 시점을 조회합니다.

<br>

### Request
```
POST /v2/va/metadata-timelist

{
    "nodeId": "813ee7995af2e8cd",
    "channelIds": ["cce679532768e7c5"],
    "eventTypes": [
        "AllDetect","Loitering","Intrusion","Falldown","Violence",
        "IllegalParking","AbnormalObjectCount","Longstay","LineEnter","LineCrossing","Direction","LeftTurn","RightTurn","UTurn",
        "Smoke","Flame","MatchingFace","NotWearingMask","NoHelmet","TrafficActuatedSignal","NonDetectionArea"
    ],
    "progressFilter": [0],
    "classIdFilter": [
        0,100,102,103,104,105,106,107,108,109,110,111,112,300,200,201,4,5
    ],
    "startTime": "2023-06-09T17:42:34",
    "endTime": "2023-06-09T17:42:35"
}
```


| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelIds | String[] | 채널 ID | O |
| eventTypes | String[] | 해당 이벤트 타입 조회 (**[EventType](models.md#eventtype)**) | O |
| progressFilter | Integer[] | 진행 필터 (**[Progress](#progress)**) | O |
| classIdFilter | Integer[] | 해당 classId 조회 (**[ClassId](models.md#classid)**) | O |
| startTime | String | 영상 재생 시작시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| endTime | String | 영상 재생 끝나는시간 (startTime ~ endTime 범위안의 영상 재생)| O |


<br>

### Response
```
// SUCCESS
{
  "code": 0,
  "message": "SUCCESS",
  "timeList": [
    2023-06-09 오후 2:47:24,
    2023-06-09 오후 2:47:25,
    2023-06-09 오후 2:47:26,
    2023-06-09 오후 2:47:30
  ]
}
// NOT_FOUND_CHANNEL_UID
{
   "code": 505,
   "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| timeList | DateTime[] | 타임 리스트 | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

# 영상, 메타데이터 기록 정보 조회
저장되 있는 영상 정보와 메타데이터 정보가 어떤날 저장됬는지 확인합니다.

<br>

### Request
```
POST /v2/va/record-days

{
    "nodeId": "53ba9bc997c72840"
}
```


| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |


<br>

### Response
```
// SUCCESS
{
    "mediaRecord": {
        "2e81e3a62c7c207f": ['2023-6-20'], 
        "9aa73a8450ad7eff": ['2023-6-21']
    }
    "metaRecord": {
        "2e81e3a62c7c207f": ["2023-6-13","2023-6-14","2023-6-15","2023-6-16"],
        "9aa73a8450ad7eff": ['2023-6-21']
    }
}
// REQUEST_TIMTOUT
{
   "code": 502,
   "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| mediaRecord | JsonObject[] | 영상 저장 날짜 | O |
| metaRecord | JsonObject[] | 메타데이터 저장 날짜 | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

### progress

<br>

| Enum | Description |
| :---- | :---- |
| Begin | 진입 |
| Continue | 진행 |
| End | 종료 |
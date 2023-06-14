---
layout: default
title: 서치
nav_order: 6
parent: v2
has_children: false
# permalink: /docs/v2
---


메타데이터 조회를 위한 API입니다. 

----

<br><br>

# 메타데이터 조회하기
메타데이터 조회하기

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
    "includeThumbnail": true,
}
```


| Name | Type | Description | Required |
| :---- | :---- |:---- | : ---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelIds | String[] | 채널 ID | O |
| eventTypes | String[] | 조회할 데이터의 이벤트 타입 | O |
| progressFilter | String[] | 조회할 데이터의 이벤트 타입 | O |
| classIdFilter | String[] | 조회할 데이터의 이벤트 타입 | O |
| startTime | String | 영상 재생 시작시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| endTime | String | 영상 재생 끝나는시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| includeThumbnail | bool | 썸네일 조회 여부 | O |


<br>

### Response
```
// Ok
{
  "code": 0
}

// Fail
{
   "code": 505,
   "message" : "Not Found Channel Uid"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

# 메타데이터 타임리스트 조회

메타데이터의 타임리스트를 조회합니다.

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
    "endTime": "2023-06-09T17:42:35",
}
```


| Name | Type | Description | Required |
| :---- | :---- |:---- |: --- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelIds | String[] | 채널 ID | O |
| eventTypes | String[] | 조회할 데이터의 이벤트 타입 | O |
| progressFilter | String[] | 조회할 데이터의 이벤트 타입 | O |
| classIdFilter | String[] | 조회할 데이터의 이벤트 타입 | O |
| startTime | String | 영상 재생 시작시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| endTime | String | 영상 재생 끝나는시간 (startTime ~ endTime 범위안의 영상 재생)| O |


<br>

### Response
```
// Ok
{
  "code": 0,
  "timeList": [
    {2023-06-09 오후 2:47:24},
    {2023-06-09 오후 2:47:25},
    {2023-06-09 오후 2:47:26},
    {2023-06-09 오후 2:47:30} ...
  ]
}

// Fail
{
   "code": 505,
   "message" : "Not Found Channel Uid"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| timeList | DateTime[] | 타임 리스트 |

<br>
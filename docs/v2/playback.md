---
layout: default
title: 플레이백
nav_order: 6
parent: v2
has_children: false
# permalink: /docs/v2
---


playback에 대한 API입니다. 

----

<br><br>

# 영상 불러오기

원하는 시간대의 영상을 불러옵니다.

<br>

### Request
```
POST /v2/va/playback

{
    "nodeId": "813ee7995af2e8cd",
    "channelId": "d08eae12e807e0db",
    "startTime": "2023-06-09T00:00:00",
    "endTime": "2023-06-09T23:59:59",
    "includeMeta": false,
    "protocol": 0
}
```


| Name | Type | Description | Required |
| :---- | :---- |:---- | O |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| startTime | String | 영상 재생 시작시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| endTime | String | 영상 재생 끝나는시간 (startTime ~ endTime 범위안의 영상 재생)| O |
| includeMeta | bool | 메타 데이터 포함 여부 | O |
| protocol | Integer | --- | O |

<br>


# 성공
{
    "code" : 0,
    "mediaUrl": "rtsp://192.168.0.98:8554/playback/8ca28b54ec156338",
    "metaUrl": ""
}
```
| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| mediaUrl | String | 영상 저장 URL |
| metaUrl | String | --- |

<br>
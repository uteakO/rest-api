---
layout: default
title: 영상 분석 상태제어
nav_order: 3
parent: 영상 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/va_command
---

# 영상 분석 제어

이 API를 이용하여 지정 채널에 대해 영상 분석을 시작하거나 중지할 수 있습니다.

또한 영상 분석 중 누적 된 데이터들을 초기화 할 수 있습니다. 예를 들어, ROI 영역의 검출객체 누적 카운팅 값을 초기화 할 수 있습니다.

------------------------


<!-- 이 API를 이용하여 지정 채널에 대해 비디오 분석을 시작하거나 중지할 수 있습니다.
또한, ROI 영역의 검출객체 카운팅 상태들을 초기화할 수 있습니다. -->
# 분석 제어

영상 분석할 컴퓨팅 노드와 채널 리스트를 설정하여 분석 시작/중지/재시작 기능을 제공

#### Request

```
POST /v2/va/control

# VA_START
{
    "nodeId":"a46147f4",
    "channelIds": ["19fa5688"],
    "operation": "VA_START"
}

# VA_STOP
{
    "nodeId":"a46147f4",
    "channelIds": ["19fa5688"],
    "operation": "VA_STOP"
}

# VA_RST
{
    "nodeId":"a46147f4",
    "channelIds" : ["X1ashF0t"],
    "operation" : "VA_RST",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelIds | String[] | 채널 ID 리스트 | O |
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
{
  "code": 0
}
//Fail
{
    "code" : 0,
    "message" : "reason"
}

```

| Name | Type | Description |
| :---- | :---- |:---- |
| sourceIp | String | Channel GRPC IP |
| sourcePort | Integer | Channel GRPC Port |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>
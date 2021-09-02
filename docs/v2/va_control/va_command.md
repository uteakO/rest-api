---
layout: default
title: 비디오 분석 상태제어
nav_order: 4
parent: 비디오 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/va_command
---

이 API를 이용하여 지정 채널에 대해 비디오 분석을 시작하거나 중지할 수 있습니다.

또한 비디오 분석 중 누적 된 데이터들을 초기화 할 수 있습니다. 예를 들어, ROI 영역의 검출객체 누적 카운팅 값을 초기화 할 수 있습니다.

------------------------

# 비디오 분석 제어

지정 채널에 대한 분석 제어명령을 전달합니다.

```
POST /v2/va/control 
```
<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| operation | Enum | 제어 명령 (**[Operations](../models.md#operations)**) | O |
| parameter | String[] | 필요시 파라미터 전달 | X |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| sourceIp | String | Channel GRPC IP |
| sourcePort | Integer | Channel GRPC Port |
| code | Integer | 오류 코드 (**[Error Code](../models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

### Remarks

VA_START를 하기 위해서는 ROI가 먼저 생성 되어있어야 합니다.

### JSON Sample
#### Request

```
POST /v2/va/control

# VA_START
{
    "channelId" : "X1ashF0t",
    "operation" : "VA_START",
}

# VA_STOP
{
    "channelId" : "X1ashF0t",
    "operation" : "VA_STOP",
}

# VA_RST
{
    "channelId" : "X1ashF0t",
    "operation" : "VA_RST",
    "parameter" : ["roiId1", "roiId2", "roiId3"]
}
```

#### Response

```
## 성공
# VA_START
{
    "sourceIp" : "192.168.0.30",
    "sourcePort" : 40400
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

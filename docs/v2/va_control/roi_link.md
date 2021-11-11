---
layout: default
title: ROI Link
nav_order: 4
parent: 영상 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/roi_link
---

# Link

여러 개의 ROI를 조합하여 이벤트를 정의할 때 사용 하는 API입니다.

------------------------

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
연동 정보를 조회합니다.

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
채널 내 Roi 연동 리스트를 조회합니다.

<br>

### Request
```
POST /v2/va/list-link
{
    "nodeId": "c6a45bc6",
    "channelId": "b501189c"
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
Roi 연동 설정을 수정합니다.

### Request
```
POST /v2/va/update-link

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
| name | String | 연계 이벤트 이름 | X |
| roiLink | JsonObject[] | 연계 영역 설정 ([Link](#link)) | X |


<br>

### Response
```
{
    "code" : 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

# Roi Link 삭제
ROI 연동 설정을 삭제합니다.

### Request
```
POST /v2/va/remove-link
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
| linkId | String[] | 연계 이벤트 ID 리스트 | O |


<br>

### Response
```
{
   "code" : 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>
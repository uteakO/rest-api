---
layout: default
title: ROI Link
nav_order: 3
parent: 비디오 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/roi_link
---



여러 개의 ROI를 조합하여 이벤트를 정의할 때 사용 하는 API입니다.

------------------------

# ROI Link 생성
영역 간의 이벤트 연계 기능을 추가할수 있습니다.
```
POST /v2/va/create-link
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| name | String | 연계 이벤트 이름 | O |
| roiLink | JsonObject[] | 연계 영역 설정 ([Link](#link)) | O |

### Link

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiId | String | ROI ID | O |
| nextRoiRealDistance | Integer | 다음 영역까지 실제 거리 | X |
| nextRoiArrivalWaitingTime | Integer | 다음 영역까지 도착 대기 시간 | X |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| linkId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](../models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

----------------

### JSON Sample
#### Request

```
{
    "channelId" : "X1ashF0t",
    "name" : "CustomEvent", //연계 이벤트 이름
    "roiLink" : 
    [
        {
            "roiId": "Gd2da1",
            "nextRoiRealDistance" : 50,
            "nextRoiArrivalWaitingTime" : 5
        },
        {
            "roiId": "A23vds",
        }
    ]
}
```

#### Response

```
#성공
{
    "linkId" : "Bd2fha8"
    "code" : 0
}
#실패
{
    "code" : 300,
    "message" : "fail"
}
```
<br><br>

# ROI Link 조회
ROI를 조회합니다.
```
POST /v2/va/get-link
```
<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| linkId | String | 연계 이벤트 ID | O |

<br>

### Response

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| linkId | String | 연계 이벤트 ID | O |
| name | String | 연계 이벤트 이름 | O |
| roiLink | JsonObject[] | 연계 영역 설정 ([Link](#link)) | O |

<br>

<!--| shape | [RoiShape](#roishape) | ROI 형태 |-->
### JSON Sample

#### Request
```
POST /v2/va/get-roi

{
    "channelId" : "X1ashF0t",
     "linkId":"Bd2fha8"
}
```

#### Response
```
# 성공
{
    "linkId":"Bd2fha8",
    "name" : "CustomEvent",
    "roiLink" : 
    [
        {
            "roiId": 0,
            "nextRoiRealDistance" : 50,
            "nextRoiArrivalWaitingTime" : 5
        },
        {
            "roiId": 1,
        }
    ],
    "code" : 0
}

# 실패
{
    "code" : 300
    "message" : "fail"
}
```

<br><br>

# 채널 내 Roi Link 조회
ROI 설정을 조회합니다.
```
POST /v2/va/list-link
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](../models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

### JSON Sample
#### Request

```
POST /v2/va/list-link

{
    "channelId" : "X1ashF0t",
    "linkList" : [
        {
            "linkId":"Bd2fha8",
            "name" : "CustomEvent",
            "roiLink" : 
            [
                {
                    "roiId": 0,
                    "nextRoiRealDistance" : 50,
                    "nextRoiArrivalWaitingTime" : 5
                },
                {
                    "roiId": 1,
                }
        ]},
        {
            "linkId":"Bd2fha8",
            "name" : "CustomEvent2",
            "roiLink" : 
            [
                {
                    "roiId": 1,
                    "nextRoiRealDistance" : 50,
                    "nextRoiArrivalWaitingTime" : 5
                },
                {
                    "roiId": 0,
                }
        ]}
    ]
}
```

#### Response

```
# 성공
{
    "code" : 0
}

# 실패
{
    "code" : 300
    "message" : "fail"
}
```


<br><br>

# Roi Link 수정
ROI 설정을 수정합니다.
```
POST /v2/va/update-link
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| linkId | String | 연계 이벤트 ID | O |
| name | String | 연계 이벤트 이름 | X |
| roiLink | JsonObject[] | 연계 영역 설정 ([Link](#link)) | X |


<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](../models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### JSON Sample
#### Request
```
POST /v2/va/remove-roi

{
    "channelId" : "X1ashF0t",
    "linkId" : "Bd2fha8",
    "name" : "CustomEvent", //연계 이벤트 이름
    "roiLink" : 
    [
        {
            "roiId": "Gd2da1",
            "nextRoiRealDistance" : 50,
            "nextRoiArrivalWaitingTime" : 5
        },
        {
            "roiId": "A23vds",
        }
    ]
}
```

#### Response
```
# 성공
{
    "code" : 0
}

# 실패
{
    "code" : 300
    "message" : "fail"
}
```

<br><br>

# Roi Link 삭제
ROI 설정을 삭제합니다.
```
POST /v2/va/remove-link
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| linkId | String[] | 연계 이벤트 ID 리스트 | O |


<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](../models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### JSON Sample
#### Request
```
POST /v2/va/remove-roi

{
    "channelId" : "X1ashF0t",
    "linkId" : ["A23vds"]
}
```

#### Response
```
# 성공
{
    "code" : 0
}

# 실패
{
    "code" : 300
    "message" : "fail"
}
```

<br><br>

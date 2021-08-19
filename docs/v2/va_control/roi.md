---
layout: default
title: ROI
nav_order: 2
parent: 비디오 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/roi
---


영상 내 ROI(Region of interest) 설정 API입니다.

------------------------

# ROI 생성
지정한 채널에 관심 영역을 정의하고, 관심 영역 내 분석 알고리즘을 설정합니다.
(다각형 영역만을 지원)
```
POST /v2/va/create-roi
```
<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| roiName | String | 이벤트 이름 | O |
| description | String | 관심 영역 설명 | X |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| feature | Enum | 영역 속성(**[RoiFeature](#roi-feature)**) | O |
| roiDots | JsonObject[] | ROI를 구성하는 점들(**[RoiDot](#roi-dot)**) | O |

<br/>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 (**[Error Code](../models.md#error-code)**) |
| message | String | 오류 메시지 |

<br/>

### Roi Dot

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| X | Integer | X 좌표 | O |
| Y | Integer | Y 좌표 | O |
| lineUntilNextDot | JsonObject[] | 검출 객체(**[RoiLine](#roi-line)**) | O |

<br/>

### Roi Line

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| disable | boolean | 비활성화 | O |
| direction | String | 방향 설정 | O |
| target | Enum[] | 검출 객체(**[ObjectType](#object-type)**) | O |

<br/>

### JSON Sample

#### Request
<!-- 
    - 무조건 polygon 형태 유지.
    - 영역 이벤트는 어떻게 처리할 것인가... 
      (혼잡도 레벨, 정지)
-->
```
{
    "channelId" : "X1ashF0t",
    "roiName" : "event_accident_roon",
    "description" : "accident in conference room",
    "stayTime" : 5,  
    "numberOf" : 1,  
    "feature" : true, 
    "roiDots" : 
    [
        {
           "X" : 0,
           "y" : 0,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human","Vehicle"]
           }
        },
        {
           "X" : 0.85,
           "y" : 0,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human"]
           }
        },
        {
           "X" : 1,
           "y" : 0.9,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Vehicle"]
           }
        },
        {
           "X" : 0,
           "y" : 0.96,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human","Vehicle"]
           }
        }
    ]
}
```
<br>


#### Response

```
#성공
{
    "roiId" : "Vif7f02j"
    "code" : 0
}
#실패
{
    "code" : 300,
    "message" : "fail"
}
```

<br><br>


# ROI 조회
ROI를 조회합니다.
```
POST /v2/va/get-roi
```
<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiId | String | 관심 영역 ID | O |

<br>

### Response

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiName | String | 이벤트 이름 | O |
| description | String | 관심 영역 설명 | O |
| stayTime | Integer | 발생 지연 시간 | O |
| numberOf | Integer | 최소 발생 객체수 조건 | O |
| feature | Enum | 영역 속성(**[RoiFeature](#roi-feature)**) | O |
| roiDots | JsonObject[] | ROI를 구성하는 점들(**[RoiDot](#roi-dot)**) | O |

<br>

<!--| shape | [RoiShape](#roishape) | ROI 형태 |-->
### JSON Sample

#### Request
```
POST /v2/va/get-roi

{
    "channelId" : "X1ashF0t",
    "roiId" : "Vif7f02j"
}
```

#### Response
```
# 성공
{
    "roiName" : "event_accident_room",
    "description" : "accident in conference room",
    "stayTime" : 5,  
    "numberOf" : 1,  
    "feature" : true, 
    "roiDots" : 
    [
        {
           "X" : 0,
           "y" : 0,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human","Vehicle"]
           }
        },
        {
           "X" : 0.85,
           "y" : 0,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human"]
           }
        },
        {
           "X" : 1,
           "y" : 0.9,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Vehicle"]
           }
        },
        {
           "X" : 0,
           "y" : 0.96,
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human","Vehicle"]
           }
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

# 채널 내 ROI 목록 조회
지정한 채널에 추가 된 모든 ROI들을 조회합니다.
```
POST /v2/va/list-roi
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response

**[ROI 조회](#roi-조회)** 응답의 배열입니다.

<br>

### JSON Sample
#### Request
```
POST /v2/va/get-roi

{
    "channelId" : "X1ashF0t",
}
```

#### Response
```
# 성공
{
    "roiList": [{
        "roiName" : "event_accident_roon",
        "description" : "accident in conference room",
        "stayTime" : 5,  
        "numberOf" : 1,  
        "feature" : true, 
        "roiDots" : 
        [{
               "X" : 0,
               "y" : 0,
               "lineUntilNextDot" : 
               {
                    "disable" : false,
                    "direction" : "enter",
                    "target" : ["Human","Vehicle"]
                }
            },
            {
                "X" : 0.85,
                "y" : 0,
                "lineUntilNextDot" : 
                {
                    "disable" : false,
                    "direction" : "enter",
                    "target" : ["Human"]
                }
            },
            {
                "X" : 1,
                "y" : 0.9,
                "lineUntilNextDot" : 
                {
                    "disable" : false,
                    "direction" : "enter",
                    "target" : ["Vehicle"]
                }
            },
            {
                "X" : 0,
                "y" : 0.96,
                "lineUntilNextDot" : 
                {
                    "disable" : false,
                    "direction" : "enter",
                    "target" : ["Human","Vehicle"]
                }
            }
        ]}
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

# ROI 수정
ROI 설정을 수정합니다.
```
POST /v2/va/update-roi
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |
| roiName | String | 이벤트 이름 | X |
| description | String | 관심 영역 설명 | X |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| feature | Enum | 영역 속성(**[RoiFeature](#roi-feature)**) | X |
| roiDots | JsonObject[] | ROI를 구성하는 점들(**[RoiDot](#roi-dot)**) | X |



<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](../models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

### JSON Sample
#### Request
```
POST /v2/va/update-roi

{
    "channelId" : "X1ashF0t",
    "roiId" : "Vif7f02j",
    "roiName" : "event_accident_roon",
    "description" : "accident in conference room",
    "stayTime" : 5,  
    "numberOf" : 1,  
    "feature" : true, 
    "roiLines" : [
        {
           "lineId" : "Vif7f02j_0",
           "startPoint" : [0,0],
           "endPoint" : [0,0],
           "lineUntilNextDot" : 
           {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Vehicle"]
            }
        },
        {
           "lineId" : "Vif7f02j_1",
           "startPoint" : [0,0],
           "endPoint" : [0,0],
           "lineUntilNextDot" : 
            {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Vehicle"]
            }
        },
        {
           "lineId" : "Vif7f02j_2",
           "startPoint" : [0,0],
           "endPoint" : [0,0],
           "lineUntilNextDot" : 
           {
               "disable" : false,
               "direction" : "enter",
               "target" : ["Vehicle"]
           }
        },
        {
           "lineId" : "Vif7f02j_3",
           "startPoint" : [0,0],
           "endPoint" : [0,0],
           "lineUntilNextDot" : 
            {
                "disable" : false,
                "direction" : "enter",
                "target" : ["Human","Vehicle"]
            }
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

# ROI 삭제
ROI 설정을 삭제합니다.
```
POST /v2/va/remove-roi
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| roiId | String[] | 관심 영역 ID 리스트 | O |


<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](../models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

### Remarks
링크되어있는 ROI는 VA를 중지 후 삭제 해야합니다.

<br><br>

### JSON Sample

#### Request

```
POST /v2/va/remove-roi

{
    "channelId" : "X1ashF0t",
    "roiId" : ["Vif7f02j"]
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
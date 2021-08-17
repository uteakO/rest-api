---
layout: default
title: 비디오 분석 설정
nav_order: 4
parent: v2
has_children: false
# permalink: /docs/v2
---


비디오 분석 설정에 대한 API입니다.

__목차__
- [ROI 생성](#roi-생성)
- [ROI 조회](#roi-조회)
- [채널 내 ROI 목록 조회](#채널-내-roi-목록-조회)
- [ROI 수정](#roi-수정)
- [ROI 삭제](#roi-삭제)
- [비디오 분석 제어](#비디오-분석-제어)
- [이벤트 목록 조회](#이벤트-목록-조회)

------------------------

# ROI 설정

ROI(Region of interest; 관심영역)은 비디오 분석을 실행할 화면 내 영역이며, 분석 종류에 따라 선 또는 폴리곤 형태가 필요합니다. ( 이벤트별 ROI 설정 방법 참조 )

한 개 채널에 여러 개의 ROI가 존재할 수 있습니다.

<br>

## ROI 생성
지정한 채널에 대해 관심 영역을 정의하고, 관심 영역 내 분석 알고리즘을 설정합니다.
```
POST /v2/va/create-roi
```

<br>

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| description | String | 관심 영역 설명 | X |
| roiDots | Double[] | 관심 영역 좌표 | O |
| detectorInfos | JsonObject[] | 검출 객체 정보 리스트 ([DetectorInfo](#detecter-info)) | O |

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Detecter Info
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| model | String | 검출 모델 버전 (default: lastest) | X |
| type | String | 검출 객체 종류  ([ObjectType](#object-type)) | O |
| confidence | Double | 객체 유사도 (default: > 0) ~ 1 | X |

<br>

### Remarks
검출하고자 하는 객체의 ROI를 설정합니다. 그외 자세한 설명...필요..

<br>

#### Sample
```
POST /v2/va/create-roi

{
    "channelId": "X1ashF0t",
    "description": "Loitering and intrusion detection for CCTV #3",
    "roiDots": [0.2, 0.2, 0, 0.5, 0.7, 0.1],
    "detectorInfos" : [{
        "model": "human/lastest",
        "type" : "PERSON",
        "confidence", "0.6"
    },
    {
        "model": "fire/lastest",
        "type" : "FIRE",
        "confidence", "0.2"
    }]
}
```
<br>


#### Sample
```
# 성공
{
    "roiId": "Vif7f02j",
    "code" : 0
}

# 실패
{
    "code" : 300,
    "message" : "fail"
}
```

<br><br>

## ROI 조회
ROI를 조회합니다.
```
POST /v2/va/get-roi
```
<br>

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| description | String | 관심 영역 설명 |
| roiDots | Double[] | 관심 영역 좌표 |
| detectorInfos | JsonObject[] | 검출 객체 정보 리스트 ([DetectorInfo](#detecter-info)) | O |

<br>

<!--| shape | [RoiShape](#roishape) | ROI 형태 |-->
### Sample

#### Requset
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
    "description" : "Loitering and intrusion detection for CCTV #3",
    "roiDots" : [0.2, 0.2, 0, 0.5, 0.7, 0.1],
    "detectorInfos" : [{
        "model": "human/lastest",
        "type" : "PERSON",
        "confidence", "0.6"
    },
    {
        "model": "fire/lastest",
        "type" : "FIRE",
        "confidence", "0.2"
    }],
    "code" : 0
}

# 실패
{
    "code" : 300
    "message" : "fail"
}
```

<br><br>

## 채널 내 ROI 목록 조회
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

[ROI 조회](roi-조회) 응답의 배열입니다.

<br>

### Sample
#### Requset
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
            "description" : "Loitering and intrusion detection for CCTV #3",
            "roiDots" : [0.2, 0.2, 0, 0.5, 0.7, 0.1],
            "detectorInfos" : [{
                "model": "human/lastest",
                "type" : "PERSON",
                "confidence", "0.6"
            },
            {
                "model": "fire/lastest",
                "type" : "FIRE",
                "confidence", "0.2"
            }]
        },
        {
            "description" : "Loitering and intrusion detection for CCTV #2",
            "roiDots" : [0.2, 0.2, 0, 0.5, 0.7, 0.1],
            "detectorInfos" : [{
                "model": "human/lastest",
                "type" : "PERSON",
                "confidence", "0.6"
            },
            {
                "model": "fire/lastest",
                "type" : "FIRE",
                "confidence", "0.2"
            }
            ]
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

## ROI 수정
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
| description | String | 관심 영역 설명 | X |
| roiDots | Double[] | 관심 영역 좌표 | X |
| detectorInfos | JsonObject[] | 검출 객체 정보 리스트 ([DetectorInfo](#detecter-info)) | X |



<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Sample
#### Requset
```
POST /v2/va/update-roi

{
    "channelId" : "X1ashF0t",
    "roiId" : "Vif7f02j",
    "description" : "Loitering and intrusion detection for CCTV #3",
    "roiDots" : [0.2, 0.2, 0, 0.5, 0.7, 0.1],
    "detectorInfos" : [{
        "model": "human/lastest",
        "type" : "PERSON",
        "confidence", "0.6"
    },
    {
        "model": "fire/lastest",
        "type" : "FIRE",
        "confidence", "0.2"
    }]
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

## ROI 삭제
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
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Remarks
링크되어있는 ROI는 VA를 중지 후 삭제 해야합니다.

<br><br>

### Sample
#### Requset
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


# 비디오 분석 제어
이 API를 이용하여 지정 채널에 대해 비디오 분석을 시작하거나 중지할 수 있습니다.
또한, ROI 영역의 검출객체 카운팅 상태들을 초기화할 수 있습니다.
```
POST /v2/va/control 
```
<br>


<!-- control 네이밍 변경하는게 좋지 않을까요.. 무엇??-->
### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| operation | String | 제어 명령 ([Operations](models#enum-operations)) | O |
| analysisConfig | JsonObject | 제어에 필요한 파라미터 ([AnalysisConfig](#analysis-config)) | O |
| parameter | String[] | 필요시 파라미터 전달 | O |

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| sourceIp | String | Channel GRPC IP |
| sourcePort | Integer | Channel GRPC Port |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

#### Remarks
parameter는 Reset에서 사용되는 ROI 리스트 등 그외에도 사용될 수 있으며, 추후 확장성을 위함..
VA_START를 하기 위해서는 ROI가 먼저 생성 되어있어야함.

### Sample
#### Requset
```
POST /v2/va/control

# VA_START
{
    "channelId" : "X1ashF0t",
    "operation" : "VA_START",
    "analysisConfig" : {
        "eventName" : "Loitering",      // 이벤트 이름
        "direction" : ["LEFT", "TOP"],  // 어느 방향으로 객체가 들어오는 지 ?(LEFF, TOP) 
        "io" : "IN2OUT",                // IN2OUT, OUT2IN, ANYWHERE
        "maintenanceSec" : "1",            // 객체가 ROI내에 해당 시간동안 ~
        "activity" : "INACTIVITY",      // ACTIVITY, INACTIVITY
        "howMany" : "1",                // ROI내에 이벤트 발생의 최소 객체 수
        "roiLink" : {
            "link": ["roi 1","roi 2"],
            "delay" : "4s",             // 4초 내로 roi를 지나가야함
            "distanceMeter" : "100"     // ROI 간의 실제 거리
        } ,
        // ROI내에 객체가 들어올떄의 기준점
        "referencePoint" : "LeftTop" // ALL, LEFT_TOP, RIGHT_BOTTOM, CENTER, ANYWHERE
    }
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
    "sourcePort" : "40400"
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


# 이벤트 목록 조회
동작중인 이벤트 목록을 조회합니다.
```
POST /v2/va/list-event 
```

<br>

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
<!-- | analysisConfig |  | 제어에 필요한 파라미터 ([AnalysisConfig](#analysis-config)) | O | -->

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>


----------------

### Sample
#### Requset
```
POST /v2/va/list-event 

{
    "channelId": "X1ashF0t",
   
}
```

<br>

#### Response
```
# 성공
{
    "analysisConfigs" : [{
        "eventName" : "Loitering",      // 이벤트 이름
        "direction" : ["LEFT", "TOP"],  // 어느 방향으로 객체가 들어오는 지 ?(LEFF, TOP) 
        "io" : "IN2OUT",                // IN2OUT, OUT2IN, ANYWHERE
        "maintenanceSec" : "1",            // 객체가 ROI내에 해당 시간동안 ~
        "activity" : "INACTIVITY",      // ACTIVITY, INACTIVITY
        "howMany" : "1",                // ROI내에 이벤트 발생의 최소 객체 수
        "roiLink" : {
            "link": ["roi 1","roi 2"],
            "delay" : "4s",             // 4초 내로 roi를 지나가야함
            "distanceMeter" : "100"     // ROI 간의 실제 거리
        } ,
        // ROI내에 객체가 들어올떄의 기준점
        "referencePoint" : "LeftTop" // ALL, LEFT_TOP, RIGHT_BOTTOM, CENTER, ANYWHERE
    },{
        "eventName" : "Loitering",      // 이벤트 이름
        "direction" : ["LEFT", "TOP"],  // 어느 방향으로 객체가 들어오는 지 ?(LEFF, TOP) 
        "io" : "IN2OUT",                // IN2OUT, OUT2IN, ANYWHERE
        "maintenanceSec" : "1",            // 객체가 ROI내에 해당 시간동안 ~
        "activity" : "INACTIVITY",      // ACTIVITY, INACTIVITY
        "howMany" : "1",                // ROI내에 이벤트 발생의 최소 객체 수
        "roiLink" : {
            "link": ["roi 1","roi 2"],
            "delay" : "4s",             // 4초 내로 roi를 지나가야함
            "distanceMeter" : "100"     // ROI 간의 실제 거리
        } ,
        // ROI내에 객체가 들어올떄의 기준점
        "referencePoint" : "LeftTop" // ALL, LEFT_TOP, RIGHT_BOTTOM, CENTER, ANYWHERE
    }],
    "code" : 0
}


# 실패
{
    "code" : 300,
    "message" : "fail"
}
```


<br><br>

## 일반 분석 설정

### Remarks
분석 시작할때 넘겨줘야하는 설정 객체
<!-- 일반적으로 사용되는 이벤트들에 대해서 Sample json 만들어줘야함 -->

<br><br>

### Analysis Config
```
{
    "eventName" : "Loitering",      // 이벤트 이름
    "direction" : ["LEFT", "TOP"],  // 어느 방향으로 객체가 들어오는 지 ?(LEFF, TOP) 
    "io" : "IN2OUT",                // IN2OUT, OUT2IN, ANYWHERE
    "maintenanceSec" : "1",            // 객체가 ROI내에 해당 시간동안 ~
    "activity" : "INACTIVITY",      // ACTIVITY, INACTIVITY
    "howMany" : "1",                // ROI내에 이벤트 발생의 최소 객체 수
    "roiLink" : {
        "link": ["roi 1","roi 2"],
        "delay" : "4s",             // 4초 내로 roi를 지나가야함
        "distanceMeter" : "100"     // ROI 간의 실제 거리
    } ,
    // ROI내에 객체가 들어올떄의 기준점
    "referencePoint" : "LeftTop" // ALL, LEFT_TOP, RIGHT_BOTTOM, CENTER, ANYWHERE
}
```

<br><br>

  
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



<!-- 이벤트 종류
 # Polygon ROI
 이벤트 ( 이벤트 발생 조건 )

 배회, 주정차 (ROI 내에 x초동안 머문 객체) (파라미터: 객체가 움직이냐?, roi 내 몇초동안)
 침입 (ROI 외부에서 내부로 들어온 객체) (파라미터: 객체가 roi 내 몇초동안)
 혼잡도 (ROI 내에 x초 동안 머문 객체) (파라미터: 객체가 얼마나 많은가 )
 신호 기다림
 정렬,
 스피드 게이트


# Line ROI 였으나 Polygon으로 대체 가능
 - 유턴, 좌회전, 우회전, 직진, (Line ROI에서 Line ROI 건너감) (파라미터: 몇초내로 건너가야 하는가?)
   속도, (Line ROI에서 Line ROI로 건너감) (파라미터: 실제 거리,)
 - 라인 크로싱 (딱히 구현 할 필요가 있을까?? Client측에서 조합 해도 될듯?) //
 - 역침입 (TNM 사용): polygon을 그리고 객체가 나갈때 이벤트 발생, 어느 방향으로 나갈때??


 -->


<!-- 사용자가 이벤트를 임의대로 지정할 수 있다면 ??
 ROI LINK 가능한 리스트 (이벤트의 개념을 사용자가 설정 할 수 있음)


이벤트 파라미터 설정:
 - ROI 입출에 따른 객체 기준점 (좌상단, 좌하단, 우상단, 우하단, 중심)
 - ROI 몇초 동안 유지 (가 되어야 이벤트 발생을 할것인가?)
 - ROI 몇개의 객채가 있어야 ?? (default 1 )
 - ROI 입출 방향성 (좌 우 상 하)
 - ROI 내 객체의 유동성
 - 

ROI LINK 불가능 한 이벤트 리스트 (그냥 하면됨.)
 싸움,
 유기,
 화재,
  -->





<!-- ### LoiteringConfig
영역 내 객체를 감지합니다.

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| AlramTime | Double | 발생 대기 시간 | O |
| ObjectTypes | [[ObjectType](#object-type)] | 검출 객체 종류 | X |


### IntrusionConfig
영역 외부에서 내부로 들어오는 객체를 감지합니다.

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| AlramTime | Double | 발생 대기 시간 | O |
| ObjectTypes | [[ObjectType](#object-type)] | 검출 객체 종류 | O |

### FalldownConfig
영역 내 쓰러진 사람을 감지합니다.

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| AlramTime | Double | 발생 대기 시간 | O |

### AbandonedConfig
영역 내 버려진 유기물을 감지합니다.
<br>
* 유기물 (가방, 쓰레기)

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| AlramTime | Double | 발생 대기 시간 | O |

### CongestionConfig
영역 내 혼잡도를 감지합니다.

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| ObjectTypes | [[ObjectType](#ObjectType)] | 검출 객체 종류 | O |
| MaxNumberOf | Integer | 객체 개수 제한 | X |
<!-- 혼잡도는 인원수에 따른 이벤트 & 영역 내 평균 값을 측정한 이벤트 두개 있음
     인원수 설정이 없을 경우 평균을 통한 레벨로 측정?-->
<!-- 
### LineCrossingConfig
라인을 통과하는 객체들을 카운팅합니다.
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| ObjectTypes | [[ObjectType](#ObjectType)] | 검출 객체 종류 | O |
| Direction | [Direction](#enum-Direction) | 방향 선택 | O |

### DoubleLineCrossingConfig
두 라인을 통과하는 객체들을 카운팅합니다.
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| ObjectTypes | [[ObjectType](#ObjectType)] | 검출 객체 종류 | O |

### SpeedConfig
두 라인을 통과하는 객체들을 카운팅합니다.
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| Distance | Integer | 두 라인 간 실제 거리 | O |
| ObjectTypes | [[ObjectType](#ObjectType)] | 검출 객체 종류 | O |

### StopConfig
영역 내 정지된 객체를 감지합니다.
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| AlramTime | Double | 발생 대기 시간 | O |
| ObjectTypes | [[ObjectType](#ObjectType)] | 검출 객체 종류 | O | -->

<!-- 아래 이벤트는 일단 보류-->
<!--
### DensityConfig
### SignalWaitingTimeConfig
### TrafficActivatedSignalConfig
### CrosswalkQueueingConfig
-->

<br><br>

<!-- 
#  Direction
| Enum | Description |
| :---- | :---- |
| ONE_WAY | 단방향 |
| TWO_WAY | 양방향 |
 -->
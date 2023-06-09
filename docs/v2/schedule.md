---
layout: default
title: 스케줄 관리
nav_order: 3
parent: v2
has_children: false
# permalink: /docs/v2
---


영상 내 Schedule Setting(영상 분석 시간 설정), Record Setting(영상, metadata 기록 시간 설정) API입니다.


----

# schedule 설정
지정한 시간과 요일에 영상 분석을 실시합니다.

<br>

### Request
```
POST /v2/va/va-schedule

{
  "nodeId": "3f16f31ecc13647d",
  "channelId": "5939a61ad39c0c37",
  "schedule": [
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23],
    [0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23]
  ],
  "except": [
    "01.01","03.01","05.05","06.06","08.15","10.03","10.09","12.25"
  ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| schedule | Integer[][] | 분석 요일, 시간 속성 | O |
| except | String[] | 분석 제외 날짜 | O |

<br>

### Response
```
// Ok
{
    "code": 0,
    "message" : ""
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

### Request
```
POST /v2/va/recording-schedule

{
  "nodeId": "3f16f31ecc13647d",
  "channelId": "5939a61ad39c0c37",
  "schedule": [
        [
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ],
        [   
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ],
        [
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ],
        [
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ],
        [
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ],
        [
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ],
        [
            {"time":0,"type":0},{"time":1,"type":0},{"time":2,"type":0},{"time":3,"type":0},{"time":4,"type":0},{"time":5,"type":0},
            {"time":6,"type":0},{"time":7,"type":0},{"time":8,"type":0},{"time":9,"type":0},{"time":10,"type":0},{"time":11,"type":0},
            {"time":12,"type":0},{"time":13,"type":0},{"time":14,"type":0},{"time":15,"type":0},{"time":16,"type":0},{"time":17,"type":0},
            {"time":18,"type":0},{"time":19,"type":0},{"time":20,"type":0},{"time":21,"type":0},{"time":22,"type":0},{"time":23,"type":0}
        ]
  ],
  "except": [
    "01.01","03.01","05.05","06.06","08.15","10.03","10.09","12.25"
  ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| schedule | JsonObject[][] | 레코딩 스케줄(**[Schedule](#schedule)**) | O |
| except | String[] | 레코드 제외 날짜 | O |

<br>

### Response
```
// Ok
{
    "code": 0,
    "message" : ""
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>


### Schedule

| Name | Type | Description |
| :---- | :---- |:---- |
| time | Integer | 레코드 시간 |
| type | Enum | 레코드 타입(**[RecordType](models.md#RecordType)**) |

<br>

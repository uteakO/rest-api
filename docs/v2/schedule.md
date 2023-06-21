

##  영상 내 Schedule Setting(영상 분석 시간 설정), Record Setting(영상, metadata 기록 시간 설정) API입니다.

--------
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
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| schedule | Integer[][] | 분석 요일(**List 일 ~ 토 모두 입력**), 분석 시간(**Integer 원하는 시간 입력**) | O |
| except | String[] | 분석 제외 날짜 | O |

<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message" : ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

# recording 설정
지정한 시간과 요일에 영상 및 메타데이터를 저장합니다.

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
| :---- | :---- |:---- |:----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| schedule | JsonObject[][] | 분석 요일(**List**), 분석 시간, 분석 타입 (**[Schedule](#schedule)**) | O |
| except | String[] | 레코드 제외 날짜 | O |

<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message" : ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----: |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>


### Schedule

| Name | Type | Description |
| :---- | :---- |:---- |
| time | Integer | 레코드 시간 |
| type | Integer | 레코드 타입 (**[RecordType](#recordtype)**) |

<br>

### RecordType

| Enum | Description |
| :---- | :---- |
| None | 저장 안함 |
| Video | 영상 저장 |
| Event | 메타데이터 저장 |
| VideoNEvent | 영상, 메타데이터 저장 |
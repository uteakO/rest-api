


## 시스템 로그를 조회하는 API입니다.
----

# 시스템 로그 조회
#### Request
```
POST /v2/system-log

{
    "nodeId" : "53ba9bc997c72840",
    "startTime" : "2023-06-21T00:00:00",
    "endTime" : "2023-06-21T23:59:59",
    "logType" : 127
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| nodeId | String | 컴퓨팅 노드 ID | O |
| startTime | String | 로그의 시작지점 시간 | O |
| endTime | String | 로그의 끝지점 시간 | O |
| logType | Integer | 로그 타입 (**[LogType](models.md#logtype)**) | O |

#### Response
```
// SECCESS
{
    "code": 0
    "message": "SUCCESS"
    "logs" : [
        {'content': 'Turn ACTIVATE_MEDIA_SERVER', 'dateTime': '2023-06-21 09:53:02.158,', 'logType': 1}, 
        {'content': 'Immediately Run ACTIVATE_MEDIA_SERVER', 'dateTime': '2023-06-21 09:53:02.159,', 'logType': 1}, 
        {'content': 'RtspServer Try Listen', 'dateTime': '2023-06-21 09:53:02.159,', 'logType': 1}
    ]
}
// REQUEST_TIMTOUT
{
    "code": 502,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| logs | JsonObject[] | 로그 정보 (**[SystemLog](#systemlog)**) | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 처리 메시지 | X |

<br>


### SystemLog

| Name | Type | Description |
| :---- | :---- |:---- |
| dateTime | String | 로그 생성 시간|
| logType | Integer | 로그 타입 (**[LogType](models.md#logtype)**) |
| content | String | 로그 종류 |

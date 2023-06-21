

## 실시간 채널 링크에 대한 API입니다.<p>채널 링크는 서로다른 채널의 ROI를 논리적 연산을 사용해 연결합니다. 

----


# 채널 링크 업데이트 
메인 채널과 서브 채널의 링크타입을 업데이트합니다.
## Request
```
POST /v2/va/update-channel-link

{
    "nodeId": "53ba9bc997c72840",
    "mainChannelId": "8c193322611294ab",
    "subChannelId": "9aa73a8450ad7eff",
    "linkedType": 1
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----:|
| nodeId | String | 컴퓨팅 노드 ID | O |
| mainChannelId | String | 메인 채널 ID | O |
| subChannelId | String | 서브 채널 ID | O |
| linkedType | Integer | 링크 타입 (**[LinkType](#linktype)**)  | O |

<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message" : ""
}
// DOES_NOT_MATCH_LINK_POINTS
{
    "code": 509,
    "message": "DOES_NOT_MATCH_LINK_POINTS"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

# 채널 링크 포인트 업데이트 
메인 채널과 서브 채널의 좌표를 업데이트합니다.
## Request
```
POST /v2/va/update-channel-link-points

{
    "nodeId": "53ba9bc997c72840",
    "channelId": "9aa73a8450ad7eff",
    "points": [
        {
            "x": 0.0,
            "y": 0.0
        },
          {
            "x": 0.84,
            "y": 0.0
        },
        {
            "x": 0.84,
            "y": 0.22
        },
        {
            "x": 0.0,
            "y": 0.5
        }
    ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----:|
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| points | JsonObject[] | ROI 라인 설정 (**[RoiDot](models.md#roi-dot)**) | O |

<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message" : ""
}
// REQUEST_TIMTOUT
{
    "code": 502,
    "message": ""
}
// NOT_FOUND_CHANNEL_UID
{
    "code": 505,
    "message": "NOT_FOUND_CHANNEL_UID"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

### LinkType

| Enum | Description |
| :---- | :---- |
| None | 링크 미설정 |
| And | 링크 AND 설정 (양쪽에서 모두 감지) |
| Or | 링크 OR 설정 (둘중 하나만 감지) |

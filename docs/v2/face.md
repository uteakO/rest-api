

## 얼굴 등록, 조회, 삭제에 대한 API입니다. 얼굴을 등록하면 검출된 객체의 얼굴과 비교해 매칭을 할 수 있습니다.

----


# 얼굴 등록
## Request
```
POST /v2/va/register-facedb

{
    "nodeId": "53ba9bc997c72840",
    "userId": "12345",
    "userName": "apple",
    "userAge": 25,
    "identifier": 0,
    "gender" : 1,
    "faceImages" : /9j/4AAQSkZJRgABAQEAYABgAAD/2....,
    "memo" : "me"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----:|
| nodeId | String | 컴퓨팅 노드 ID | O |
| userId | String | 유저 고유 ID | O |
| userName | String | 이름 | O |
| userAge | Integer | 나이 | O |
| identifier | Integer | 인종 (**[Identifier](#identifier)**) | O |
| gender | Integer | 성별 (**[Gender](#gender)**) | O |
| faceImages | String | 얼굴 이미지 정보 (이미지 string 변환) | O |
| memo | String | 메모 | X |


<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message": "",
    "uuId": "70697e9139e95a76"
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
| uuId | String | 유저 고유 ID | O |
| message | String | 오류 메시지 | X |

<br>

# 등록된 얼굴 리스트 조회 
## Request
```
POST /v2/va/list-facedb

{
    "nodeId": "53ba9bc997c72840"          
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----:|
| nodeId | String | 컴퓨팅 노드 ID | O |


<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message": "",
    "faceDBs": [
        {
            "faceImages": ['/9j/4AAQSkZJRgABAQAAAQABAAD/...]
        }
    ]
}
// REQUEST_TIMTOUT
{
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "code": 503,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| faceDBs | JsonObject[] | 얼굴 이미지 정보 리스트 (이미지 string 변환) | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |


# 등록된 얼굴 삭제
## Request
```
POST /v2/va/remove-facedb

{
    "nodeId": "53ba9bc997c72840",
    "uuId": "70697e9139e95a76"         
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----:|
| nodeId | String | 컴퓨팅 노드 ID | O |
| uuId | String | 유저 고유 ID | O |

<br>

### Response
```
// SUCCESS
{
    "code": 0,
    "message": ""
}
// REQUEST_TIMTOUT
{
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "code": 503,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 오류 메시지 | X |

<br>

# Identifier

| Enum | Description |
| :---- | :---- |
| Normal | 황인 |
| White | 백인 |
| Black | 흑인 |

# Gender

| Enum | Description |
| :---- | :---- |
| Unknown | 식별 안됨 |
| Male | 백인 |
| Female | 흑인 |
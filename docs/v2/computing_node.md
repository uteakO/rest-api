

## 실시간 영상 분석을 수행할 컴퓨팅 노드를 관리하는 API입니다.<p>컴퓨팅 노드는 NK-AI 프로세스를 논리적으로 지칭합니다.

----


# 컴퓨팅 노드 등록하기
## Request
```
POST /v2/va/create-computing-node

{
  "host": "192.168.0.39",
  "nodeName": "TEST_SYSTEM_PC",
  "license": "NKAI_IP_MAC_servercnt_chcnt"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----:|
| host | String | 호스트주소 | O |
| nodeName | String | 노드 닉네임 | O |
| license | String | 암호화된 라이선스 값 (**[Licese](#license)**)  | O |

<br>

### Response
```
// SUCCESS
{
  "nodeId": "350d8934",
  "productVersion": "1.0.8.9",
  "releaseDate": "2023.06.01",
  "code": 0
}
// REQUEST_TIMTOUT
{
  "nodeId": "",
  "productCode": "",
  "releaseDate": "",
  "code": 502
}
// INVALID_LICENSE
{
  "nodeId": "",
  "productCode": "",
  "releaseDate": "",
  "code": 20
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----:|
| nodeId | String | 컴퓨팅 노드 ID | O |
| productVersion | String | 제품 버전| O |
| releaseDate | String | 제품 릴리즈 날짜 | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |

<br><br>

# 컴퓨팅 노드 조회하기
### Request
```
POST /v2/va/get-computing-node 
{

}
```

<br>

### Response
```
// SUCCESS
{
  "node": 
  {
    "httpHost": "192.168.0.98", 
    "httpPort": 8880, 
    "nodeId": "e339d131d4a6bbc5", 
    "nodeName": "Computing Node", 
    "productVersion": "1.0.8.9", 
    "releaseDate": "2023.06.01", 
    "rpcHost": "192.168.0.98", 
    "rpcPort": 5556
  },
  "code": 0,
  "message": ""
}
// REQUEST_TIMTOUT
{
  "node":
  {
    "httpHost": "",
    "httpPort": 0,
    "nodeId": "",
    "nodeName": "",
    "productVersion": "",
    "releaseDate": "",
    "rpcHost": "",
    "rpcPort": 0
  },
  "code": 502,
  "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----|
| httpHost | String | http 호스트 | O |
| httpPort | Integer | http 포트 | O |
| nodeId | String | 컴퓨팅 노드 ID | O |
| nodeName | String | 컴퓨팅 노드 이름| O |
| productVersion | String | 제품 버전 | O |
| releaseDate | String | 제품 릴리즈 날짜 | O |
| rpcHost | String | 메타 전송 호스트 | O |
| rpcPort | Integer | 메타 전송 포트 | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 처리 메시지 | X |


<br><br>


# [deprecated] ~~컴퓨팅 노드 목록 조회하기~~ 

모든 컴퓨팅 노드를 조회합니다.

### Reqeust
```
POST /v2/va/list-computing-node 
{

}
```

### Response
```
// SUCCESS
{
    "node": 
    {
        "httpHost": "192.168.0.98", 
        "httpPort": 8880, 
        "nodeId": "e339d131d4a6bbc5", 
        "nodeName": "Computing Node", 
        "productVersion": "1.0.8.9", 
        "releaseDate": "2023.06.01", 
        "rpcHost": "192.168.0.98", 
        "rpcPort": 5556
    },
    "code": 0,
    "message": ""
}
// REQUEST_TIMTOUT
{
    "node":
    {
        "httpHost": "",
        "httpPort": 0,
        "nodeId": "",
        "nodeName": "",
        "productVersion": "",
        "releaseDate": "",
        "rpcHost": "",
        "rpcPort": 0
    },
    "code": 502,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- | :---- | :----: |
| nodeId | String | 컴퓨팅 노드 ID | O |
| nodeName | String | 컴퓨팅 노드 별칭| O |
| httpHost | String | http 호스트 | O |
| httpPort | Integer | http 포트 | O |
| rpcHost | String | 메타 전송 호스트 | O |
| rpcPort | Integer | 메타 전송 포트 | O |
| productVersion | String | 제품 버전 | O |
| releaseDate | String | 제품 릴리즈 날짜 | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 처리 메시지 | X |

<br>

# 컴퓨팅 노드 수정하기

```
POST /v2/va/update-computing-node

{
    "nodeId": "14f502f2",
    "nodeName": "TEST_NODE",
    "license" : "NKAI_IP_MAC_servercnt_chcnt"
}
```

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 노드 ID | O |
| nodeName | String | 노드 닉네임 | O |
| license | String | 암호화된 라이선스 값 (**[Licese](#license)**)  | O |

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
| :---- | :---- |:---- |:----: |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 처리 메시지 | X |




<br><br>

# 컴퓨팅 노드 삭제하기
### Request

```
POST /v2/va/remove-computing-node

{
    "nodeId": "4945bb32"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| nodeId | String | 노드 ID | O |

<br>

### Response
```
// SUCCESS
{
    "nodeId": "4945bb32",
    "code": 0,
    "message": ""
}
// REQUEST_TIMTOUT
{
    "nodeId": "",
    "code": 502,
    "message": ""
}
// NOT_FOUND_COMPUTING_NODE
{
    "nodeId": "",
    "code": 503,
    "message": ""
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:----: |
| nodeId | String | 노드 ID | O |
| code | Integer | 응답 코드 (**[Error Code](models.md#error-code)**) | O |
| message | String | 처리 메시지 | X |

<br>

## License 

| Name | Description |
| :---- |:---- |
| license | 암호화 방식에 대한 내용은 사내 개발자와 협의 필요 | 

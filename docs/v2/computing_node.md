---
layout: default
title: 컴퓨팅 노드
nav_order: 3
parent: v2
has_children: false
# permalink: /docs/v2
---

실시간 영상 분석을 수행할 컴퓨팅 노드를 관리하는 API입니다.<p>
컴퓨팅 노드는 NK-AI 프로세스를 논리적으로 지칭합니다.

----


# 컴퓨팅 노드 등록하기
## Request
```
POST /v2/va/create-computing-node

{
  "host": "192.168.0.39",
  "nodeName": "TEST_SYSTEM_PC",
  "license": "license-test-code-nkai"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| host | String | 호스트주소 | O |
| nodeName | String | 노드 닉네임 | O |
| licnese | String | 라이선스 값 | O |

<br>

### Response
```
//Ok
{
  "nodeId": "350d8934",
  "productVersion": "1.0.8.9",
  "releaseDate": "2023.06.01"
  "code" : 0
}
//Fail
{
  "message": "Failed Create Node ID",
  "code": 100
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----|
| nodeId | String | 컴퓨팅 노드 ID | O |
| productVersion | String | 제품 버전| O |
| releaseDate | String | 제품 정보 | O |
| code | Integer | 요청 응답 | O |
| message | String | 처리 메시지 | X |

<br><br>

# 컴퓨팅 노드 조회하기
### Request
```
POST /v2/va/get-computing-node {}

```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |


<br>

### Response
```
// Ok
{
  "node" : 
  {
    "httpHost": "192.168.0.98", 
    "httpPort": 8880, 
    "nodeId": "e339d131d4a6bbc5", 
    "nodeName": "Computing Node", 
    "productVersion": "1.0.8.9", 
    "releaseDate": "2023.06.01", 
    "rpcHost": "192.168.0.98", 
    "rpcPort": 5556
  }
  "message": ""
  "code": 0
}

// Fail
{
    "code": 101
    "message": "Not Found NodeId"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----|
| httpHost | String | http 호스트 | O |
| httpPort | int | http 포트 | O |
| nodeId | String | 컴퓨팅 노드 ID | O |
| nodeName | String | 컴퓨팅 노드 이름| O |
| productVersion | String | 제품 버전 | O |
| releaseDate | String | 제품 정보 | O |
| rpcHost | String | rpc 호스트 | O |
| rpcPort | int | rpc 포트 | O |
| code | Integer | 요청 응답 | O |
| message | String | 처리 메시지 | X |


<br><br>


# 컴퓨팅 노드 수정하기

```
POST /v2/va/update-computing-node
{
  "nodeId": "14f502f2",
  "nodeName": "TEST_NODE",
}
```

### Request

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 노드 ID |
| nodeName | String | 노드 닉네임 |

<br>

### Response
```
{
  "message": "",
  "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| message | String | 처리 메시지 |




<br><br>

# 컴퓨팅 노드 삭제하기
### Request

```
POST /v2/va/remove-computing-node

{
  "nodeId": "4945bb32",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String |노드 ID | O |

<br>

### Response
```
//ok
{
  "nodeId": "4945bb32",
  "code": 0
}
//fail
{
  "code": 400
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |


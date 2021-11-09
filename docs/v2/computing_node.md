---
layout: default
title: 컴퓨팅 노드
nav_order: 2
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
  "httpPort": 8880,
  "rpcPort": 33300,
  "nodeName": "ABNORMAL_DETECTING_NODE"
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| host | String | 호스트주소 | O |
| httpPort | Integer | HTTP 포트번호 | O |
| rpcPort | Integer | RPC 포트번호 | O |
| nodeName | String | 노드 닉네임 | X |
<br>

### Response
```
//Ok
{
  "nodeId": "4945bb32",
  "code": 0
}
//Already
{
  "nodeId": "4945bb32",
  "message": "ComputeNode that already exists",
  "code": 0
}
//Fail
{
  "message": "Failed Create Roi ID",
  "code": 0
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- | :----|
| nodeId | String | 노드 ID | X |
| message | String | 응답메시지 | X |
| code | int | 처리 코드 |  O |

<br><br>

# 컴퓨팅 노드 조회하기
### Request
```
POST /v2/va/get-computing-node

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
{
  "nodeId": "4945bb32",
  "nodeName": "NK_PC",
  "host": "192.168.0.36",
  "httpPort": 8880,
  "rpcPort": 33300,
  "productCode": "NKAI",
  "productVersion": "v1.0.0_v2",
  "description": "description : beta tester",
  "licenseValidity": true,
  "licenseExpired": "2021-11-13 ?? 6:47:14"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 노드 ID |
| nodeName | String | 노드 닉네임 |
| host | String | 호스트 |
| httpPort | Integer | HTTP 포트번호 |
| rpcPort | Integer | RPC 포트번호 |
| productCode | String | 제품 코드 |
| productVersion | String | 제품 버전 |
| description | String | 제품 설명 |
| licenseValidity | Bool | 라이센스 유효 여부 |
| licenseExpired | String | 라이센스 만료일(YYYY-MM-DD) |
| functions | Enum[] | (NotYet) 현재 라이센스에서 사용 가능한 기능 목록 (**[Functions](models.md#functions)**)|


<br><br>


# 컴퓨팅 노드 목록 조회하기
모든 컴퓨팅 노드를 조회합니다.

### Reqeust
```
POST /v2/va/list-computing-node

{

}
```
### Response
```
[
  {
    "nodeId": "4945bb32",
    "nodeName": "NK_PC",
    "host": "192.168.0.36",
    "httpPort": 8880,
    "rpcPort": 33300,
    "productCode": "NKAI",
    "productVersion": "v1.0.0_v2",
    "description": "description : beta tester",
    "licenseValidity": true,
    "licenseExpired": "2021-11-13 ?? 6:47:14"
  },
  {
    "nodeId": "14f502f2",
    "nodeName": "NK_TEST_PC",
    "host": "192.168.0.31",
    "httpPort": 8880,
    "rpcPort": 33300,
    "productCode": "NKAI",
    "productVersion": "v1.0.0_v2",
    "description": "description : beta tester",
    "licenseValidity": true,
    "licenseExpired": "2020-04-05 ?? 6:50:09"
  }
]
```

"[컴퓨팅 노드 조회하기](#컴퓨팅-노드-조회하기)"와 동일한 응답이 배열로 반환 됩니다.


<br><br>


# 컴퓨팅 노드 수정하기

```
POST /v2/va/update-computing-node
{
  "nodeId": "14f502f2",
  "httpPort": 9000,
  "rpcHost": "192.168.0.33"
  "rpcPort": 45500,
  "nodeName": "TEST_NODE"
}
```

### Request

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 노드 ID |
| httpPort | Integer | HTTP 포트번호 |
| rpcHost | String | RPC 호스트 |
| rpcPort | Integer | RPC 포트번호 |
| nodeName | String | 노드 닉네임 |

<br>

### Response
```
{
  "nodeId": "14f502f2",
  "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |




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
  "nodeId": "14f502f2",
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


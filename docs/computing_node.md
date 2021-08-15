# 컴퓨팅 노드

비디오 분석을 수행할 컴퓨팅 노드를 관리하는 API입니다. 컴퓨팅 노드는 실행 중인 NK-AI 서버(프로세스)입니다.

## 컴퓨팅 노드 등록하기

```
POST /v2/va/create-computing-node
```

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| host | String | 호스트 | O |
| httpPort | Integer | HTTP 포트번호 | O |
| rpcPort | Integer | RPC 포트번호 | O |
| nodeName | String | 노드 닉네임 | X |


<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |


<br><br>

## 컴퓨팅 노드 조회하기

```
POST /v2/va/get-computing-node
```
### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String |노드 ID | O |


<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 노드 ID |
| host | String | 호스트 |
| httpPort | Integer | HTTP 포트번호 |
| rpcPort | Integer | RPC 포트번호 |
| nodeName | String | 노드 닉네임 |
| productCode | String | 제품 코드 |
| productVersion | String | 제품 버전 |
| description | String | 제품 설명 |
| licenseValidity | Bool | 라이센스 유효 여부 |
| licenseExpired | String | 라이센스 만료일(YYYY-MM-DD) |
| features | [EventType](models.md#eventtype) | 현재 라이센스에서 사용 가능한 이벤트타입 목록 |


<br><br>


## 컴퓨팅 노드 목록 조회하기
모든 컴퓨팅 노드를 조회합니다.

```
POST /v2/va/list-computing-node
```

### Response
[컴퓨팅 노드 조회하기](#컴퓨팅-노드-조회하기)와 동일한 응답이 배열로 반환 됩니다.


<br><br>


## 컴퓨팅 노드 수정하기

```
POST /v2/va/update-computing-node
```

### Request

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 노드 ID |
| host | String | 호스트 |
| httpPort | Integer | HTTP 포트번호 |
| rpcPort | Integer | RPC 포트번호 |
| nodeName | String | 노드 닉네임 |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |




<br><br>

## 컴퓨팅 노드 삭제하기

```
POST /v2/va/remove-computing-node
```

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String |노드 ID | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |


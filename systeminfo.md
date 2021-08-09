# SystemInfo

### 시스템 기본정보 조회

```
POST /v2/va/get-system-info
```

| Name | Type | Description |
| :---- | :---- |:---- |
| server_id | String | 서버 UUID |
| product_code | String | 제품 코드 |
| product_version | String | 제품 버전 |
| description | String | 제품 설명 |
| license_validity | Bool | 라이센스 유효 여부 |
| license_expired | String | 라이센스 만료일(YYYY-MM-DD) |
| features | [EventType] | 현재 라이센스에서 사용 가능한 이벤트타입 목록 |
| state_is_normal | Bool | 시스템 상태가 정상인지 유무 |
| error_detail | [SystemStatus] | 오류 상태 목록 |





### 시스템 이상상태 조회

```
POST /v2/va/get-system-errors
```

| Name | Type | Description |
| :---- | :---- |:---- |
| server_id | String | 서버 UUID |
| state_is_normal | Bool | 시스템 상태가 정상인지 유무 |
| error_detail | [SystemStatus] | 오류 상태 목록 |



### SystemStatus

| Enum | Description |
| :---- | :---- |
| STATE_NORMAL | 정상 |
| STATE_RESOURCE_FULL | 시스템 리소스 한계 사용 중 |
| STATE_UNSTABLE_NETWORK | 네트워크 불안정 |
| STATE_NO_LICENSE | 라이센스 없음 |
| STATE_LICENSE_EXPIRED | 라이센스 만료 |


<!-- | STATE_LINKED_DEVICE_CONNECTION_LOST | 연동 장치 연결 불가 (예: 신호제어용 옵션보드) | -->
#


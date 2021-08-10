# SystemInfo

### 시스템 기본정보 조회

```
POST /v2/va/get-system-info
```

| Name | Type | Description |
| :---- | :---- |:---- |
| serverId | String | 서버 UUID |
| productCode | String | 제품 코드 |
| productVersion | String | 제품 버전 |
| description | String | 제품 설명 |
| licenseValidity | Bool | 라이센스 유효 여부 |
| licenseExpired | String | 라이센스 만료일(YYYY-MM-DD) |
| features | [EventType] | 현재 라이센스에서 사용 가능한 이벤트타입 목록 |
| stateIsNormal | Bool | 시스템 상태가 정상인지 유무 |
| errorDetail | [SystemStatus] | 오류 상태 목록 |





### 시스템 이상상태 조회

```
POST /v2/va/get-system-errors
```

| Name | Type | Description |
| :---- | :---- |:---- |
| systemDeviceId | String | 장치 ID |
| stateIsNormal | Bool | 시스템 상태가 정상인지 유무 |
| errorDetail | [SystemStatus] | 오류 상태 목록 |



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


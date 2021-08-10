시스템 상태를 조회하는 API입니다.

## 시스템 상태 조회
시스템에 이상이 없는지 조회합니다. 이 API를 주기적으로 호출하여 서버의 상태를 체크하십시오.
```
POST /v2/va/get-system-errors
```

### Response
아래 표시 된 노드 상태정보를 배열로 응답합니다.

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| channelsInVaRunning | Integer | 비디오 분석이 실행 중인 채널 개수 |
| systemWarnings | [SystemWarnings](#systemwarnings) | 오류 상태 목록 |
| channelsInWarning | [[Channel](models#channel-model)] | 경고 상태인 채널들의 정보 |
| cpuUsage | Double | CPU 사용률% |
| gpuUsage | Double | GPU 사용률% |
| memoryUsage | Double | Memory 사용률% |
| diskUsage | Double | Storage 사용률% |
| recentCrashLogs | [[RecentCrashLogs](models#recentcrashlogs)] | 최근 24시간 내 비정상 종료 된 컴퓨팅 노드 기록정보 |


#### JSON sample

```
{
    {
        "nodeId": "vgj3d0Aj",
        "channelsInVaRunning": 2,
        "systemWarnings": [],
        "channelsInWarning": [],
        "cpuUsage": 63.2,
        "gpuUsage": 81.1,
        "memoryUsage": 42.0,
        "diskUsage": 4.8
    },
    {
        "nodeId": "Boa9dl19",
        "channelsInVaRunning": 1,
        "systemWarnings": [],
        "channelsInWarning": [],
        "cpuUsage": 33.5,
        "gpuUsage": 41.2,
        "memoryUsage": 22.1,
        "diskUsage": 3.7
    }    
}
```

<!-- 오류 샘플 추가하기 -->



<br>

## SystemWarnings

| Enum | Description |
| :---- | :---- |
| SYS_RESOURCE_FULL | 시스템 리소스 한계 사용 중 |
| SYS_UNSTABLE_NETWORK | 네트워크 불안정 |
| SYS_NO_LICENSE | 라이센스 없음 |
| SYS_LICENSE_EXPIRED | 라이센스 만료 |



<br><br>


<!-- | STATE_LINKED_DEVICE_CONNECTION_LOST | 연동 장치 연결 불가 (예: 신호제어용 옵션보드) | -->




<!-- ## 시스템 업데이트 (TBD)
서버 버전을 업데이트 합니다.

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
|  | String |  | O | -->

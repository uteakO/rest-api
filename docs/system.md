# 2) 시스템

시스템 상태를 조회하는 API입니다.

## 시스템 상태 조회

시스템에 이상이 없는지 조회합니다. 이 API를 주기적으로 호출하여 서버의 상태를 체크하십시오.
```
POST /v2/va/get-system-status
```

### Response

아래 표시 된 노드 상태정보를 배열로 응답합니다.

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| version | [Version](#version) | 버전 정보 |
| channelsInVaRunning | Integer | 비디오 분석이 실행 중인 채널 개수 |
| systemWarnings | [SystemWarnings](#systemwarnings) | 오류 상태 목록 |
| channelsInWarning | [Channel](models.md#channel-model) | 경고 상태인 채널들의 정보 |
| performance | [Performance](#performance) | 시스템 사용률 |
| code | int | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |
| recentCrashLogs | [RecentCrashLogs](models.md#recentcrashlogs) | 최근 (24시간) 내 비정상 종료 된 컴퓨팅 노드 기록정보 |

<br>

#### JSON sample

### Request
```
POST /v2/va/get-system-status

{}
```

### Response
```
# 성공
{
    "systems":[{
        "nodeId": "vgj3d0Aj",
        "version" :{
            "software" : "1.0.0",
            "firmware" : "Windows 10 Build 19042.1165",
            "gpuModel" : "RTX 2060",
            "gpuVersion" : "462.75",
            "detectorModel": {
                "face" : "1.0.0",
                "human" : "1.1.0"
            }
        },
        "channelsInVaRunning": 2,
        "systemWarnings": [],
        "channelsInWarning": [],
        "performance" :{
            "cpuUsage": 63.2,
            "gpuUsage": 81.1,
            "memoryUsage": 42.0,
            "diskUsage": 4.8
        },
        "code" : 0
    },
    {
        "nodeId": "Boa9dl19",
        "version" :{
            "software" : "1.1.0",
            "firmware" : "ubuntu linux 30.2.1",
            "gpuModel" : "RTX 3060",
            "gpuVersion" : "462.75",
            "detectorModel": {
                "face" : "1.0.0",
                "human" : "1.1.0"
            }

        },
        "channelsInVaRunning": 1,
        "systemWarnings": [],
        "channelsInWarning": [],
        "performance" :{
            "cpuUsage": 63.2,
            "gpuUsage": 81.1,
            "memoryUsage": 42.0,
            "diskUsage": 4.8
        },
        "code" : 0
    }]  
}
```

```
# 실패
{
    "systems":[
        "nodeId": "Boa9dl0",
        "code": 8,
        "message": "can not connect node Boa9dl0"
    },
    {
        "nodeId": "Boa9dl19",
        "version" :{
            "software" : "1.1.0",
            "firmware" : "ubuntu linux 30.2.1",
            "gpuModel" : "RTX 3060",
            "gpuVersion" : "462.75" 

        },
        "channelsInVaRunning": 1,
        "systemWarnings": [],
        "channelsInWarning": [],
        "performance" :{
            "cpuUsage": 63.2,
            "gpuUsage": 81.1,
            "memoryUsage": 42.0,
            "diskUsage": 4.8
        }
    }]  
}
```

<br>

## SystemWarnings

| Enum | Description |
| :---- | :---- |
| SYS_RESOURCE_FULL | 시스템 리소스 한계 사용 중 |
| SYS_UNSTABLE_NETWORK | 네트워크 불안정 |
| SYS_NO_LICENSE | 라이센스 없음 |
| SYS_LICENSE_EXPIRED | 라이센스 만료 |

<br>

## Performance

| Name | Type | Description |
| :---- | :---- |:---- |
| cpuUsage | Double | CPU 사용률 |
| gpuUsage | Double | GPU 사용률 |
| memoryUsage | Double | Memory 사용률 |
| diskUsage | Double | Disk 사용률 |


<br>

## Version

| Name | Type | Description |
| :---- | :---- |:---- |
| software | String | NK 프로그램 버전 |
| detectorModel | Dynaimc Dictionary | model version |
| firmware | String | 펌웨어 버전 (OS) |
| gpuModel | String | GPU 모델 |
| gpuVersion | String | GPU 버전 |


<br><br>
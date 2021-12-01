---
layout: default
title: 시스템
nav_order: 6
parent: v2
has_children: false
# permalink: /docs/v2
---


시스템 상태를 조회하는 API입니다.

# 시스템 상태 조회

시스템에 이상이 없는지 조회합니다. 이 API를 주기적으로 호출하여 시스템의 전반적인 이상 상태를 체크할 수 있습니다.
```
POST /v2/va/get-system-status
```

### Response

아래 표시 된 노드 상태정보를 배열로 응답합니다.

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| version | JsonObject | 버전 정보(**[Version](models.md#version)**) |
| channelsInVaRunning | Integer | 비디오 분석이 실행 중인 채널 개수 |
| systemWarnings | Enum[] | 오류 상태 목록(**[SystemWarnings](models.md#systemwarnings)**) |
| channelsInWarning | JsonObject[] | 경고 상태인 채널들의 정보 (**[Channel](models.md#channel)**) |
| performance | JsonObject | 시스템 사용률(**[Performance](models.md#performance)**) |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |


<!-- | recentCrashLogs | JsonObject | 최근 (24시간) 내 비정상 종료 된 컴퓨팅 노드 기록정보([RecentCrashLogs](models.md#recentcrashlogs)) | -->

<br>

### JSON sample

#### Request
```
POST /v2/va/get-system-status

{}
```

#### Response
```
# 성공
{
    "systems" : 
    [
        {
            "nodeId": "ae7255c0",
            "version": {
                "software": "NKProcess",
                "detectorModel": [
                    "Normal"
                ],
                "firmware": "firmware_20211125 05:47:46",
                "gpuModel": "NVIDIA GeForce RTX 3070 Laptop GPU",
                "gpuVersion": "9984",
                "disk": "C:\\"
            },
            "countVAChannels": 1,
            "performance": {
                "cpuUsage": 26.82,
                "gpuUsage": 13.4,
                "memoryUsage": 51.54,
                "memoryTotal": 34110451712.0,
                "memoryFree": 16507592704.0,
                "diskUsage": 64.23,
                "diskTotal": 977443745792.0,
                "diskFree": 349605699584.0
            }
        }
    ],
  "code": 0
}
```

```
# 실패
{
    "code": 8,
    "message": "can not connect node Boa9dl0"
}
```

<br>

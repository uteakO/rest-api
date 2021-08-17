# 3) 채널

채널에 대한 API입니다. 채널은 1개의 비디오에 대한 정보이며, 영상분석을 수행하는 단위입니다.

__목차__

- [채널 등록하기](#채널-등록하기)
- [채널 보기](#채널-보기)
- [채널 목록보기](#채널-목록보기)
- [채널 수정하기](#채널-수정하기)
- [채널 삭제하기](#채널-삭제하기)
- [카메라 캘리브레이션](#카메라-캘리브레이션)
- [스냅샷](#스냅샷)

------------------------

## 채널 등록하기

비디오 분석을 수행할 채널을 등록합니다.

```
POST /v2/va/register-channel
```
<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelName | String | 채널 별칭 | X |
| inputUri | String | 입력 비디오 URI (RTSP 주소 또는 로컬파일 경로) | O |
| inputType | String | 입력 비디오 타입 ([InputType](models#inputtype)) | X |
| siblings | String[] | 연결된 채널 id 목록 | X |

<!-- | annotatedVideoOutputUri | String | Annotation 렌더링한 비디오파일 저장위치 | X | -->

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| code | int | 오류 코드 ([Error Code](models.md#error-code)) |
| message | string | 오류 메시지 |

<br>

### Remarks
#### nodeId
채널의 입력 영상에 대해 비디오 분석을 수행 할 컴퓨팅 노드의 ID 입니다. 비디오 분석을 수행하기 위해서는 최소 1개의 컴퓨팅 노드가 필요합니다.

#### siblings
동일한 목표지점을 촬영하는 채널인 경우, sibling 관계가 될 수 있습니다. 예를 들어, 같은 위치에서 같은 목표지점을 촬영하도록 일반카메라와 열화상카메라 CCTV가 각각 설치 된 경우입니다. 이 때, 두 CCTV 영상들의 분석결과는 서로 상관관계가 있으므로, 이것을 응용 앱에서 활용하기 위해 본 파라메터를 이용하여 sibling 관계를 관리할 수 있습니다.

<br>

### Sample
#### Request
```
POST /v2/va/register-channel

{
    "nodeId": "a9fjaLsT",
    "channelName": "CCTV on front door",
    "inputUri": "rtsp://admin:password@192.168.0.100:554/live",
    "inputType": "SRC_IPCAM_NORMAL",
    "siblings": []
}
```

#### Response
```
# 성공
{
    "channelId": "X1ashF0t",
    "code": 0,
}
```

```
# 실패
{
    "channelId": "X1ashF0t",
    "code": 3,
    "message": "Authentication failed"
}
```

<br><br>



## 채널 보기
채널의 상세 정보를 조회합니다.

```
POST /v2/va/get-channel
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| channel | JsonObject | 채널 정보 ([Channel Model](models.md#channel-model)) |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Sample

#### Requset
```
POST /v2/va/get-channel

{
    "channelId": "X1ashF0t"
}
```

### Response
```
# 성공
{
   "channel": { 
       "channelId": "X1ashF0t",
       "nodeId": "a9fjaLsT",
       "inputUri" : "rtsp://admin:password@192.168.0.100:554/live",
       "channelName": "CCTV on front door",
       "inputType": "SRC_IPCAM_NORMAL",
       "sibilngs" : ["",""]
       "status": "CH_STATUS_NORMAL"
   },
   "code": 0
}
```

```
# 실패
{
    "code" : 1
    "message" : "ChannelId (X1ashF0t) not exists"
}
```

<br><br>


## 채널 목록보기
전체 채널 상세정보를 조회합니다.

```
POST /v2/va/list-channels
```

<br>


### Response

[Channel Model](models.md#channel-model)의 배열을 반환합니다.

<br>

### Sample

#### Requset
```
POST /v2/va/list-channels

{}
```

### Response
```
{
   "channels": [{ 
       "channelId": "X1ashF0t",
       "nodeId": "a9fjaLsT",
       "inputUri" : "rtsp://admin:password@192.168.0.100:554/live",
       "channelName": "CCTV on front door",
       "inputType": "SRC_IPCAM_NORMAL",
       "sibilngs" : ["",""]
       "status": "CH_STATUS_NORMAL"
   },
   { 
       "channelId": "X1ashF0t2",
       "nodeId": "a9fjaLsT2",
       "inputUri" : "rtsp://admin:password@192.168.0.100:554/live",
       "channelName": "CCTV on back door",
       "inputType": "SRC_IPCAM_NORMAL",
       "sibilngs" : ["",""]
       "status": "CH_STATUS_INPUT_DEVICE_CONNECTION_LOST"
   }]
}
```


<br><br>


## 채널 수정하기
채널의 정보를 수정합니다.

```
POST /v2/va/update-channel
```

<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| nodeId | String | 컴퓨팅 노드 ID | X |
| inputUri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) | X |
| channelName | String | 채널 별칭 | X |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Sample

#### Requset
```
POST /v2/va/update-channel

{
    "channelId": "X1ashF0t",
    "channelName": "Home CCTV",
}
```

#### Response
```
# 성공
{
   "code": 0
}
```

```
# 실패
{
    "code" : -1
    "message" : "Not Exist ChannelId"
}
```

<br><br>

## 채널 삭제하기
채널의 정보를 삭제합니다.

```
POST /v2/va/remove-channel
```
<br>

### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |


<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

### Remarks

비디오 분석이 실행 중인 채널은 삭제할 수 없으며, 삭제하려면 먼저 분석 실행을 중단해야 합니다.

<br>

### Sample
#### Request
```
POST /v2/va/remove-channel

{
    "channelId": "X1ashF0t"
}
```

#### Response
```
# 성공
{
    "code" : 0
}
```

```
# 실패
{
    "code" : 5
    "message" : "stop analyzing first"
}
```


<br><br>

## 카메라 캘리브레이션

```
POST /v2/va/callibrate
```

<br>


### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| distortionPoints | JsonObject | 왜곡 보정을 위한 동일한 직선 위의 3점의 영상 좌표 ([DistortionPoint](models#distortion-point))| O |
| calibrationPoints | JsonObject | 왜곡 보정을 위한 동일한 직선 위의 3점의 영상 좌표 ([CalibrationPoint](models#calibration-point)) | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

#### Sample JSON

#### Requset
```
POST /v2/va/callibrate

{
    "channelId": "X1ashF0t",
    "distortionPoints": {
        "startPoint" : [0.3, 0.4],
        "middlePoint": [0.3, 0.4],
        "endPoint": [0.3, 0.4]
    },
    "calibrationPoints": {
        "verticalPoint1" : [0.3, 0.4],
        "verticalPoint2" : [0.3, 0.4],
        "horizontalPoint1" : [0.3, 0.4],
        "horizontalPoint2" : [0.3, 0.4]
    }
}

```

#### Response 
```
# 성공
{
    "code" : 0
}

# 오류
{
    "code": 6,
    "message": "Channel X1ashF0t not exists"
}
```

<br><br>

## 스냅샷

채널의 영상 스냅샷을 반환합니다.
```
POST /v2/va/snapshot
```

<br>


### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| imageData | String | 카메라 스틸컷 데이터 (jpeg -> base64인코딩) |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

#### Sample JSON

#### Requset
```
POST /v2/va/snapshot

{
    "channelId": "X1ashF0t"
}

```

#### Response 
```
# 성공
{
    "imageData" : "x35hj34Bd239...."
    "code" : 0
}

# 오류
{
    "code": 1,
    "message": "Channel X1ashF0t not exists"
}
```
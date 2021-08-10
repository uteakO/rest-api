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


### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | X |
| channelName | String | 채널 별칭 | X |
| inputUri | String | 입력 비디오 URI (RTSP 주소 또는 로컬파일 경로) | X |
| inputType | enum([InputType](models#inputtype)) | 입력 비디오 타입| X |
| siblings | [String] | 연결된 채널 id 목록 | X |

<!-- | annotatedVideoOutputUri | String | Annotation 렌더링한 비디오파일 저장위치 | X | -->

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |

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
{
    "channelId": "X1ashF0t"
}
```

<br><br>



## 채널 보기
채널의 상세 정보를 조회합니다.

```
POST /v2/va/get-channel
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response
[Channel Model](models#channel-model)을 반환합니다.


<!-- #### Sample
##### Response

```
{
    "channelId": "X1ashF0t",
    "inputUri": "rtsp://admin:password@192.168.0.100:554/live",
    "name": "cam01",
    "status": "OK"
}
``` -->

<br><br>


## 채널 목록보기
전체 채널 상세정보를 조회합니다.

```
POST /v2/va/list-channels
```

### Response

[Channel Model](models#channel-model)의 배열을 반환합니다.


<br><br>


## 채널 수정하기
채널의 정보를 수정합니다.

```
POST /v2/va/update-channel
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| nodeId | String | 컴퓨팅 노드 ID | X |
| inputUri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) | X |
| name | String | 채널 별칭 | X |

<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |



<br><br>

## 채널 삭제하기
채널의 정보를 삭제합니다.

```
POST /v2/va/remove-channel
```

### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |


<br>

### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |

<br>

### Remarks
비디오 분석이 실행 중인 채널은 삭제할 수 없으며, 삭제하려면 먼저 분석 실행을 중단해야 합니다.


<!-- #### Sample
##### Request
```
POST /v2/va/channels/modify/X1ashF0t

{
    "inputUri": "rtsp://admin:password@192.168.0.101:554/live",
    "name": "cam03"
}
```

##### Response
```
{
    "channelId": "X1ashF0t",
    "inputUri": "rtsp://admin:password@192.168.0.101:554/live",
    "name": "cam03",
    "status": "OK"
}
``` -->


<br><br>

## 카메라 캘리브레이션

```
POST /v2/va/callibrate
```


### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| distortionPoints | object([DistortionPoint](#distortionpoint)) | 왜곡 보정을 위한 동일한 직선 위의 3점의 영상 좌표 | O |
| calibrationPoints | object([CalibrationPoint](#calibrationpoint)) | 왜곡 보정을 위한 동일한 직선 위의 3점의 영상 좌표 | O |


### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| callibrationResult | String | 캘리브레이션 결과 |

#### 오류 코드
| 코드 | 설명 |
| :---- | :---- |
| -1 | 등록되지 않은 채널 |
| -2 | 비디오 입력(inputUri)이 유효하지 않음 |
| -3 | 캘리브레이션 실패 |


#### Sample JSON
```
# 성공
{
    "channelId": "X1ashF0t",
    "callibrationResult": "Success"
}

# 오류
{
    "code": -1,
    "error_message": "Channel X1ashF0t not exists"
}
```

<br><br>

### DistortionPoint
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| startPoint | [Integer] |  첫 번째 점의 X, Y 좌표 | O |
| middlePoint | [Integer] |  중간 점의 X, Y 좌표 | O |
| endPoint | [Integer] |  마지막 점의 X, Y 좌표 | O |


<br>

### CalibrationPoint
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| verticalPoint1 | [Integer] |  세로로 된 직선 1의 시작, 끝 X, Y 좌표 | O |
| verticalPoint2 | [Integer] |  세로로 된 직선 2의 시작, 끝 X, Y 좌표 | O |
| horizontalPoint1 | [Integer] |  가로로 된 직선 1의 시작, 끝 X, Y 좌표 | O |
| horizontalPoint2 | [Integer] |  가로로 된 직선 2의 시작, 끝 X, Y 좌표 | O |




## 스냅샷
채널의 영상 스냅샷을 반환합니다.
```
POST /v2/va/snapshot
```


### Request

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| imageData | String | 카메라 스틸컷 데이터 (jpeg -> base64인코딩) |
| imageWidth | Integer | 가로 해상도 |
| imageHeight | Integer | 세로 해상도 |


<br>

#### 오류 코드
| 코드 | 설명 |
| :---- | :---- |
| -1 | 등록되지 않은 채널 |
| -2 | 비디오 입력(inputUri)이 유효하지 않음 |
| -3 | 스냅샷 생성 실패 |

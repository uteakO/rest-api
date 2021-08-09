채널에 대한 API입니다. 채널은 1개의 비디오에 대한 정보이며, 영상분석을 수행하는 단위입니다.

------------------------

### 채널 등록하기

```
POST /v2/va/channels/register
```


#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| input_uri | String | 입력 비디오 URI (RTSP 주소 또는 로컬파일 경로) | X |
| name | String | 채널 별칭 | X |
| input_device_type | enum([DeviceType](classes.md#DeviceType)) | 입력장치 타입| X |
| siblings | [String] | 연결된 채널 id 목록 | X |


#### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channel_id | String | 채널 ID |
| input_uri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) |
| name | String | 채널 별칭 |
| input_device_type | enum([DeviceType](classes.md#DeviceType)) | 입력장치 타입 |
| siblings | [String] | 연결된 채널 id 목록 |
| status | String | 채널 상태 |

#### Remarks
##### siblings
동일한 목표지점을 촬영하는 채널인 경우, sibling 관계가 될 수 있습니다. 예를 들어, 같은 위치에서 같은 목표지점을 촬영하도록 일반카메라와 열화상카메라 CCTV가 각각 설치 된 경우입니다. 이 때, 두 CCTV 영상들의 분석결과는 서로 상관관계가 있으므로, 이것을 응용 앱에서 활용하기 위해 본 파라메터를 이용하여 sibling 관계를 관리할 수 있습니다.



#### Sample
##### Request
```
{
    "input_uri": "rtsp://admin:password@192.168.0.100:554/live",
    "name": "cam01"
}
```

##### Response
```
{
    "channel_id": "X1ashF0t",
    "input_uri": "rtsp://admin:password@192.168.0.100:554/live",
    "name": "cam01",
    "status": "OK"
}
```


### 채널 목록보기
전체 채널 상세정보를 조회합니다.

```
POST /v2/va/channels/list
```



#### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channel_id | String | 채널 ID |
| input_uri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) |
| name | String | 채널 별칭 |
| status | String | 채널 상태 |

#### Sample

##### Response
```
{
    {
        "channel_id": "X1ashF0t",
        "input_uri": "rtsp://admin:password@192.168.0.100:554/live",
        "name": "cam01",
        "status": "OK"
    },
    {
        "channel_id": "aAdjbu39",
        "input_uri": "rtsp://admin:password@192.168.0.101:554/live",
        "name": "cam02",
        "status": "CANNOT ACCESS RTSP VIDEO SOURCE"
    }
}
```


### 채널 보기
채널의 상세 정보를 조회합니다.

```
POST /v2/va/channels/{channel_id}
```


#### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channel_id | String | 채널 ID |
| input_uri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) |
| name | String | 채널 별칭 |
| status | String | 채널 상태 |


#### Sample
##### Response

```
{
    "channel_id": "X1ashF0t",
    "input_uri": "rtsp://admin:password@192.168.0.100:554/live",
    "name": "cam01",
    "status": "OK"
}
```

### 채널 수정하기
채널의 정보를 수정합니다.

```
POST /v2/va/channels/modify/{channel_id}
```

#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channel_id | String | 채널 ID | O |
| input_uri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) | X |
| name | String | 채널 별칭 | X |


#### Response
| Name | Type | Description |
| :---- | :---- |:---- |
| channel_id | String | 채널 ID |
| input_uri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) |
| name | String | 채널 별칭 |
| status | String | 채널 상태 |




#### Sample
##### Request
```
{
    "channel_id": "X1ashF0t",
    "input_uri": "rtsp://admin:password@192.168.0.101:554/live",
    "name": "cam03"
}
```

##### Response
```
{
    "channel_id": "X1ashF0t",
    "input_uri": "rtsp://admin:password@192.168.0.101:554/live",
    "name": "cam03",
    "status": "OK"
}
```



### 카메라 캘리브레이션

```
POST /v2/va/channels/{channel_id}/callibration
```


#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| distortion_points | [DistortionPoint] | 왜곡 보정을 위한 동일한 직선 위의 3점의 영상 좌표 | O |
| calibration_points | [CalibrationPoint] | 왜곡 보정을 위한 동일한 직선 위의 3점의 영상 좌표 | O |




#### DistortionPoint
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| start_point | [Integer] |  첫 번째 점의 X, Y 좌표 | O |
| middle_point | [Integer] |  중간 점의 X, Y 좌표 | O |
| end_point | [Integer] |  마지막 점의 X, Y 좌표 | O |



#### CalibrationPoint
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| vertical_point_1 | [Integer] |  세로로 된 직선 1의 시작, 끝 X, Y 좌표 | O |
| vertical_point_2 | [Integer] |  세로로 된 직선 2의 시작, 끝 X, Y 좌표 | O |
| horizontal_point_1 | [Integer] |  가로로 된 직선 1의 시작, 끝 X, Y 좌표 | O |
| horizontal_point_2 | [Integer] |  가로로 된 직선 2의 시작, 끝 X, Y 좌표 | O |

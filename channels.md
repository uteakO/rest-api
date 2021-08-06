채널에 대한 API입니다. 채널은 1개의 동영상에 대한 정보이며, 영상분석을 수행하는 단위입니다.

------------------------

### 채널 등록하기

```
POST /v2/va/channels/register
```


#### Request
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| input_uri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) | O |
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
GET /v2/va/channels
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
---
layout: default
title: 비디오 분석 결과
nav_order: 8
parent: v2
has_children: false
# permalink: /docs/v2

---

비디오 분석 결과는 zmq의 PUBlisher – SUBscriber 패턴(서버가 발행하는 메시지가 각각의 클라이언트로 분산되어 전파된다.)을 통해 스트리밍 방식으로 클라이언트에게 전송됩니다.
이 외에도 rest-api를 통해 서버와 클라이언트가 메타데이터를 주고 받으며 ai_edge_link 프로그램을 통해 mqtt, csv 등과 같은 통신방식으로 메타데이터를 송신할 수 있습니다. 

---

<br>

### ObjectMeta 

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| CameraName | String | 채널 별칭 |
| CameraUID | String | 채널 ID |
| EventList | String | 오류 메시지 (**[EventList](va_results.md#eventlist)**) |
| FrameHeight | Integer | 영상 높이 |
| FrameNumber | Integer | 영상 프레임 |
| FrameWidth | Integer | 영상 가로길이 |
| TimeStamp | Integer | 영상 타임스탬프 |

<br>

### EventList

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| AbnormalScore | Double | 계산된 이상수치 (이벤트 타입별로 정체지수, 체류시간, 자세이상수치의 의미를 가짐) |
| ClassID | Integer | 채널 ID (**[ClassId](models.md#classid)**) |
| EventDetail | String | 이벤트 디테일 (**[EventDetail](va_results.md#eventdetail)**) |
| EventStatus | Integer | 이벤트 진행 상태 (**[EventStatus](va_results.md#eventstatus)**) |
| EventType | String | 이벤트 타입 (**[EventType](models.md#eventtype)**) |
| ImageBuffer | String | 이미지 버퍼 |
| ImageRect | Integer | 이미지 좌표 및 크기 (**[ImageRect](va_results.md#imagerect)**) |
| InnerImageRect | Double | ----- |
| IsDetected | bool | 감지 여부 |
| IsEvent | bool | 이벤트 발생 여부 |
| IsTracked | bool | 객체 추적 여부 |
| ObjectColor | Integer | 바운딩 박스 색상 (**[ObjectColor](va_results.md#objectcolor)**) |
| ObjectID | String | 객체 ID |
| RoiInfo | Integer | 관심 영역 정보 (**[RoiInfo](va_results.md#roi-info)**) |
| StayTime | String | 체류 시간 |

<br>

### Roi Info

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| RoiUid | String | 관심 영역 ID |
| RoiName | String | 관심 영역 별칭 |
| ~~RoiColor~~ | ~~Integer~~ | ~~관심 영역 색상 (**[ObjectColor](va_results.md#objectcolor)**)~~ |
| ObjectCount | Integer | 현재 영역안의 객체 수 |
| EnteredCount | Integer | 영역안에 진입한 총 객체 수 |
| ExitedCount | Integer | 영역밖으로 진출한 총 객체 수 |
| AvgStayTime | Double | 평균 체류 시간 |

<br>

### EventDetail

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| EventScore | Integer | --- |
| Face | JasonObject[] | 얼굴 정보 (**[Face](va_result.md#face)**) |
| FaceUID | String | 객체 ID |
| KeyPoints | JasonObject[] | 키 포인트 (**[KeyPoints](va_result.md#keypoints)**) |

<br>

### ImageRect

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| Height | Double | 이미지 높이 |
| Width | Double | 이미지 가로길이 |
| X | Double | 이미지 X 좌표 |
| Y | Double | 이미지 Y 좌표 |

<br>

### Face

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| Age | Integer | 객체 나이 |
| Gender | Integer | 객체 성별 |
| Name | String | 객체 이름 |

<br>

### KeyPoints

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| Score | Double | 정확도 |
| X | Double | 키 포인트 X좌표 |
| Y | Double | 키 포인트 Y좌표 |

<br>

### ObjectColor

<br>

| Name | Type | Description |
| :---- | :---- |:---- |
| R | Integer | 빨강 |
| G | Integer | 초록|
| B | Integer| 파랑 |

<br>

### EventStatus

<br>

| Value | Description | 
| :---- | :---- |
| -1 | 이벤트 미발생 |
| 0 | 이벤트 발생 |
| 1 | 이벤트 지속 |
| 2 | 이벤트 종료 |

<br>


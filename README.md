# Welcom to NK developers

<!-- * [Introduction](README.md) -->
* [채널](channels.md)
* [영상 분석 설정](va.md)
* [시스템 정보](systeminfo.md)
* [클래스](classes.md)


# 구성

* channel CRUD + list
  - GET detail 포함내용
      - WebRTC 비디오 출력 정보 정의
      - RTSP output
  - output meta uri 설정기능
  - 카메라 캘리브레이션
* VA config CRUD + list (구 ROI)
   - 이벤트 타입별로 커맨드 파라메터를 정의하여 reset 기능 정의하기
      - 진입, 진출, 평균대기시간, 전체카운트 (배열 파라메터로 정의하기)
   - preset 제공 (ITS, 시설보안, 방위산업)
   - API 가독성 향상 필요
   - 사진을 포함한 예제 동봉하기
* 분석 start, stop
* 수신 URI 등록
* GET 시스템상태
  - 상태 비정상인 채널 전체 목록
    - 카메라 접속 상태 불량
  - 시스템 리소스 한계사용 경고
  - 시스템 네트워크 상태 불량
  - 라이센스 오류 (미입력, 만료)
  - 연동 장치 연결오류 (예: 신호제어용 옵션보드)
* 스냅샷

* 에러 응답 정의

* 서버 정보 조회
  - 서버 고유 ID
  - 제품코드 (예: NKAI_WINDOWS)
  - 버전
  - 서버 별칭
  - 라이센스 획득 여부
  - 사용 가능한 알고리즘 리스트


# 정책
* All POST method: 레거시 시스템 호환, Client측의 GET 캐싱으로 인한 오류 원천차단
* 검출 타겟별로 개별 설정 가능해야 함
  - Google, Kakao와 같이 알고리즘별로 설정파라메터를 개별 정의함
* OSD 결과출력 (디버깅 용도로만 사용)
* RTSP output uri를 채널 보기 API에서 제공해야하는가?
  - uri 구성 룰: `http://host:port/{channel_id}`
* RTSP output resolution 조정 파라메터


# QnA
- channel_id : 분산 된 서버에서 unique할 수 있는가?
- name or channel_name : 개발 시 검색 편의성 측면
- uuid 중복 위험은? 서버/클라이언트 분리 시, N개 서버에서 1개 DB서버 공유할 것인가?
- 연동장치는 channel단위인가? 시스템단위인가?
- 옵션보드 연동을 VA서버에서 하는 것이 맞는가? 비즈니스로직을 실행하는 독립서비스에서 처리하는 것이 맞지 않는가?
- 이벤트라는 용어가 객체검출과 이벤트검출을 모두 포함하는가? VA feature라고 부르는 것이 맞지 않은가?


- 다음 파라메터들이 이벤트별로 공통인가?
```
abnormal_stay_time	Double	배회: 검지 시간
distance	Double	차량 속도: 두 라인간 거리, 차량 밀도: 영역의 거리
abnormal_obj_count	Double	영역 ROI 내 개체밀집: 기준 인원 수
abnormal_ci	Double	영역 ROI 내 이동흐름 정체: 정체도 기준값
```
  - 검출항목에 특화된 설정이 향후 발생할 여지가 높으므로, 검출항목별로 config 항목을 개별 정의
     - 참고: [Google cloud video intelligence API](https://cloud.google.com/video-intelligence/docs/reference/rest/v1p3beta1/videos/annotate#videocontext)

- 진입/진출 등 카운트 리셋이 개별로, 채널단위 전체리셋으로 필요한가?
- 분석결과 출력 시 아래 중 어느 것이 더 쓸모있는가?
   - ROI 단위로 이벤트를 모아서 출력
   - 현재처럼 검출항목 단위로 모아서 출력하고, 각 검출결과에 ROI id를 첨부해주는 것

# Welcom to NK developers

<!-- * [Introduction](README.md) -->

__목차__
* [채널](channels)
* [비디오 분석 제어](va_control)
* [시스템](system)
* [모델](models)
* [영상 분석 결과](va_results)






# 정책
* All POST method: 레거시 시스템 호환, Client측의 GET 캐싱으로 인한 오류 원천차단
* 검출 타겟별로 개별 설정 가능해야 함
  - Google, Kakao와 같이 알고리즘별로 설정파라메터를 개별 정의함
* OSD 결과출력 (디버깅 용도로만 사용)
    * RTSP output uri를 채널 보기 API에서 제공해야하는가?
        - uri 구성 룰: `http://host:port/{channelId}`
    * RTSP output resolution 조정 파라메터
* Master노드 1개 : 컴퓨팅노드 N개 방식으로 구성
    - DB는 Master노드에 위치
    - Master노드와 컴퓨팅노드는 동일 서버일 수 있음


# QnA
- channel_id : 분산 된 서버에서 unique할 수 있는가 --> master DB 설정하는 방식으로 결정.
  - uuid 중복 위험은? 서버/클라이언트 분리 시, N개 서버에서 1개 DB서버 공유할 것인가?
- name or channel_name : 개발 시 검색 편의성 측면 --> 접두사 붙이는 방식으로 결정
- 옵션보드 연동을 VA서버에서 하는 것이 맞는가? 비즈니스로직을 실행하는 독립서비스에서 처리하는 것이 맞지 않는가? -> No. 독립서비스 실행이 정상구조. 본 OpenAPI에는 반영하지 않음
  - 연동장치는 channel 단위인가? 시스템단위인가? --> edge에서는 장비:보드가 1:1이지만, 채널단위로 장치를 정의함 (현재 edge에서만 연동되어있음)
- 이벤트라는 용어가 객체검출과 이벤트검출을 모두 포함하는가? VA feature라고 부르는 것이 맞지 않은가?
  --> 이벤트알람, 객체검출 용어를 분리해서 사용하는 것이 자연스럽다


- 검출항목별 파라메터들이 이벤트별로 공통인가?
  -> No. 이벤트별로 다르므로 개별 정의하기
     - 참고: [Google cloud video intelligence API](https://cloud.google.com/video-intelligence/docs/reference/rest/v1p3beta1/videos/annotate#videocontext)

- 진입/진출 등 카운트 리셋이 개별로, 채널단위 전체리셋으로 필요한가?
  --> 유저마다 요구가 다름. 채널단위로 우선 하고, roi단위는 향후 요구사항 발생 시 추가 예정
- 분석결과 출력 시 아래 중 어느 것이 더 쓸모있는가?
   - ROI 단위로 이벤트를 모아서 출력
   - 현재처럼 검출항목 단위로 모아서 출력하고, 각 검출결과에 ROI id를 첨부해주는 것
     --> 현재방식이 유효

- 시스템 정보출력에서 CPU, RAM, DISK 사용률도 함께 출력 필요 (네트워크 대역폭 사용량은 향후 필요시 추가) --> OK

- 검출항목별로 세부파라메터는 실무자들이 협의하여 작성

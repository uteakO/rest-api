# NK-AI API 목록 

<!-- * [Introduction](README.md) -->


[컴퓨팅 노드](computing_node.md)

[시스템](system.md)

[채널](channels.md)

[비디오 분석 제어](va_control.md)

[영상 분석 결과](va_results.md)

[모델](models.md)






# 정책
* 레거시 시스템과의 호환성을 위해 모든 REST API 메서드는 POST로 통일하였습니다.
* 어노테이션 렌더링 된 비디오 출력은 내부적으로 디버깅 용도로만 사용 중입니다. 클라이언트 측에서는 검출결과 메타데이터를 활용해주십시오. 
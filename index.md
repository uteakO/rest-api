---
layout: default
title: Home
nav_order: 1
description: ""
permalink: /
---

# Introduction

NK-AI API의 프로토콜은 REST API(HTTP/JSON)와 gRPC(HTTP2)로 구성됩니다.


### REST API
단방향 요청/응답 형식의 기능에 사용합니다.
 - 예: [채널 관리](docs/v2/channels), [비디오 분석 설정](docs/v2/va_control/roi)

### gRPC
메세지를 반복 전송하는 스트리밍 성격의 통신에 사용합니다.
 - 예: [비디오 분석 결과 전송](docs/v2/va_results)

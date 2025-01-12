---
layout: post
title: Websocket disconnect
description: >
  Websockets client 연결 끊김
categories:
  - python
  - websocket
---

파이썬 Websockets 라이브러리에서 

websockets.exceptions.InvalidStatus: server rejected WebSocket connection: HTTP 403

에러가 발생 할 시

~~~python
from websockets.asyncio.client import connect

async with connect(url, ping_interval=None) as websocket:
  pass
~~~

처럼 ping_interval 을 None 으로 주면 해결된다

하지만 핑을 꺼버리면 연결 상태 확인이 어려워진다

~~~python
logger = logging.getLogger()
logger.addHandler(handler)
logger.setLevel(logging.INFO)
~~~

로그를 확인해본 결과 핑은 정상적으로 수행되었고
핑 전송 일정 시간 후 연결이 종료된다는 것을 확인하였다

~~~python
from websockets.asyncio.client import connect

async with connect(url) as websocket:
  message = await websocket.recv()
~~~

서버에서 메시지를 받으면 응답하도록 되어있었는데
서버에서 보내는 메시지를 recv() 로 응답을 받으면 더이상 끊기지 않는다

핑 테스트 후 어딘가 데이터가 저장되다 가득차면서 끊기는 것 같다 (추정)



*[HTML]: HyperText Markup Language
*[CSS]: Cascading Style Sheets
*[JS]: JavaScript

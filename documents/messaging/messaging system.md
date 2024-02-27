# 메시징 시스템(messaging system)

## 메시지 큐
- 데이터 교환에 사용되는 통신 방법
- Producer -> Queue -> Consumer 

## 종류
- Apache Kafka
- RabbitMQ

## Apache Kafka
- 게시(publish) / 구독(subscribe) 방식
- 분산 메시징 시스템
- 대규모 분산 이벤트 스트리밍에 주로 사용
- 스트리밍 데이터를 처리하는 곳에 적합

## RabbitMQ
- publisher -> exchange -> queues -> consumer
- AMQP 프로토콜을 구현한 메시지 브로커 방식
- 높은 안정성으로 수집한 메시지 데이터를 queue에 넣고 꺼내 쓰는 방식
- 신뢰성 높은 작업(장시간 실행), 안정적인 데이터를 처리하는 곳에 적합

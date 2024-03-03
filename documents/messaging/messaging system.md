# 메시징 시스템(messaging system)

## 사융 이유
- 발신자와 수신자가 서로의 정보를 알 필요없이 독립적으로 시스템을 구성할 수 있다.(느슨한 결합, decoupling)
- 수신자의 서비스에 장애가 발생하여도 발행된 메시지는 모두 Queue에 보관되어 있기 때문에 메시지 손실이 없다.
- MSA 시스템에 효율적이다.
- http 통신은 request 후 response를 기다리지만(동기 통신)
- 메시지는 Queue에 메시지를 발행하고 수신자(구독)가 가져가는 방식(비동기 통신)

## 메시지 큐
- 데이터 교환에 사용되는 통신 방법
- Producer -> Queue -> Consumer 

## 메시지 브로커
- 송신자의 메세지 프로토콜 형식을 수신자의 메시지 프로토콜 형식으로 바꾸는 프로그램
- 메시지 큐, 토픽과 같은 구조에 송신된 메세지를 임시로 저장하고 수신자에게 전달하는 방식
- 생산자와 소비자간 중개 역할을 하여, 두 시스템이 독립적으로 작동할 수 있게한다.

## 종류
- Apache Kafka
- RabbitMQ

## Apache Kafka
- 게시(publish) / 구독(subscribe) 방식
- 분산 메시징 시스템
- 대규모 분산 이벤트 스트리밍에 주로 사용
- 스트리밍 데이터를 처리하는 곳에 적합
- 주키퍼를 사용해 클러스터를 관리

### Apache Kafka 구조
- Producer -> ZooKeeper[Broker[Topic[Partition]]] -> Consumer
- Producer : 송신자는 특정 토픽에 메시지를 발행한다.
- ZooKeeper : 브로커를 관리(kafka 3.0부터 ZooKeeper 없이 사용할 수 있다.)
- Brodker : 송신자로부터 받은 메시지를 저장하고 수신자에게 전달
- Topic : kafka에서 데이터를 분류하는 단위
- Partition : 토픽을 병렬로 저장한다.
- Consumer : kafka의 특정 토픽(Topic1 또는 Topic2)를 구독하고 해당 토픽의 메시지를 수신
```html
    Topic1(Partition1, Partition2...)
    Topic2(Partition1, Partition2...)
```

## RabbitMQ
- AMQP 프로토콜을 구현한 메시지 브로커 방식
- 높은 안정성으로 수집한 메시지 데이터를 queue에 넣고 꺼내 쓰는 방식
- 신뢰성 높은 작업(장시간 실행), 안정적인 데이터를 처리하는 곳에 적합

### RabbitMQ 구조
- Publisher -> AMQP Broker[Exchange -> Queues] -> Consumer
- Publisher : 발행자는 특정 Exchange에 메시지를 발송한다.
- Exchange : 메시지를 분류에 맞게 Queue로 전달한다.
- Queue : 수신된 메시지를 저장하고 구독자에게 전달한다.
- Consumer : Queue를 구독하고 메시지를 수신한다. 
# topic_demo

`topic_demo`는 ROS 2의 Topic 통신을 가장 단순한 형태로 보여주는 예제 패키지입니다.  
`talker` 노드는 문자열 메시지를 발행하고, `listener` 노드는 같은 토픽을 구독해서 수신 내용을 출력합니다.

## Topic 개념

Topic은 ROS 2에서 가장 기본적인 비동기 메시지 통신 방식입니다.

- Publisher: 데이터를 보내는 노드
- Subscriber: 데이터를 받는 노드
- Message Type: 주고받는 데이터 형식
- QoS: 메시지 전달 방식과 큐 크기 같은 통신 정책

Topic은 발행자와 구독자가 서로를 직접 몰라도 된다는 점이 핵심입니다.  
같은 토픽 이름과 메시지 타입만 맞으면 여러 노드가 느슨하게 연결됩니다.

## 패키지 구성

| 실행 파일 | 노드 이름 | 역할 |
| --- | --- | --- |
| `talker` | `talker_node` | `/chatter` 토픽에 문자열 발행 |
| `listener` | `listener_node` | `/chatter` 토픽 구독 후 로그 출력 |

## 사용 인터페이스

- Topic 이름: `/chatter`
- 메시지 타입: `std_msgs/msg/String`
- 발행 주기: 1초
- QoS depth: `10`

`talker`는 매초 `"Hello ROS2 Topic"` 문자열을 발행합니다.

## 빌드 방법

워크스페이스 루트에서 빌드합니다.

```bash
cd ~/ros2_ws
colcon build --packages-select topic_demo
source install/setup.bash
```

## 실행 방법

터미널 1에서 publisher를 실행합니다.

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run topic_demo talker
```

터미널 2에서 subscriber를 실행합니다.

```bash
cd ~/ros2_ws
source install/setup.bash
ros2 run topic_demo listener
```

## 확인용 ROS 2 CLI 명령

```bash
ros2 topic list
ros2 topic info /chatter
ros2 topic echo /chatter
```

## 실행 흐름

1. `talker`가 `/chatter`에 `String` 메시지를 발행합니다.
2. `listener`가 `/chatter`를 구독하고 메시지를 수신합니다.
3. 수신한 문자열이 터미널 로그로 출력됩니다.

## 학습 포인트

- Topic은 연속적으로 흘러가는 데이터 스트림에 적합합니다.
- 센서 데이터, 상태 정보, 주기적 브로드캐스트에 주로 사용합니다.
- 요청에 대한 즉시 응답이 필요한 경우에는 Service나 Action이 더 적합합니다.

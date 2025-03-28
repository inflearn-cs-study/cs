## Q1. TCP/UDP 뭐가 더 구조가 복잡한지 이유
- TCP가 더 복잡하다. 신뢰성 있는 데이터 전송을 위해 추가적인 필드를 가지고 있기 때문이다.

## Q1-1. 신뢰성 보장을 위한 TCP 헤더의 필드는 무엇이 있나요?
- **응답번호**: 헤더 응답 번호가 직전 패킷의 순서 값이기 때문에 연속적인지 확인해 정상적인 통신이 이루어지고 있는지 확인한다.
- **시퀀스 번호**: 데이터의 순서를 보장하기 위해 사용한다.
- **플래그**: 데이터 전송의 상태를 나타내는 필드로, 데이터 전송의 상태를 확인할 수 있다.

---

## Q2. TCP 전송 시 분리와 재조립 과정
- 데이터 전송 시 세그먼트 단위로 전송하고, 각 블록마다 시퀀스 번호를 부여한다. 
- 수신측에서는 시퀀스 번호를 통해 데이터를 재조립한다.

---

## Q3. TCP 헤더의 요소들 중에서 TCP가 제공하는 흐름 제어와 연관되어 있는 것은?
- **윈도우 크기**: 수신자가 윈도우 크기 값을 통해 수신량을 정할 수 있다.
  → 흐름 제어

---

## Q4. TCP와 UDP 헤더의 공통된 요소
- **발신지와 수신지의 포트 주소**
- **체크섬**: 오류 검출

---

## Q5. HTTP Keep-Alive란?
- 연결을 재사용하여, 하나의 TCP 연결을 통해 여러 개의 HTTP 요청과 응답을 주고받을 수 있도록 해주는 기능이다. 
- 이를 통해 연결 수립과 해제에 따른 오버헤드를 줄일 수 있다.

---

## Q6. TCP Keep-Alive란?
- TCP 계층에서 연결을 확인하기 위해 주기적으로 ACK를 주고받는 행위이다. 
- ACK를 정상적으로 받지 못한다면 OS에서 TCP 연결을 종료한다. 즉, TCP의 Keep-Alive는 OS의 설정에 의해서 관리된다.

---

## Q7. Keep-Alive란 무엇인가?
- Single Connection으로 여러 request, response를 주고받을 수 있게끔 하는 persistent connection을 만드는 기능

---

## Q8. HTTP Keep-Alive의 장점
- **TCP 연결 재사용**: 초기 연결(3-way-handshake)를 여러 번 수행하지 않고 기존의 연결을 재사용한다.
- **연결 설정 오버헤드 감소**
- **데이터 전송 속도 향상**

---

## Q9. HTTP Keep-Alive의 문제점
- **서버 리소스 점유 증가**: 연결이 일정 시간 동안 유지되므로 서버 리소스를 더 많이 점유할 수 있다.
- **적절한 타임아웃 설정 필요** : 너무 긴 타임아웃은 리소스 낭비, 너무 짧은 타임아웃은 연결 재사용 효과를 감소시킨다.
- **불필요한 연결 유지** : 클라이언트가 더 이상 요청하지 않아도 연결이 유지되면 리소스가 낭비될 수 있다.

---

## Q10. HTTP Keep Alive와 TCP Keep Alive의 차이점
- TCP Keep Alive는 OS에 의해 관리되며 HTTP Keep Alive는 Header를 통해서 Client와 Server가 주고 받으며 규약된다.
- TCP Keep Alive는 이 연결이 유효한, 정상적인 연결이 맞는지 확인하는 것을 목적으로 하지만 HTTP Keep Alive는 연결을 일정시간 동안 유지하여 연결을 재사용하는 것을 목적으로 한다.

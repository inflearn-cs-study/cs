# Deadlock(교착 상태)의 개념과 발생 조건 4가지
<img src="https://velog.velcdn.com/images/zioo/post/5289c361-a70e-4208-a58a-ef49dc2922fd/image.png" width="70%">

- 서로 상대방이 사용 중인 자원을 쓰기 위해 무한 대기하며, 더 이상 작업을 진행하지 못하는 상태

### 발생 조건 4가지
1. **상호 배제(Mutual Exclusion)**
    - 자원은 한 번에 한 프로세스만 사용할 수 있어야 함
2. **점유 대기(Hold and Wait)**
    - 프로세스가 할당된 자원을 가진 채 다른 자원을 기다릴 수 있음
3. **비선점(No Preemption)**
    - 다른 프로세스에 할당된 자원을 강제로 빼앗을 수 없음
4. **순환 대기(Circular Wait)**
    - 프로세스 간의 사이클 형태로 자원을 대기하는 상황

# Deadlock을 예방하거나 해결하는 방법
### 1. **Deadlock 예방** - 네 가지 필수 조건 중 하나 이상을 부정하여 방지

- **상호 배제 부정** : 자원을 공유할 수 있도록 함
- **점유 대기 부정** : 프로세스가 실행 전에 모든 자원을 할당받도록 함
- **비선점 부정** : 자원을 강제로 뺏을 수 있도록 함
- **순환 대기 부정** : 자원에 고유한 번호를 할당하고, 번호 순서대로 자원을 요청하도록 함
### 2. **Deadlock 회피** - 교착상태가 발생하지 않는 범위 내에서만 자원을 할당하고 그렇지 않으면 프로세스를 대기시킴

- **은행원 알고리즘**
  - 프로세스가 자원을 요청할 때, 시스템은 자원을 할당한 후에도 안정 상태로 남아있게 되는지를 미리 검사함
  - 안정 상태로 남아있게 되면 자원을 할당하고, 그렇지 않으면 대기시킴
  ###### **안정 상태** : 시스템이 어떤 순서로든지 모든 프로세스의 요청을 만족시킬 수 있는 상태
    - 예시) 안정 상태
          
      || 최대 소요량 | 현재 사용량 | 
      |--------|--------|--------|
      | P0     | 10     | 5      |
      | P1     | 4      | 2      |
      | P2     | 9      | 2      |
          - Available 자원 : 12
          - 안전 순서열 : P1 → P0 → P2
          - 작업 순서
                - P1은 2개가 이미 할당되어 있고, 2개를 추가적으로 할당하여 작업을 끝냄
                - P0은 5(p0가 반납한 4개와 기존에 남은 1개)개를 할당받아 작업을 끝냄
                - P2는 7개를 할당받아 작업을 끝냄
  - **은행원 알고리즘의 단점** 
    - 자원의 최대 요구량을 미리 알아야함.
    - 할당할 수 있는 자원이 고정적이어야함. 유동적이면 안정상태인지 불안정 상태인지 판단하기 어려움.
    - 자원을 할당할 때마다 안정 상태를 유지하는지 확인해야 하므로 오버헤드 발생.

### 3. **Deadlock 탐지** - Deadlock이 발생하면 탐지하고 회복시킴
  - **자원 할당 그래프**
    - 시스템 내의 프로세스가 어떤 자원을 사용하고 있는지, 기다리고 있는지 알 수 있는 그래프
    - 단일 자원을 사용하는 경우 자원 할당 그래프에 사이클이 존재하면 교착상태가 발생한다고 말할 수 있음(다중 자원일 때는 아닐 수 있음)
  - **타임 아웃**
    - 일정 시간 내에 자원을 사용하지 않으면 자원을 반납하도록 하는 방법
### 4. **Deadlock 회복** - Deadlock이 발생하면 회복시킴
  - **프로세스 종료**
    - Deadlock이 발생하면 모든 프로세스를 종료시키는 방법
  - **자원 선점**
    - Deadlock이 발생하면 자원을 선점하여 다른 프로세스에게 할당하는 방법

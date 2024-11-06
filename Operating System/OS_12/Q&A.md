### Q1. 멀티 태스킹과 단점은 무엇인가요?
- 멀티태스킹은 운영체제가 여러 작업을 짧은 시간 간격으로 빠르게 전환하여 동시에 실행되는 것처럼 보이게 하는 방식
- 멀티태스킹의 단점은 잦은 컨텍스트 스위칭으로 인한 오버헤드가 발생해 성능 저하가 있을 수 있습니다. 각 작업의 우선순위 관리가 중요하고 잘못 설정된 우선순위는 기아 상태를 초래할 수 있음

### Q2. 멀티프로세싱이란 무엇이며 장점은? 
- 다수의 프로세서가 협력해서 작업을 처리하는 것. 
- 하나의 프로세서가 고장이나더도 다른 프로세서가 같은 작업을 수행하고 있었기에 하고 있던 작업이 중지되지 않음.

### Q3. 멀티 프로그래밍과 멀티 스레드의 특징
- 멀티 프로그래밍은 CPU 대기시간을 최소화하기에 자원 관리에 효율적이지만 자원 관리가 복잡하고 대기 시간이 길어질 수 있음
- 멀티 스레딩이란 프로세스 안에 스레드를 여러 개 두어서 스레드끼리 번갈아가며 수행하는 것 같은 프로세스 내에서 메모리 공간을 공유하기 때문에 메모리 부분에서 속도가 빠르고 스레드 내에서 병렬적으로 작업을 수행할 수 있다는 장점이 있다. 하지만 단일 프로세스 내에서 여러 개의 스레드가 존재하기 때문에 하나의 스레드에서 오류가 발생하면 전체 프로세스에 영향을 끼칠 수 있다.

### Q4. 멀티프로세싱과 멀티스레딩의 차이점은 무엇인가요? 
- 멀티 프로세싱은 하나의 프로세서는 다운되도 프로그램에 전체에 상관없지만 많은 메모리를 차지함.
- 멀티 스레드는 같은 메모리를 사용하기 때문에 프로세스간 자원 공유보단 빠르지만 하나의 스레드에 문제 생기면 프로세스 전체에 영향이 가고 동기화 문제가 생길 수 있음.

### Q5. 멀티프로세싱 환경에서 자원에 접근할 때 발생하는 동기화 문제 해결하는 방법
- 동기화 기법(뮤텍스, 세마포어 등)을 이용하여 자원에 접근할 때 발생하는 동기화 문제를 해결
###### 뮤텍스는 임계영역에 진입하는 스레드가 다른 스레드에 의해 방해받지 않도록 하는 동기화 기법 
###### 세마포어는 임계영역에 진입하는 스레드의 수를 제한하는 동기화 기법


### Q6.

| 구성                             | 설명                                                                                      | 멀티스레딩                                  | 멀티프로세싱                              | 멀티프로그래밍                                      |
|-------------------------------------|-----------------------------------------------------------------------------------------------|-------------------------------------------------|------------------------------------------------|---------------------------------------------------------|
| 단일코어 CPU + 단일 스레드 + 단일 프로세스 | - 단일 작업만 처리 가능<br>- 병렬성 및 동시성 없음                                       | X                                               | X                                              | X                                                       |
| 2코어 CPU + 2개 스레드 + 1개 프로세스     | - 한 프로세스 내에서 두 개의 스레드가 2개의 코어를 사용<br>- 같은 프로세스 내 동시성 확보 가능 | O (두 스레드가 각기 다른 코어 사용)              | X                                              | X                                                       |
| 2코어 CPU + 1스레드 + 2개 프로세스      | - 2개의 프로세스가 각기 다른 코어를 사용하여 작업 수행<br>- 프로세스 간 병렬성 제공        | X                                               | O                                              | O (두 개의 프로그램 실행 가능)                           |
| 2코어 CPU + 2개 스레드 + 2개 프로세스    | - 각 프로세스에서 각각 두 스레드가 2개의 코어에서 동시에 실행<br>- 동시성과 병렬성 모두 확보 | O (각 프로세스에 스레드 두 개씩)                 | O                                              | O (두 개의 프로그램 실행 가능)                           |

### Q7. 멀티 스레드의 동시성과 병렬성
- 동시성이란 싱글 코어에서 하나의 프로세스 내에서 여러 개의 스레드가 실행될 때 동시에 실행되는 것처럼 보이는 것
- 병렬성이란 멀티 작업을 위해 멀티 코어에서 한 개 이상의 스레드를 포함하는 각 코어들을 동시에 실행하는 것
→ 코어의 개수와 프로세스의 수에 초점

### Q8. 멀티 프로세스와 멀티 스레드가 사용되는 때
- 멀티 프로세스 : CPU가 처리해야하는 task의 특성이 크기가 크면서 개수가 적은 경우, 실시간이 중요하지 않은 일괄 처리
- 멀티 스레드 : CPU가 처리해야하는 task의 특성이 크기가 크지 않으면서 개수가 많을 경우나 실시간이 중요한 웹과 같은 경우


### Q4. 크롬 브라우저에서의 멀티 프로그래밍과 멀티 스레드
- 크롬 브라우져는 멀티 프로세스를 하면서 멀티 스레드를 한다. 
- 각각의 탭들은 프로세스로 구성되어있다. 실제로 작업 관리자를 열어보면 각 탭 별로 프로세스가 실행되고 있는 것을 알 수 있다. 따라서 하나의 프로세스가 죽더라도 다른 프로세스는 살아있는 구조된다. 또한 서로 메모리를 공유하지 않기 때문에 보안적으로 안전하다고 할 수 있다.
- 반대로 하나의 탭의 각 페이지 안에서는 멀티 스레드로 동작하여 각 페이지 안에서 한번에 여러 일을 처리한다. 하나의 다운로드가 끝나지 않았음에도 다른 다운로드를 시작할 수 있고, 이미지 로딩이 끝나지 않아도 그 다음 글들의 로딩이 되어있는 것처럼 멀티 스레드 방식으로 동작하는 것을 알 수 있다
# OS_01 : OS란 무엇이며, 핵심 기능은?

---
#### Process 
- 컴퓨터를 실행할 때 나를 대신하는 무언가
- 키보드, 마우스로 조작하는 대상은 기본적으로 Process
- 우리가 캐릭터를 움직인다고 해서 게임의 월드나 날씨의 정책이 바뀌지 않듯이, 컴퓨터를 키보드, 마우스를 이용해 Process를 통제한다고 한들, 컴퓨터 내부 기본 정책은 바뀌지 않는다.


#### 컴퓨터 구성 3대 요소
- **User** : Daemon(리눅스), Service(윈도우) 등의 시스템 프로세스 | **캐릭터 역할**
- **Kernel** (SW) : 관리, 제어 | **게임 월드**
- H/W : CPU + RAM
---

## 운영체제 
컴퓨터는 피지컬(H/W) + 로지컬(S/W : Kernel + User 영역)으로 이루어져 있다.
여기서 **Kernel + User 영역을 "운영체제"** 라고 부른다.
<img src="http://hongong.hanbit.co.kr/wp-content/uploads/2022/09/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C%EC%9D%98-%ED%81%B0-%EA%B7%B8%EB%A6%BC-e1664436836640.png">


## 운영체제 핵심 기능

### 1. 프로세스 관리
- 프로세스란 실행 중인 프로그램을 의미하며, **운영체제는 이러한 프로세스들이 CPU 시간을 공정하게 사용할 수 있도록 관리**한다. <br>
- 프로세스 스케줄링을 통해 어떤 프로세스가 언제 CPU 를 점유할지, 얼마나 오랜 시간동안 사용할지를 결정하며 효율적으로 시스템 리소스를 배분한다.

### 2. 메모리 관리
- 운영체제는 각 프로그램이 메모리 내에 적절한 공간을 할당받고, 그 공간을 효율적으로 사용할 수 있도록 관리한다. 
- 프로그램의 실행을 위해 필요한 메모리를 할당하고, 사용이 끝난 메모리를 회수한다. 
- 이를 통해 메모리의 낭비를 방지하고 가능한 많은 프로그램이 동시에 실행될 수 있도록 한다.

### 3. 파일 시스템 관리 
- 사용자와 응용 프로그램이 장치를 쉽게 사용할 수 있도록 한다. 

### 4. 장치 관리
- 시스템에 연결된 모든 장치(키보드, 마우스, 프린터 외장 하드드라이브)를 관리한다.

### 5. 사용자 인터페이스
- UI를 제공하여 사용자가 컴퓨터와 상호작용할 수 있도록 한다. 
- CLI(명령줄 인터페이스) 나 GUI(그래픽 사용자 인터페이스) 형태를 취할 수 있다.

### 6. 보안 및 접근 제어 
- 사용자 인증, 접근 권한 설정, 암호화 등의 기능을 통해 무단 접근으로부터 시스템을 보호한다.

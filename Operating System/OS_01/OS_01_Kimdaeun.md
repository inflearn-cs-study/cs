# OS_01 : OS란 무엇이며, 핵심 기능은?

## **운영체제란?**

운영체제(OS, Operating System)는 컴퓨터 시스템의 하드웨어 자원(CPU, 메모리, 저장 장치, 입출력 장치 등)을 관리하고, 사용자와 응용 프로그램이 이러한 자원에 효율적으로 접근할 수 있도록 중재하는 핵심 소프트웨어

운영체제는 하드웨어와 사용자 간의 인터페이스 역할을 하며, 컴퓨터 시스템이 원활하게 동작하도록 보장하며, 사용자에게는 프로그램 실행, 파일 관리, 데이터 저장 및 전송 등을 지원하는 환경을 제공

---

## **운영체제의 구조**

운영체제는 계층적 구조로 이루어져 있으며, 각 계층은 하드웨어와 사용자 사이에서 상호 작용합니다. 주요 구조는 다음과 같습니다:

### **1. 커널(Kernel)**

- 운영체제의 핵심, 하드웨어 자원과 응용 프로그램간의 상호작용을 담당
- 프로세스 스케줄링, 메모리관리, 파일시스템, 입출력장치관리, 보안기능

### 2. 쉘(Shell)

- 사용자와 커널 사이의 인터페이스 역할
- 사용자가 명령어를 입력하면 이를 해석해서 커널에게 전달
- 명령어(CLI) / 그래픽(GUI)기반의 사용자 인터페이스가 있음

### 3. **시스템 호출 인터페이스(System Call Interface)**

- 응용 프로그램이 운영체제의 서비스를 요청할 때 사용하는 인터페이스
- 프로그램은 시스템 호출을 통해 프로세스 관리, 파일 입출력, 메모리 관리 등을 수행

### 4. **유틸리티(Utility Programs)**

- 사용자나 시스템 관리자가 시스템 자원을 관리하는 데 도움을 주는 다양한 도구와 프로그램을 포함

---

## 운영체제의 핵심 기능

### 1. 프로세스 관리

- 실행 중인 프로그램(프로세스)를 생성하고 스케줄링하며 종료하는 역할
- 여러 프로세스가 동시에 실행될 수 있도록 CPU시간을 할당하고 프로세스 간 충돌을 방지

### 2. 메모리 관리

- 각 프로세스가 필요한 만큼의 메모리를 할당하고, 사용이 끝난 메모리는 회수하는 과정을 관리
- 가상 메모리 기술도 지원

### 3. 파일 시스템 관리

- 파일을 디스크에 저장하고, 파일에 대한 read/write 작업을 제. 파일은 디렉토리를 통해 관리

### 4. 입출력(I/O) 장치 관리

- 키보드, 마우스, 프린터, 디스트 드라이버등 입출력 장치와의 데이터 통신을 제어

### 5. 보안 및 권한 관리

- 사용자와 프로세스가 시스템 자원에 접근할 때 적절한 권한 부여하며 불법적인 접근 방지

### 6. 네트워크 관리

- 여러 컴퓨터가 네트워크를 통해 데이터를 주고받을 수 있도록 통신을 관리

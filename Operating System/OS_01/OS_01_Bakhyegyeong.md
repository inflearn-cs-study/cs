# OS_01 : OS란 무엇이며, 핵심 기능은?



## 운영체제

: 사용자가 컴퓨터를 쉽게 다루게 해주는 **인터페이스**

→ 하드웨어와 소프트웨어(유저 프로그램)을 관리한다.

<img src="https://velog.velcdn.com/images%2Fdddooo9%2Fpost%2Fae507c30-a412-4af4-844e-7242fffcd2c6%2Fimage.png">

<br>

운영체제는 <span style="color:LightSkyBlue">**인터페이스(GUI, CUI), 시스템콜, 커널, 드라이버** </span> 부분을 의미한다.

- **시스템콜** : 커널에 접근하기 위한 인터페이스로써 **프로그램이 운영체제의 서비스를 이용하기 위해 커널 함수(fs.readFile() 등)를 호출할 때 사용**된다.
- **커널** : 프로세스 관리, 메모리 관리, 디스크 파일 관리 등 운영체제의 핵심적인 기능을 모아놓은 것
→ 운영체제 전부를 메모리에 올려놓을 수 없으므로 **운영체제 중 필요한 부분만을 메모리에 올려놓은 것**
- **드라이버** : 하드웨어를 제어하기 위한 소프트웨어



> 💡 펌웨어 : 하드웨어를 제어하는 소프트웨어 운영체제 프로그램 <br>
→ 하드웨어와 소프트웨어의 중간 역할로 운영체제와 유사하지만 소프트웨어를 추가로 설치할 수 없다.


## 운영체제의 역할

1. **CPU 스케쥴링과 프로세스 관리** : CPU 소유권 부여 + 프로세스의 생성, 삭제, 자원 할당 및 반환을 관리
2. **메모리 관리** : 한정된 메모리를 어떤 프로세스에 얼마큼 할당할지 관리
3. 디스크 파일 관리 : 디스크 파일을 어떻게 보관할지 관리
4. I/O 디바이스 관리 : I/O 디바이스(마우스, 키보드)와 컴퓨터간에 데이터를 주고받는 것을 관리
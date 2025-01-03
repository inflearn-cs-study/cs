### Q1. 아파치와 톰캣의 차이점은 무엇인가요?
- 아파치는 정적 콘텐츠(HTML, CSS, JavaScript) 처리가 주 목적인 웹 서버입니다.
- 톰캣은 서블릿을 처리하는 웹 애플리케이션 서버(WAS)입니다.
- 아파치는 멀티 프로세스 방식으로 동작하며, 톰캣은 멀티 스레드 방식으로 동작합니다.

### Q2. 아파치와 톰캣을 함께 사용하는 이유는 무엇인가요?
- 아파치가 정적 콘텐츠를 효율적으로 처리하고, 톰캣이 동적 콘텐츠(JSP, 서블릿)를 처리하도록 분리하여 성능을 최적화할 수 있습니다. 
- 아파치의 로드 밸런싱 기능을 통해 톰캣 서버의 부하를 분산시킬 수 있습니다.

### Q3. 톰캣은 멀티 프로세스인가 멀티 스레드인가
- 톰캣은 WAS로 jsp, servlet 같은 동적 데이터를 관리하며 멀티 스레드 방식으로 동작합니다.
- 요청을 처리하기 위한 Thread Pool을 관리하며 요청이 들어오면 Thread Pool 내에서 스레드를 제공해 요청을 처리합니다. 
- 스레드간 메모리를 공유하기에 응답 속도가 빠르고 메모리 사용에 효율적입니다.

### Q4. 아파치는 멀티프로세스인지 멀티 스레드인지 설명해주세요.
- 아파치는 멀티 프로세스 방식으로 동작하며, 설정에 따라 멀티 스레드로 운용 가능합니다.
- 정적 데이터를 주로 처리. 각 요청에 대해 별도의 프로세스를 생성하여 처리합니다. 

### Q5. 톰캣의 서블릿 컨테이너 역할은 무엇인가요?
- 클라이언트의 요청을 받아 서블릿을 실행하고 응답을 생성하여 클라이언트에게 반환합니다.

### Q6. 톰캣에서의 연결 풀(Connection Pool)이란 무엇인가요?
- 데이터베이스와의 연결을 미리 생성해두고 재사용하여 성능을 향상시키는 기술입니다. 
- 연결 풀을 사용하면 데이터베이스와 연결하고 해제하는 오버헤드를 줄일 수 있습니다.

### Q7. 톰캣을 경량 서버라고 부르는 이유는?
- 톰캣은 서블릿 컨테이너만 있는 웹 애플리케이션 서버로, 다른 WAS에 비해 경량화되어 있어서 경량 서버라고 불립니다.

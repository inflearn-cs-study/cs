## 스레싱

: 메모리의 **페이지 폴트율이 높아 CPU 이용률이 급격하게 떨어지는 현상**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F24388A4057188EAD38)

**프로세스를 처리하는 시간보다 페이지 폴트로 인한 페이지 교체에 소모되는 시간**이 더 많아지면 CPU의 이용률이 감소된다.

운영체제는 CPU의 가용성을 높이기 위해 더 많은 **프로세스를 메모리에 올리게** 되는데 동시에 실행되는 프로세스가 많아질수록 **각 프로세스에 할당되는 페이지는 작아지게 되면서 악순환이 반복**된다.

### 해결방법

1. 메모리 증가시키기
2. HDD를 SSD로 바꾸기
3. **작업 세트 (Working Set)** : 프로세스의 과거 사용 이력인 지역성을 통해 결정된 **페이지 집합을 만들어 미리 메모리에 로드하는 것**
    
    → **자주 참조되는 페이지들을 묶어 메모리에 동시에 올라갈 수 있도록 보장**하는 관리 방법
    
    > 💡 페이지 : 논리 주소에서의 메모리의 주소를 나타내는 단위 <br>
    → 물리 주소에서는 프레임이라 부른다.
    
    
4. **PFF (Page Fault Frequency)** : 페이지 폴트 빈도를 조절하는 방법
    
    → 프로세스의 페이지 폴트율을 주기적으로 조사하고 이 값에 근거해 각 **프로세스에 할당할 메모리 양을 동적으로 예측하고 조절**한다.
    
    → 상한선과 하한선이라는 기준에 따라 **운영체제가 메모리에 올라가 있는 프로세스의 수를 조절**한다.
    
# 아이템 48 : 스트림 병렬화는 주의해서 적용하라

# 동시성 프로그래밍

1. 릴리스 : 스레드, 동기화, wait/notify를 지원
    - wait : 갖고 있던 고유 락을 해제, 스레드를 대기 상태로 전환
    - notify : 대기 상태의 스레드들 중 임의로 하나를 실행
2. 자바 5 이후 : 동시성 컬렉션인 `java.util.concurrent` 라이브러리와 실행자(Executor) 프레임워크 지원
3. 자바 7 이후 : 고성능 병렬 분해 프레임워크인 포크-조인(fork-join) 패키지를 추가
4. 자바 8 이후 : parallel 메서드를 통해 병렬 실행이 가능한 스트림 지원

동시성 프로그래밍을 할 때는 항상 **안전성(safety)와 응답 가능(liveness) 상태를 유지**해야 하는 것에 주의해야 한다.

## 동시성 프로그래밍 주의점

```java
public class ParallelMersennePrimes {
    public static void main(String[] args) {
        primes().map(p -> TWO.pow(p.intValueExact()).subtract(ONE))
                .parallel() // 스트림 병렬화
                .filter(mersenne -> mersenne.isProbablePrime(50))
                .limit(20)
                .forEach(System.out::println);
    }

    static Stream<BigInteger> primes() {
        return Stream.iterate(TWO, BigInteger::nextProbablePrime);
    }
}
```

무작정 성능을 향상시키기 위해 `parallel()` 를 사용하면, 위와 같이 아무것도 출력하지 못하면서 CPU는 `90%` 나 잡아먹는 상태가 무한히 계속되는 문제가 발생할 수 있다.

→ 스트림 라이브러리가 이 파이프라인을 병렬화하는 방법을 찾아내지 못했기 때문이다.
→ **데이터 소스가 `Stream.iterate`인 경우**나 **중간 연산으로 `limit` 을 사용하는 경우**에는 파이프라인 병렬화로는 성능 개선을 기대할 수 없다.

> ⭐
>
> **파이프라인 병렬화**는 limit를 다룰 때 **CPU 코어가 남는다면 원소를 몇 개 더 처리한 후 제한된 개수 이후의 결과를 버려도 아무런 해가 없다고 가정**한다.
>
> → 위의 코드에서는 새롭게 소수를 찾을 때마다 그 전 단계보다 시간이 2배 정도 걸린다.
>
> → **원소 하나를 계산하는 비용이 그 이전까지의 원소 전부를 계산한 비용을 합친 것**만큼 소모된다.


## 적절한 스트림 병렬화 사용처

대체로 스트림의 소스가 `ArrayList`, `HashMap`, `HashSet`, `ConcurrentHashMap`의 인스턴스거나 `배열`, `int 범위`, `long 범위`일 때 병렬화의 효과가 가장 좋다.

1. 정확성 <br> : **모두 데이터를 원하는 크기로** **정확하고 손쉽게 나눌 수 있다.** <br>
    → 일을 다수의 스레드에 분배하기에 좋다.

1. 참조 지역성
    
    : 이웃한 원소의 참조들이 메모리에 연속해서 저장되어 있다.
    
    → **참조 지역성이 높으면 캐시에서 데이터를 바로 찾을 수 있으므로 속도가 빨라지지만**, 낮다면 주 메모리에서 캐시로 다시 로드하는 과정이 필요하기 때문에 성능이 낮아진다.
    

## 종단 연산과 병렬화

종단 연산에서 수행하는 작업량이 **파이프라인 전체 작업에서 상당 비중을 차지하면서 순차적인 연산**이라면, 파이프라인 병렬 수행의 효과가 떨어진다.

### 적합한 종단 연산

- 파이프라인에서 만들어진 원소를 하나로 합치는 축소 메서드
    
    ex) reduce, min, max, count, sum
    
- 조건에 맞으면 바로 반환되는 메서드
    
    ex) anyMatch, allMatch, noneMatch
    

### 부적합한 종단 연산

- 컬렉션들을 합치는 부담이 큰 가변 축소 메서드
    
    ex) collect
    

## 핵심 정리

- 계산도 올바로 수행하고 성능도 빨라질 거라는 확신 없이는 스트림 파이프라인 병렬화는 시도조차 하지 말라.
- 잘못되면 오동작하게하거나 성능을 급격히 떨어뜨린다.
- 테스트 후에, 계산도 정확하고 성능도 좋아졌음이 확실해졌을 때, 오직 그럴 때만 병렬화 버전 코드를 운영 코드에 반영하라.
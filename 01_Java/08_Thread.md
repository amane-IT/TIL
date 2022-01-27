# Thread

> Process
> > 실행 중인 하나의 프로그램
> > 하나 이상의 Thread로 구성

> Thread
> > Process의 실행 단위
> > CPU + Code + Data로 구성
> > > CPU는 한 번에 한 가지 일만 수행 가능
> > 다중 스레드 지원

## Life Cycle
- new Thread() -> ** start() ** -> 스레드 실행
- Runnable -> 작업 실행 중인 것으로 간주 -> ** run() **
  + run() -> Java Thread Scheduler가 실행
- 실행 중이다가 CPU에 새로운 일이 들어오면 sleep후 일 처리
- Runnable -> Running -> Timed Waiting -> Runnable의 반복
- 일이 끝나면 Terminate


## 장점
- CPU 효율성 증가
- Thread 생성이 Process 생성보다 빠름
  + Process보다 Thread의 비용이 더 적음
  + 메모리 점유 공간이 작음
- 통제 쉬움
- 기존 정보와의 공유가 쉬움

- - -

## 구현법
### 구현법 1
1. java.lang.Thread 상속받은 클래스 선언
2. run() Overriding 하여 재정의
3. 1에서 선언한 클래스 객체를 main()에 생성
4. 생성한 객체의 start() 호출


### 구현법 2
1. 다른 클래스를 상속받고 있어 java.lang.Thread를 상속받지 못하는 경우인지 확인
2. Runnable 인터페이스를 상속받는 클래스 선언
3. Runnable 인터페이스의 run() 재정의
4. 2의 Runnable 객체를 main()에 생성
5. Runnable 객체로 java.lang.Thread 클래스의 객체 생성 -> 생성자 arg에 주입
6. 5번에서 생성한 객체의 start() 호출
  + run() 직접 호출하면 안됨 -> **Thread 스케줄러가 run() 호출**

<br>
- - -

## join()
- A 스레드의 run()에서 B 스레드의 join()을 호출하려면 B 스레드의 작업이 종료되거나 지정된 시간이 지날 때까지 A 스레드가 Waiting 상태가 됨
- A has B 관계일 경우 join() 사용 가능
- B 스레드 먼저 실행 후, A 스레드가 실행 됨

``` java
B.run(){
  A.join(2000);
}
```

## 멀티 스레드와 동시성 문제
- 하나의 Data 객체를 여러 스레드에서 동시에 접근하면 올바른 Data가 유지되지 않을 수 있다.
- 동기화(순서 처리)로 해결
  + 모든 객체는 Lock flag를 가지고 있음
  + sychronized 키워드가 붙어있으면 Lock flag가 있어야 접근 가능
  + 처음 만난 A 스레드가 Lock flag를 얻고 로직 수행
  + 다음에 온 B 스레드는 Lock flag를 얻지 못해 로직 수행 불가 (Blocked -> runnable)
  + A 스레드가 로직 수행이 끝나면 Lock flag를 synchronized에 반납 후 terminated
  + 그 다음 온 스레드가 Lock flag를 얻고 로직 수행 ...

- 결론적으로 순서대로 스레드가 수행되면서 올바른 Data 유지
- Synchronized 블록 = Critical Section


- - -
## Synchronized Method
- 공유 데이터에 접근하는 메서드를 synchronized 키워드로 정리
- 하나의 스레드만 접근 가능
- 나머지 스레드는 대기
- 객체에 동기화가 일어남
  + 객체에 접근하고자 하는 다른 스레드의 대기시간이 길어짐
  + 성능저하로 이어짐


## Synchronized Block
- 꼭 필요한 객체 사용 부분만 동기화
- 공유 데이터에 접근하는 영역을 블록화
- 메서드 전체 처리 대비 성능 향상


=> Block 상테의 스레드가 낭비됨


- - -
## Block상태의 낭비되는 스레드를 줄이는 방법

### wait()
- 스레드 객체가 현재 작업을 할 수 없으면 대기상태로 만듦
- 작업 중이던 객체는 자원을 반납 후 대기 상태로 전환
- notify()가 있어야 다시 작업할 수 있음

### notify()
- 대기 상태의 스레드 객체가 작업할 수 있는 상황이 되었을 때, 호출
- 작업 재개 시킴
- wait()된 스레드를 복구



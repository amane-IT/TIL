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


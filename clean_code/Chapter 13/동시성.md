# Clean Code - 13.  동시성

Created: January 15, 2022
Created by: Lee Anne
Tags: Clean Code

## 동시성이 필요한 이유?

- 동시성은 ***결합을 없애는 전략***. What과 When을 분리하는 전략.
- 단일 스레드는 프로그램 스택을 통해 상태가 곧바로 드러난다.
- 대표적인 예로는 서블릿(Servlet). 컨테이너 아래에서 실행되면서 동시성을 `부분적`으로 관리(비동기로 호출)But, 동시성을 잘 관리해주어야 한다는건 사실!
- 동시성은 필요한 상황에만 적절하게 적용할 때 도움이 된다.(성능 향상에 지대한 영향...!)

## 주의사항

- 동시성 적용 시 몇 가지 사항을 고려해야 한다.
    - 동시성은 다소 부하를 유발한다.
    - 동시성은 복잡하다.
    - 일반적으로 동시성 버그는 재현하기 어렵다.
    - 동시성을 구현하려면 흔히 근본적인 설계 전략을 재고해야 한다.

## 동시성 방어원칙

- 동시성 코드는 다른 코드와 분리해라!(SRP)
- 공유 자원을 최대한 줄이고 자료를 ***캡슐화***하라!(synchronized 성능 이슈)
- 스레드는 가능한 독립적으로 동작할 수 있도록 구현하라!
- 동기화는 최대한 작게!(synchronized)
- **스레드는 생성해서 실행시키는 것보다 중단하는게 더 어렵다. 이 부분을 신경써서 가져가기!(자바 병렬 프로그래밍 공부에 나오는 내용! 학습중)**
- 스레드 코드 테스트를 진행하라! → 성능에 부하를 많이 주면서 잠정적으로 버그나 에러가 발생하는지 체크

> ***여기서 질문: 책에 보면 POJO를 스레드에 많이 집어넣어서 테스트하라는데 이게 무슨 소리일까...?***
> 
- 스레드 테스트를 진행할 때 수동으로 테스트 작성하면 실수할 가능성이 많다. 자동화 방식을 고려할 것!(`이때, 핵심은 스레드 관계없이 순수 자바 코드만 다루는 POJO와 스레드 작업 관련 코드를 분리하여 테스트하기`)
- 자바 라이브러리를 이해하여 적극 활용하자!
    - OpenJDK 5부터 Thread Safe 한 컬렉션 제공(Executor, Concurrent, Atomic, Locks 등)
- 자주 접할 수 있는 동시성 이슈 알고리즘 ⇒ `해당 문제들은 monitor 기술에 의해 해결이 가능하다`
    1. Producer-Consumer : `한정 버퍼 문제` 라고도 한다.
        1. 버퍼를 동기화시킴으로써 문제를 해결할 수 있음.(with mutex 세마포어)
        2. 간단한 어플리케이션에서는 Java 기준 Blocking Queue 컬렉션으로 해결이 가능하지만 이럼에도 자원 관리가 제대로 되지 않을 적에는 세마포어 적용할 수 있음.
        3. 예제 코드
            
            ```java
            package thread;
            
            public class ProducerConsumer {
            
                static final int N = 100;
                static producer p = new producer();
                static consumer c = new consumer();
                static our_monitor mon = new our_monitor();
                public static void main(String args[]) {
                    p.start();
                    c.start();
                }
            
                static class producer extends Thread {
                    public void run() {
                        int item;
                        while (true) {
                            item = produce_item();
                            mon.insert(item);
                        }
                    }
                }
            
                static class consumer extends Thread {
                    public void run() {
                        int item;
                        while (true) {
                            item = mon.remove();
                            consume_item(item);
                        }
                    }
                }
            
                static class our_monitor {
                    private int buffer[] = new int[N];
                    private int count = 0, lo = 0, hi = 0;
                    public synchronized void insert(int val) {
                        if (count == N) go_to_sleep();
                        buffer[hi] = val;
                        hi = (hi + 1) % N;
                        count = count + 1;
                        if (count == 1) notify();
                    }
                    public synchronized int remove() {
                        int val;
                        if (count == 0) go_to_sleep();
                        val = buffer[lo];
                        lo = (lo + 1) % N;
                        count = count - 1;
                        if (count == N - 1) notify();
                        return val;
                    }
                    private void go_to_sleep() {
                        try {
                            wait();
                        } catch(InterruptedException e) {} ;
                    }
                }
            
                public static int produce_item() {
                    return 1;
                }
            
                public static void consume_item(int item) {
                    item -= 1;
                }
            }
            ```
            
    2. Dining Philosophers
        1. 하나의 테이블에 5명의 철학자들이 식사를 할 경우를 빗대어 표현
        2. 한정된 메모리 자원을 1개 이상의 스레드가 사용하고자 할 때 발생하는 이슈(Deadlock or Starvation)
        3. 예제 코드
        
        ```java
        do {
        	wait(chopstick[i]);
        	// n = 사용 가능한 자원의 수
        	wait(chopstick[(i+1) % n];
        	...
        	signal(chopstick[i]);
        	signal(chopstick[(i+1) % n];
        	...
        } while(true)
        ```
        
    3. Readers-Writers
        1. 데이터베이스에서 Read session과 Write session이 동시다발적으로 접속했을 때 Write process만 임계 영역에 접근할 수 있어 Lock을 걸게 되면 나머지 Read process들이 무한대기상태에 빠지는 경우
        2. 예제 코드
        
        ```java
        do {
        	wait(wrt);
        	...
        	// writing is performed
        	signal(wrt);
        } while(true)
        ```
        

## 참고자료

- 애플리케이션 성능 측정에 있어선 두 가지 측면에서 접근 가능
    - CPU bound: 프로세서 성능이 특정 이유(수치 계산, 정규 표현식 계산, GC 등)로 인해 사용량이 많아 성능에 이슈를 줄 경우
    - I/O bound: 잦은 디스크 I/O, 페이지 스와핑, 소켓 사용 등으로 인하여 디스크 접근 시도가 많아 성능에 영향을 주는 경우
- CPU bound로 인한 성능 이슈가 있을 경우 무조건 멀티 스레딩 프로그램으로 구현한다고 해결되지 않는다. CPU 사이클은 근본적으로 한계가 있으므로 오히려 하드웨어를 업그레이드(Scale-Up) 해줘야 한다.

## 깜짝 Quiz~!

아래 사진의 코드는 Clean Code일까요...?!

![KakaoTalk_Photo_2022-01-29-00-30-01](https://user-images.githubusercontent.com/15176192/153567528-382d77dc-4353-4613-893e-8d88b26bb25e.jpeg)

*A. process(final Socket socket) 메소드 안에서 현재 4개의 역할을 하고 있기에 단일 책임 원칙을 위반하므로 해당 코드는 Clean Code가 아니다!*

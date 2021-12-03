## -목표

###### 자바의 멀티쓰레드 프로그래밍에 대해 학습하세요.



## 학습할 것

- Thread 클래스와 Runnable 인터페이스
- 쓰레드의 상태
- 쓰레드의 우선순위
- Main 쓰레드
- 동기화
- 데드락



## 학습 내용 정리

#### - Thread 클래스와 Runnable 인터페이스

> * Thread 클래스
>
>   * ```java
>     public class ThreadSample1{
>         public static void main(String[] args){
>             Thread t = new Thread();
>             t.start(); // 아무것도 하지 않은 스레드가 생성 후 바로 소멸
>         }
>     }
>     
>     // 원하는 작업을 수행하는 스레드를 만들기 위해선 Thread 클래스의 run() 메소드를 오버라이딩해야 함.
>     
>     public class ThreadSample2 Thread{
>         public static void main(String[] args){
>         	ThreadSample2 sample2 = new ThreadSample2();
>             sample2.run();
>     	}
>         
>         // Thread 클래스의 run 메소드 오버라이딩
>         public void run(){
>             System.out.println("New Flow, new thread is running");
>         }
>     }
>     // extend 키워드로 Thread 를 상속받아 Thread() 클래스의 run() 메소드르 오버라이딩해서 새로운 일을 하도록 재정의
>     ```
>
> * Runnable 인터페이스
>
>   * 반드시 implements 키워드를 사용해서 구현해야 함.
>
>   * run()  메소드가선언되어 있어 구현 클래스는 반드시 그 내용을 구현해야 한다.
>
>   * ```java
>     public class ThreadSample3 implements Runnable{
>         public static void main(String[] args){
>             // ThreadSample3는 Runnable 인터페이스의 구현 클래스이므로 아래와 같이 Runnable r로 업캐스팅 가능.
>             Runnable r = new ThreadSample3();
>             Thread t = new Thread(r);
>             t.start();
>         }
>     }
>     ```

#### - 쓰레드의 상태

> * 스레드는 상황에 따라 여러상태를 옮겨 다니며 작업을 수행하기 때문에 start() 메서드를 호출하자 마자실행되지 않는다.
>
> * 스레드의 start() 메소드를 실행하면 '실행 가능한 상태(Runnable)'로 변경되고, 그 다음 스레드 스케줄러의 의해 '실행상태(Running)'로 변경된 후에야 비로소 실행된다.
>
> * > CREATE --> Runnable <--> Running --> Done
>   >
>   > ​                                 |^                 |
>   >
>   > ​                          WAITING, BLOCKED
>
>   * CREATE:
>     * Thread 객체를 인스턴스 했을 때의 상태.
>     * Thread 객체의 start() 메소드가 아직 호출되기 전이다.
>   * Runnable
>     * 인스턴스된 스레드 객체의 start() 메소드가 호출되었을 때의 상태.
>     * 보통 실행 가능한 상태라고 하며 스레드의 실행 주기가 시작되는 상태이기도 하다
>   * Running
>     * 스레드 객체가 실제로 동작하는 단계
>     * 스레드 스케줄러가 스레드 풀에서 실행시킬 목적으로 객체를 뽑는 경우에 Running 상태로 변경되어 run() 메소드가 실행된다
>   * Waiting, Blocked
>     * 대기하고 있는 상태.
>     * 실제 동작하고 있지 않은 상태이며 notify() 메소드에 의해 다시 깨어날 수 있다.
>     * 깨어난 스레드는 다시 Runnable 상태로 변경되어 작업 처리 가능
>   * Done
>     * run() 메소드가 그 역활을 다 했을 때 스레드 객체 종료.

#### - 쓰레드의 우선순위

> * 스레드 우선 순위를 조정하여 스레드가 얻는 실행 시간을 조정 가능.
>
> * 우선 순위는 1~10까지 설정 가능하며 값이 높을수록 우선 순위는 높아짐.
>
> * 기본값은 NORM_PRIORITY 변수값.
>
> * ```java
>   public final static int MIN_PRIORITY = 1;
>   public final static int NORM_PRIORITY = 5;
>   public final static int MAX_PRIORITY = 10;
>   ```
>
> * ```java
>   public class ThreadSample9 implements Runnable{
>       private String mark;
>       
>       public ThreadSample9(String mark){
>           this.mark = mark;
>       }
>       
>       public static void main(String[] args){
>           Thread th_prio1 = enw Thread(new ThreadSample9("-"), "Prio1");
>           Thread th_prio5 = enw Thread(new ThreadSample9("/"), "Prio5");
>           Thread th_prio10 = enw Thread(new ThreadSample9("*"), "Prio10");
>           
>           th_prio1.setPriority(Thread.MIN_PRIORITY);
>           th_prio5.setPriority(Thread.NORM_PRIORITY);
>           th_prio10.setPriority(Thread.MAX_PRIORITY);
>           
>           th_prio1.start();
>           th_prio5.start();
>           th_prio10.start();
>       }
>       
>       @Override
>       public void run(){
>           for(int i=0; i<200; i++){
>               System.out.println(mark);
>               for(int j=0; j<10000; j++)
>                   ; // 작업 지연
>           }
>           System.out.println(Thread.currentTHread().getName() + " done");
>       }
>   }
>   
>   // 실행결과
>   -/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*-/*
>   //////////////////////////////////////////////////////
>   //////////////////////////////////////////////////////
>   /////////*********************************************
>   ******************************************************
>   *********************************************---------
>   ------------------------------------------------------
>   ------------------------------------------------------
>   -----------------------Prio5 donePrio1 donePrio10 done
>   ```

#### - Main 쓰레드

> ```java
> public static void main (String[] args) {
> 	// 코드 작성
> }
> ```

#### - 동기화

> * 목적: 멀티 스레딩을 사용해서 보다 빠른 작업을 처리하기 위해서.
>
> * 상호 배타적 처리
>
> * 동기화는 오직 하나의 스레드만이 공유 자원에 대한 접근을 허락한다.
>
> * 자바 동기화에 필요한 것은 synchronized 구문과 스레드 락(Lock)이다.
>
>   * ```java
>     // 메소드에 키워드를 선언하는 방법: 동기화 메소드
>     [제어자] synchronized [반환값] [메소드 이름] () { // 공유 자원 변경 }
>         
>     // 메소드 내부에 키워드를 선언하는 방법: 동기화 블록
>     [메소드 선언부]{
>         synchronized ( [락 객체] ){
>             // 공유 자원 변경
>         })
>     }
>         
>     사용예: // 동기화 메소드의 예제
>     public synchronized void reportCurrentStatus(){
>         // 구문
>         // 동기화 블록의 예제
>         public void reportCurrentStatus(){
>             synchronized (this){
>             // 공유 자원 변경
>         }
>     }
>     ```
>
>   *  락 객체는 문지기 역할을 해서 오직 하나의 스레드만이 동기화 블록에 접근할 수 있다.
>
>   * 동기화 부작용: 병목 현상

#### - 데드락

> * 교착상태
> * 둘 이상의 스레드가 lock을 획득하기 위해 대기할때, 이 lock을 잡고 있는 스레드들도 똑같이 다른 lock을 기다리면서 서로 block 상태에 놓이는 것.




전체 출처: 자바를 다루는 기술, 자바의 정석

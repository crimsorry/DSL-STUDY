## -목표

###### 자바의 예외 처리에 대해 학습하세요.



## 학습할 것

- 자바에서 예외 처리 방법 (try, catch, throw, throws, finally)
- 자바가 제공하는 예외 계층 구조
- Exception과 Error의 차이는?
- RuntimeException과 RE가 아닌 것의 차이는?
- 커스텀한 예외 만드는 방법



## 학습 내용 정리

#### - 자바에서 예외 처리 방법 (try, catch, throw, throws, finally)

> * try-catch-finally 문
>
>   * ```java
>     try{
>         // Exception 객체를 발생시킬 수 있는 구문
>     }catch(NumberFormatException nfe){
>         // catch 구문에서 정의한 예외 객체가 발생하면 처리할 구문
>     }catch(IOException e){
>         // catch 구문에서 정의한 예외 객체가 발생하면 처리할 구문2
>     }finally{
>         // 예외 발생 여부와 상관없이 반드시 처리할 구문
>     }
>     ```
>
>   * 하나의 try 블럭 다음에는 여러 종류의 예외를 처리할 수 있도록 하나 이상의 catch 블록이 올 수 있으며, 이 중 발생한 예외의 종류와 일치하는 단 한 개의 catch 블럭만 수행된다.
>
>   * 발생한 예이의 종류와 일치하지 않는 catch 블럭이 없으면 예외는 처리되지 않는다.
>
>   * if 문과는 달리 try 블럭이나 catch 블럭 내에 포함된 문장이 하나뿐이어도 **괄호{}를 생략할 수 없다.**
>
>   * **finally** 의 경우 상황에 따라서 **생략이 가능**하다.
>
> * throw
>
>   * throw 키워드는 새로운 Throwale 객체를 던질 때 사용
>
>   * ```java
>     throw new Exception ("Wrong parameter format");
>     throw new ArithmeticException;
>     ```
>
> * throws
>
>   * 이 메소드를 실행함녀서 내부에 발생한 예외를 JVM에게 던지는 기능을 담당
>
>   * ```java
>     public void runTest() throws Exception{
>         ///
>     }
>     
>     public void calculate() thrwos ArithemeticException, ClassNotFoundException{
>         ///
>     }
>     ```



#### - 자바가 제공하는 예외 계층 구조

> Object 
>
> > Throwable : 모든 오류의 최상위 클래스. 이 클래스를 상속받아야 JVM에게 예외 객체로 던져져 예외처리 가능.
> >
> > > Exception
> > >
> > > RuntimeException
> > >
> > > > ClassCastException
> > > >
> > > > ArithmeticException
> > > >
> > > > NegativeSizeException
> > > >
> > > > NullPointerException
> > > >
> > > > ArrayStoreException
> > > >
> > > > IndexOutOfBoundException
> > > >
> > > > ecurityException
> > >
> > > CloneNotSupportException
> > >
> > > IllegalAccessException
> > >
> > > IntantiationException
> > >
> > > NosuchMethodException
> > >
> > > ClassNotFoundException
> > >
> > > IOException
> > >
> > > > EOFException
> > > >
> > > > FileNotFOundException
> > > >
> > > > InterupttediException
> >
> > Error
> >
> > > LinkageError
> > >
> > > THreadDeath
> > >
> > > VirtualMachineError



#### - Exception과 Error의 차이는?

> * Exception
>   * 처리 가능한 오류들
> * Error
>   * 프로그램에 치명적인 에러를 대표



#### - RuntimeException과 RE가 아닌 것의 차이는?

> * RuntimeException
>   * JVM에서 연산 혹은 논리 작업을 할때 발생할 수 있는 예외를 의미.
>   * 이 예외의 특징은 try-catch 구문으로 예외 처리를 하지 않아도 자동으로 예외처리가 된다는 것.
>   * Unchecked Exception
>   * 만약 예외처리를 하지 않는다면 컴파일 시 에러가 발생하여 실행 불가능.
>   * RuntimeException 관련 예외들은 개발자의 실수로 인해 많이 발생하므로 코드 작성에 주의 필요
>   * 프로그램 내부의 원인에 의해 발생하는 예외
> * Re 가 아닌 클래스
>   * 반드시 try-catch로 작성 필요
>   * Checked Exception



#### - 커스텀한 예외 만드는 방법

> 1. 새로운 Exception 클래스는 반드시 Throwable 클래스를 상속
>
>    * Throwable 클래스를 상속해야 다른 메소드에 의해 throw 혹은 throws 키워드 사용하여 예외를 던질 수 있음
>
> 2. 가능하면 Exception 클래스의 생성자를 모두 오버라이딩 하기
>
>    * ```java
>      public class homeException extends Exception{
>          private static final long serialVersionUID = -54168765216541L;
>          
>          public homeException(){
>              super();
>          }
>          
>          public homeException(String message){
>              super(message);
>          }
>          
>          public homeException(String message, Throwable cause){
>              super(message, cause);
>          }
>          
>          public homeException(Throwable cause){
>              super(cause);
>          }
>      }
>      ```
>
>    * 커스텀할 예외 클래스는 단계적으로 스택 구조를 가져야 한다.
>
>    * 그러므로 기본적인 생성자를 모두 오버라이딩하여 Exception 처리 구조를 벗어나지 않도록 해야한다.




전체 출처: 자바를 다루는 기술, 자바의 정석

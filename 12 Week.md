## -목표

###### 자바의 애노테이션에 대해 학습하세요.



## 학습할 것

- 애노테이션 정의하는 방법
- [@retention](https://github.com/retention)
- [@target](https://github.com/target)
- [@documented](https://github.com/documented)
- 애노테이션 프로세서



## 학습 내용 정리

#### - 애노테이션 정의하는 방법

> * 애노테이션
>
>   * 프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것이 바로 애너테이션이다.
>
>   * 주석처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에 유용한 정보를 제공할 수 있다는 장점이 있다.
>
>   * ```java
>     @Test
>     public void method(){
>         
>     }
>     ```

#### - @retention

> * 애너테이션이 유지되는 범위를 지정하는데 사용한다.
>
> * | 유지 정책 | 의미                                             |
>   | --------- | ------------------------------------------------ |
>   | SOURCE    | 소스 파일에만 존재. 클래스파일에는 존재하지 않음 |
>   | CLASS     | 클래스 파일에 존재. 실행시에 사용불가. 기본값    |
>   | RUNTIME   | 클래스 파일에 존재. 실행시에 상용가능.           |
>
> * 컴파일러를 직접 작성할 것이 아니면, 이 유지정책은 필요없다.

#### - @target

> * 애너테이션이 적용 가능한 대상을 지정하는데 사용한다.
>
> * 애너테이션이 적용가능한 대상을 지정한느데 사용됨.
>
> * ```java
>   @Target({TYPE, FIELD, METHOD, PARAMETER, CONSTUCTOR, LOCAL_VARIABLE})
>   @Retention(RetentionPolicy.SOURCE)
>   public @interface SuppressWarnings{
>       String[] value();
>   }
>   ```
>
> * | 대상 타입       | 의미                            |
>   | --------------- | ------------------------------- |
>   | ANNOTATION_TYPE | 애너테이션                      |
>   | CONSTRUCTOR     | 생성자                          |
>   | FIELD           | 필드(멤버변수, enum상수)        |
>   | LOCAL_VARIABLE  | 지역변수                        |
>   | METHOD          | 메서드                          |
>   | PACKAGE         | 패키지                          |
>   | PARAMETER       | 매개변수                        |
>   | TYPE            | 타입(클래스, 인터페이스, enum)  |
>   | TYPE_PARAMETER  | 타입 매개변수(JDK1.8)           |
>   | TYPE_USE        | 타입이 사용되는 모든 곳(JDK1.8) |

#### - @documented

> * 애너테이션 정보가 javadoc으로 작성된 문서에 포함되게 한다.
>
> * 자바에서 제공하는 기본 애너테이션 중에 '@Override' 와 '@SuppressWarnings'를 제외하고는 모두 이 메타 애너테이션이 붙어있다.
>
> * ```java
>   @Documented
>   @Retention(RetentionPolicy.RUNTIME)
>   @Target(ElementType.TYPE)
>   public @interface FunctionalInterface{}
>   ```

#### - 애노테이션 프로세서

> * 여러 라운드(rounds)에 거쳐 소스 및 컴파일 된 코드를 처리 할 수 있다.



전체 출처: 자바를 다루는 기술, 자바의 정석


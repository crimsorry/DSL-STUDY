## -목표

###### 자바의 열거형에 대해 학습하세요.



## 학습할 것

- enum 정의하는 방법
- enum이 제공하는 메소드 (values()와 valueOf())
- java.lang.Enum
- EnumSet



## 학습 내용 정리

#### - enum 정의하는 방법

> * enum(열거형)
>
>   * 서로 관련된 상수를 편리하게 선언하기 위한 것으로 여러 상수를 정의할 때 사용함녀 유용하다.
>
>   * JDK1.5부터 추가.
>
>   * ```java
>     class Test1{
>     	static final int one = 0;
>     	static final int two = 1;
>         static final int three = 2;
>         static final int four = 3;
>             
>         static final int good = 4;
>         static fint int think = 5;
>             
>         final int num;
>         final int mind;
>     }
>     ```
>
>   * ```java
>     class Test1{
>         enum Num {one, two, three, four}; // 열거형 num 정의
>         enum Mind {good, think}; // 열거형 mind 정의
>             
>         final Num num; // 타입이 Num 임!
>         final Mind mind;
>     }
>     ```

#### - enum이 제공하는 메소드 (values()와 valueOf())

> * values()
>
>   * 열거형의 모든 상수를 배열에 담아 반환
>
>   * ```java
>     // 열거형 Direction에 정의된 모든 상수를 출력
>     Direction[] dArr = Direction.values(); 
>     
>     for(Direction d : dArr){
>         System.out.printf("%s = %d%n", d.name(), d.ordinal());
>     }
>     ```
>
> * valueof()
>
>   * 컴파일러가 자동적으로 추가해주는 메서드
>
>   * ```java
>     static E values();
>     static E valueof(String names);
>         
>     Direction d = Direction.valueOf("WEST");
>     
>     System.out.printf(d);
>     System.out.printf(Direction.WEST == Direction.valueOf("WEST"));
>     ```

#### - java.lang.Enum

> * Enum 클래스 메서드 들
>
>   * | 메서드                                    | 설명                                                 |
>     | ----------------------------------------- | ---------------------------------------------------- |
>     | Class<E> getDeclaringClass()              | 열거형의 Class객체를 반환                            |
>     | String name()                             | 열거형 상수의 일므을 문자열로 반환                   |
>     | int ordinal()                             | 열거형 상수가 정의된 순서를 반환 (0부터 시작)        |
>     | T valueOf<CLass<T> enumType, String name) | 지정된 열거형에서 name과 일치하는 열거형 상수를 반환 |

#### - EnumSet

> * EnumSet 클래스에는 생성자가 존재하지 않는다.



전체 출처: 자바를 다루는 기술, 자바의 정석

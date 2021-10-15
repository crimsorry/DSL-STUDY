## -목표

###### 자바가 제공하는 다양한 연산자를 학습하세요.



## 학습할 것

- 산술 연산자
- 비트 연산자
- 관계 연산자
- 논리 연산자
- instanceof
- assignment(=) operator
- 화살표(->) 연산자
- 3항 연산자
- 연산자 우선 순위
- (optional) Java 13. switch 연산자



## 학습 내용 정리

#### - 산술 연산자

> * /
>
>   * 모든 피연산자가 정수형일때만 정수 나눗셈을 한다.
>
>   * 그렇지 않으면 부동소수점 나눗셈을 한다.
>
>     ```
>     result = 7 / 2 # 3
>     result = 7.0 / 2 # 3.5
>     result = 7 / 0 # 예외 발생
>     result = 7.0 / 0 # 무한대 or NaN 
>     ```
>
> | 연산자 | 기호           | 의미 | 예 |
> | -------- | --------------- | ---------- | ------ |
> | 덧셈   | +  | x에서 y를 더한다. | x + y |
> | 뺄셈   | -   | x에서 y를 뺀다. | x - y |
> | 곱셉     | *   | x에서 y를 곱한다. | x * y |
> | 나눗셈   | /   | x에서 y를 나눈다. | x / y |
> | 나머지  | %            | x에서 y를 나눌 떄의 나머지값. | x % y |



#### - 비트 연산자

> | 연산자 | 의미                       | 예                                                   |
> | ------ | -------------------------- | ---------------------------------------------------- |
> | ~      | 비트별 NOT                 | ~(0x0FF)은 0xfffff000이 된다.                        |
> | &      | 비트별 AND                 | (0x0FFF & 0xFFF0)은 0xFF0이 된다.                    |
> | ^      | 비트별 XOR                 | (0x0FFF ^ 0xFFF0)은 0xFF0이 된다.                    |
> | \|     | 비트별 OR                  | (0x0FFF \| 0xFFF0)은 0xFF0이 된다.                   |
> | <<     | 비트 왼쪽 이동             | 0xFFF << 4는 0xFFF0이 된다.                          |
> | >>     | 비트 오른쪽 이동           | 0xFFF >> 4는 0xFFF0이 된다.                          |
> | >>>    | 비트 오른쪽 이동(unsigned) | 왼쪽 비트가 부호비트로 채워지지 않고 0으로 채워진다. |



#### - 관계연산자

> * 두개의 피연산자를 비교하는데 사용된다.
>
> * 관계 연산자의 결과는 True(참) 아니면 False(거짓)으로 계산된다.
>
>   | 연산자 기호 | 의미                   | 사용 예 |
>   | ----------- | ---------------------- | ------- |
>   | ==          | x와 y가 같은가?        | x == y  |
>   | !=          | x와 y가 다른가?        | x != y  |
>   | >           | x와 y가 큰가?          | x > y   |
>   | <           | x와 y가 작은가?        | x < y   |
>   | >=          | x와 y가 크거나 같은가? | x >= y  |
>   | <=          | x와 y가 작거나 같은가? | x <= y  |
>



#### - 논리 연산자

> * 여러개의 조건을 조합하여 참인지 거짓인지를 따질때 사용된다.
>
> * **논리 연산자**
>
>    | 연산자 기호 | 사용 예  | 의미                                                       |
>    | ----------- | -------- | ---------------------------------------------------------- |
>    | &&          | x && y   | AND 연산, x와 y가 모두 참이면 참, 그렇지 않으면 거짓       |
>    | \|\|        | x \|\| y | OR 연산, x와 y 중에서 하나만 참이면 참, 모두 거짓이면 거짓 |
>    | !           | !x       | NOT 연산, x가 참이면 거짓,  x가 거짓이면 참                |
>
> * **논리 연산의 결과값**
>
>    | x     | y     | x AND y | x OR y | NOT x |
>    | ----- | ----- | ------- | ------ | ----- |
>    | false | false | false   | false  | true  |
>    | false | true  | false   | true   | true  |
>    | true  | false | false   | true   | false |
>    | true  | true  | true    | true   | false |



#### - instanceof

> * 참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 사용.
>
> * 주로 조건문에 사용되며, instanceof의 왼쪽에는 참조변수를, 오른쪽에는 타입(클래스명)이 피연사자로 위치
>
> * 연산의 결과로 boolean 값인 true와 false중 하나를 반환한다.
>
> * instanceof를 이용한 연산결과로 true를 얻었다는 것은 참조변수가 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.
>
>    ```java
>    class Instanceof { 
>        public static void main(String args[]) { 
>            FireEngine fe = new FireEngine(); 
>         
>            if(fe instanceof FireEngine) { 
>                System.out.println("This is a FireEngine instance."); 
>            } 
>            if(fe instanceof Car) { 
>                System.out.println("This is a Car instance."); 
>            } 
>            if(fe instanceof Object) { 
>                System.out.println("This is an Object instance."); 
>            } 
>            System.out.println(fe.getClass().getName()); // 클래스의 이름을 출력 
>        } 
>    } 
>         
>    class Car {} 
>    class FireEngine extends Car {} // FireEngine은 Object 클래스와 Car 클래스를 상속받았기 때문에 Object 인스턴스와 Car 인스턴스를 모두 포함. 따라서 제 인스턴스와 같은 타입의 instanceof 연산 이외의 조상타입의 instanceof 연산에도 true를 결과로 얻으며, instanceof 연산의 결과가 ture라는 것은 검사한 타입으로의 형변환을 해도 아무런 문제가 없다.
>         
>    -------- // 출력
>    This is a FireEngine instance.
>    This is a Car instance.
>    This is an Object instance.
>    FireEngine    
>    ```
>
>   * 어떤 타입의 대한 instanceof 연산의 결과가 true라는 것은 검사한 타입으로 형변환이 가능하다는 뜻.
>



#### - assignment(=) operator

> * 대입 연산자는 변수에 값을 대입할 때 사용하는 이항 연산자이며, 피연산자들의 결합 방향은 오른쪽에서 왼쪽이다.
>
>   | 대입 연산자 | 설명                                                         |
>   | ----------- | ------------------------------------------------------------ |
>   | =           | 왼쪽의 피연산자에 오른쪽의 피연산자를 대입함.                |
>   | +=          | 왼쪽의 피연산자에 오른쪽의 피연산자를 더한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | -=          | 왼쪽의 피연산자에서 오른쪽의 피연산자를 뺀 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | *=          | 왼쪽의 피연산자에 오른쪽의 피연산자를 곱한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | /=          | 왼쪽의 피연산자를 오른쪽의 피연산자로 나눈 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | %=          | 왼쪽의 피연산자를 오른쪽의 피연산자로 나눈 후, 그 나머지를 왼쪽의 피연산자에 대입함. |
>   | &=          | 왼쪽의 피연산자를 오른쪽의 피연산자와 비트 AND 연산한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | \|=         | 왼쪽의 피연산자를 오른쪽의 피연산자와 비트 OR 연산한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | ^=          | 왼쪽의 피연산자를 오른쪽의 피연산자와 비트 XOR 연산한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | <<=         | 왼쪽의 피연산자를 오른쪽의 피연산자만큼 왼쪽 시프트한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | >>=         | 왼쪽의 피연산자를 오른쪽의 피연산자만큼 부호를 유지하며 오른쪽 시프트한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>   | >>>=        | 왼쪽의 피연산자를 오른쪽의 피연산자만큼 부호에 상관없이 오른쪽 시프트한 후, 그 결괏값을 왼쪽의 피연산자에 대입함. |
>
>   출처: http://www.tcpschool.com/java/java_operator_assignment
>



#### - 화살표(->) 연산자

> * Java 8 버전부터 추가된 연산자로 람다 표현식과 함께 사용.
>
>   ```
>   (argument, ...) -> {expression}
>   ```
>
> * **람다식**은 메소드를 변수처럼 다룰 수 있다는 측면에서 편리
>
> * 대부분의 메소드들은 클래스에 종속된 멤버함수의 형태로 제공되는 형태이지만, 람다식은 클래스에 종속되지 않는다.
>
> * 인자를 0개부터 받아서 implementation 부분에서 활용할 수 있다.
>
> * argument list 부분의 인자가 하나라면 구현부의 소괄호를 생략할 수 있으며, statement 개수가 1개이면 중괄호를 생략할 수 있다.
>
>   출처: https://recoderr.tistory.com/24



#### - 3항 연산자

> * 조건 연산자 ?:
>
>   * 조건 연산자는 첫번쨰 피연산자인 조건식의 평가결과에 따라 다른 결과를 반환.
>
>   * 조건식의 평가결과가 true이면 식1이, false이면 식1가 연산결과가 된다.
>
>     ```java
>     result = (x > y) ? x : y;
>     
>     // (x > y) 결과가 true일 경우
>     result = (5 > 3) ? 5 : 3;
>     result = (true) ? 5 : 3;
>     result = 5;
>     
>     // (x > y) 결과가 false일 경우
>     result = (2 > 3) ? 2 : 3;
>     result = (false) ? 2 : 3;
>     result = 3;
>     ```
>
>   * 조건연산자는 조건문인 if로 바꿔서 간편하게 쓸 수 있다.
>
>     ```java
>     result = (x > y) ? x : y;
>     
>     // 위의 코드와 아래 코드가 같음
>     
>     if(x > y){
>         result = x; 
>     }else{
>         result = y;
>     }
>     ```
>
>   * 기타
>
>     ```java
>     result = x > 0 ? 1 : (x == 0 ? 0 : -1); // x가 양수: 1, 음수: -1. 0: 0
>         
>     // 산술연산 발생
>     x = x + (mod < 0.5 ? 0 : 0.5) // 0과 0.5의 타입이 다르다.
>     x = x + (mod < 0.5 ? 0.0 : 0.5) // 0이 0.0으로 변환되었다.
>     ```
>



#### - 연산자 우선 순위

> * 괄호의 우선순위가 제일 높다.
>
> * 산술 > 비교 > 논리 > 대입의 순서로 우선순위가 진행된다.
>
> * 단항(1) > 이항(2) > 삼항(3)의 순서이며 단항 연산자의 우선순위가 이항 연산자보다 높다.
>
> * 단항 연산자와 대입 연산자를 제외한 모든 연산의 진행방향은 왼쪽에서 오른쪽이다.
>
>   | 종류        | 결합규칙      | 연산자                                      | 우선순위 |
>   | ----------- | ------------- | ------------------------------------------- | -------- |
>   | 단항 연산자 | <------------ | ++  --  +  -  ~  !  (type)                  | 높음     |
>   | 산술 연산자 | ------------> | *  /  %                                     |          |
>   |             | ------------> | +  -                                        |          |
>   |             | ------------> | <<  >>                                      |          |
>   | 비교 연산자 | ------------> | <  >  <=  >= instanceof                     |          |
>   |             | ------------> | == !=                                       |          |
>   | 논리 연산자 | ------------> | &                                           |          |
>   |             | ------------> | ^                                           |          |
>   |             | ------------> | \|                                          |          |
>   |             | ------------> | &&                                          |          |
>   |             | ------------> | \|\|                                        |          |
>   | 삼항 연산자 | ------------> | ?:                                          |          |
>   | 대입 연산자 | <------------ | =  +=  -=  *=  /=  %=  <<=  >>=  &=  ^=  != | 낮음     |



#### - (optional) Java 13. switch 연산자

> * 자바 SE 12 에서 switch 표현식 도입.
>
>   ```java
>   public static void main(String[] args){
>       int num, result;
>       final int ONE = 1;
>
>       switch(result){
>           case '1': // 문자 리터럴
>           case ONE: // 정수 상수
>           case "YES": // 문자열 리터럴. JDK 1.7부터 허용
>           case num: // 에러. 변수는 불가능
>           case 1.0: // 에러. 실수도 불가능
>       }
>   }
>   ```
>
>   ```java
>   public enum Day { SUNDAY, MONDAY, TUESDAY,
>       WEDNESDAY, THURSDAY, FRIDAY, SATURDAY; }
>
>   // ...
>
>   int numLetters = 0;
>   Day day = Day.WEDNESDAY;
>   switch (day) {
>       case MONDAY:
>       case FRIDAY:
>       case SUNDAY:
>           numLetters = 6;
>           break;
>       case TUESDAY:
>           numLetters = 7;
>           break;
>       case THURSDAY:
>       case SATURDAY:
>           numLetters = 8;
>           break;
>       case WEDNESDAY:
>           numLetters = 9;
>           break;
>       default:
>           throw new IllegalStateException("Invalid day: " + day);
>   }
>   System.out.println(numLetters);
>   ```
>
> * 13에서 yield 명령문 도입
>
>   ```java
>   Day day = Day.WEDNESDAY;
>   int numLetters = switch (day) {
>       case MONDAY:
>       case FRIDAY:
>       case SUNDAY:
>           System.out.println(6);
>           yield 6;
>       case TUESDAY:
>           System.out.println(7);
>           yield 7;
>       case THURSDAY:
>       case SATURDAY:
>           System.out.println(8);
>           yield 8;
>       case WEDNESDAY:
>           System.out.println(9);
>           yield 9;
>       default:
>           throw new IllegalStateException("Invalid day: " + day);
>   };
>   System.out.println(numLetters);
>   ```
>
>   출처: https://docs.oracle.com/en/java/javase/13/language/switch-expressions.html



전체 출처: Power Java, 자바의 정석

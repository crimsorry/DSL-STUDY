## -목표

###### 자바가 제공하는 다양한 연산자를 학습하세요.



## 학습할 것

- 인터페이스 정의하는 방법
- 인터페이스 구현하는 방법
- 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법
- 인터페이스 상속
- 인터페이스의 기본 메소드 (Default Method), 자바 8
- 인터페이스의 static 메소드, 자바 8
- 인터페이스의 private 메소드, 자바 9



## 학습 내용 정리

#### - 인터페이스 정의하는 방법

> * 인터페이스를 작성하는 것은 클래스를 작성하는 것과 같다.
>
> * 다만 키워드로 class대신 interface를 사용한다는 것만 다른다.
>
> * 그리고 interface에도 클래스와 같이 접근 제어자로 public 또는 default를 사용할 수 있다.
>
> * ```java
>   interface 인터페이스이름{
>   	public static final 티입 상수이릅 = 값;
>       public abstract 메서드이름(매개변수목록);
>   }
>   ```
>
> * 일반적인 클래스의 멤버들과 달리 인터페이스의 멤버들은 다음과 같은 제약사항이 있다.
>
> * > - 모든 맴버변수는 public final이어야 하며, 이를 생략할 수 있다.
>   > - 모든 메서드는 public abstract 이어야 하며, 이를 생략할 수 있다. (단 static 메서드와 디폴트 메서드를 예외 JDK 1.8 부터)
>   > - 생성된 제어자는 컴파일 시 컴파일러가 자동적으로 추가해준다.



#### - 인터페이스 구현하는 방법

> * 클래스는 확장한다는 의미의 키워드인 'extends'를 사용하지만 인터페이스는 구현한다는 의미의 키워드 'implements'를 사용한다.
>
> * ```java
>   class 클래스이름 implements 인터페이스이름{
>       // 인터페이스에 정의된 추상메서드를 구현해야 한다.
>   }
>   class Fighter implements Fightable{
>       public void move(int x, int y){ }
>       public void attack(Unit u){ }
>   }
>   ```



#### - 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법

> * 자손클래스의 인스턴스를 조상타입의 참조변수로 참조하는 것이 가능하다.
>
> * 리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 것을 의미한다.
>
> * ```java
>   interface Paraseable{
>       // 구분 분석작업을 수행
>       public abstract void parse(String fileName);
>   }
>   
>   class ParserManager{
>       // 리턴타입이 Parseable 인터페이스이다.
>       public static Parseable getParser(String type){
>           if(type.equals("XML")){
>               return new XMLParser();
>           }else{
>               Parseable p = new HTMLParser();
>               return p;
>           }
>       }
>   }
>   
>   class XMLParser implements Parseable{
>       public void parse(String fileName){
>           System.out.println(fileName + "- XML parsing completed.");
>       }
>   }
>   
>   class HTMLParser implements Parseable{
>       public void parse(String fileName){
>           System.out.println(fileName + "- HTML parsing completed.");
>       }
>   }
>   
>   class ParserTest{
>       public static void main(String args[]){
>           Parseabl parser = ParserManager.getParser("XML");
>           parser.parse("document.xml");
>           parser = ParserManager.getParser("HTML");
>           parser.parse("document2.html");
>       }
>   }
>   
>   // 실행결과
>   document.xml - XML parsing completed.
>   document.xml2 - HTML parsing completed.
>   ```
>
> * 만일 나중에 새로운 종류의 XML구문 분석기 NewXMLParser 클래스가 나와도 ParserTest 클래스는 변경할 필요없이 ParserManager 클래스의 getParser 메서드에서 'return new XMLParser();' 대신 'return new NewXMLParser();'로 변경하면 된다.
>
> * 이러한 장점은 특히 분산환경 프로그래밍에서 위력을 발휘한다.



#### - 인스페이스 상속

> * 인터페이스는 인터페이스로부터만 상속받을 수 있으며, 클래스와는 달리 다중 상속, 즉 여러개의 인터페이스로부터 상속 받는 것이 가능하다.
>
> * 인터페이스는 클래스와 달리 Object 클래스와 같은 최고 조상이 없다.
>
> * ```java
>   interface Movable{
>       // 지정된 위치(x, y)로 이동하는 기능의 메서드
>       void move(int x, int y);
>   }
>   interface Attackable{
>       // 지정된 대상(u)를 공격하는 기능의 메서드
>       void move(int x, int y);
>   }
>   interface Fightable extends Movable, Attackable{}
>   ```
>
> * 클래스의 상속과 마찬가지로 자손 인터페이스(Fightable)은 조상 인터페이스(Movable, Attackable)에 정의된 멤버를 모두 상속받는다.



#### - 인터페이스의 기본 메소드 (Default Method), 자바 8

> * 원래는 인터페이스에 추상 메서드만 선언할 수 있었지만, JDK 1.8부터 디폴트 메서드와 static 메서드를 추가할 수 있게 되었다.
>
> * 디폴트 메서드는 추상 메서드의 기본적인 구현을 제공하는 메서드로, 추상 메서드가 아니기 때문에 디폴트 메서드가 새로 추가되어도 해당 인터페이스를 구현한 클래스르 변경하지 않아도 된다.
>
> * 디폴트 메서드는 앞에 키워드 default 를 붙이며, 추상 메서드와 달리 일반 메서드처럼 몸통{ } 이 있어야 한다.
>
> * 디폴트 메서드 역시 접근 제어자가 public 이며, 생략가능하다.
>
> * ```java
>   // 1
>   interface MyInterface{
>       void method();
>       void newMethod(); // 추상메서드
>   }
>   
>   // 2
>   interface MyInterface{
>       void method();
>      	default void newMethod(); // 추상메서드
>   }
>   ```
>
> * 1과 같이 newMethod()라는 추상 메서드를 추가하는 대신, 1와 같이 디폴트 메서드를 추가하면, 기존의 MyInterface를 구현한 클래스를 변경하지 않아도 된다. 즉, 조상 클래스에 새로운 메서드를 추가하는 것돠 동일해지는 것이다.
>
> * 대신 이름이 같이 충돌하는 경우가 발생한다.
>
> * > * 여러 인터페이스의 디폴트 메서드 간의 충돌
>   >
>   >   -> 인터페이스를 구현한 클래스에서 디폴트 메서드를 **오버라이딩**해야 한다.
>   >
>   > * 디폴트 메서드와 조상 클래스의 메서드 간 충동
>   >
>   >   -> 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시된다.



#### - 인터페이스의 static 메소드, 자바 8

> * static 메서드는 인스턴스와 관계가 없는 독립적인 메서드이기 때문에 인터페이스에 추가하지 못할 이유가 없었다. 그러나 자바를 보다 쉽게 배울 수 있게 하기 위해 인터페이스의 모든 메서드는 추상메서드여야 한다는 규칙에 예외를 두지 않았다. 그래서 자바 8 이전까지는 별도의 클래스에 따로 두어야 했다.
> * 가장 대표적으로 java.util.Conllection 인스페이스가 있다. 이 인터페이스와 관련된 static 메서드들이 인터페이스에는 추상 메서드만 선언할 수 있다는 원칙 때문에 별도의 클래스, Collection 클래스에 들어가게 되었다.
> * 만일 인터페이스에 static 메서드를 추가할 수 있었다면, Collection 클래스는 존재하지 않았을 것이다.



#### - 인터페이스의 private 메소드, 자바 9

> * interface 내부 메서드에서 사용할 뿐인데, public method로 만들어야 하는 문제가 있고, interface를 구현할 수 있는 interface 또는 class가 특정 metod에 접근하는거 자체를 막고싶을 수도 있기때문에 private 메서드가 추가되었다.
>
> * ```java
>   public interface Boo {
>       /**
>        * @implSpec 이 메소드는 오버라이드 하거나, 외부에서 접근할 수 없습니다.  
>        * @return "Bye"
>        */
>       private String printBye(){
>           return "Bye";
>       }
>       default void knockDoor(){
>           System.out.println("Ok.. " + printBye());
>       }
>   }
>   ```
>
> * 위와 같이 작성을 해서 외부에서 접근이 불가능하도록 만들 수 있다.
>
> 출처: https://catch-me-java.tistory.com/44




전체 출처: 자바를 다루는 기술, 자바의 정석

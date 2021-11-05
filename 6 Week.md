## -목표

###### 자바가 제공하는 다양한 연산자를 학습하세요.



## 학습할 것

- 자바 상속의 특징
- super 키워드
- 메소드 오버라이딩
- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
- 추상 클래스
- final 키워드
- Object 클래스



## 학습 내용 정리

#### - 자바 상속의 특징

> * 상속
>
>   * 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것
>   * 상속을 통해서 클래스를 작성함녀 보다 적은 양의 코드로 새로운 클래스를 작성할 수 있고, 코드를 공통적으로 관리할 수 있기 때문에 코드의 추가 및 변경이 매우 용이하다.
>   * 이러한 특징은 코드의 재사용성을 높이고 코드의 중복을 제거하여 프로그램의 생산성과 유지보수에 크게 기여한다.
>
> * 자바에서 상속 구현하는 법
>
>   * 새로 작성하고자 한느 클래스의 이름 뒤에 상속받고자 하는 클래스의 이름을 키워드 'extends'와 함께 작성
>
>     ```java
>     class Child extends Parent{
>     
>     }
>     ```
>
>   * 이 두 클래스는 서로 상속 관계에 있다고 하며,상속해주는 클래스를 '조상 클래스'라 하고, 상속받는 클래스는 '자손 클래스'라고 한다.
>
>     > 조상 클래스: 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스
>     >
>     > 자손 클래스: 자식(child)클래스, 하위(sub)클래스, 파생된(derived)클래스
>
>     ```java
>     class Parent{
>     	int age;
>     }
>     
>     class Child extends Parent{
>         void play(){
>             System.out.println("놀자~");
>         }
>     }
>     ```
>
>   * Child 클래스에 새로운 코드가 추가되어도 조상인 Parent클래스는 아무런 영향도 받지 않는다.
>
>   * 하지만 조상 클래스가 변경되면 자손 클래스는 자동적으로 영향을 받게 된다.
>
>   * 따라서 자손 클래스는 조상 클래스의 모든 멤버를 상속받으므로 항상 조상 클래스보다 같거나 많은 멤버를 갖게 된다.
>
>     > - 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다.
>     > - 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.
>     > - 코드를 한 곳에서 관리함으로서 코드의 중복이 줄어든다. 하지만 코드의 중복이 많아지면 유지보수가 어려워지고 일관성을 유지하지 어렵다.
>     > - 자손 클래스의 인스턴스를 생성하면 조상 클래스의 멤버와 자손 클래스의 멤버가 합쳐진 하나의 인스턴스로 생성된다.
>
>   



#### - super 키워드

> * super 키워드
>
>   * 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조변수이다.
>
>   * 멤버변수와 지역변수의 이름이 같을 때 this를 붙여서 구별했듯이 상속받은 멤버와 자신의 멤버와 이름이 같을 때는 super 를 붙여서 구별할 수 있다.
>
>     ```java
>     class SuperTest{
>         public static void main(String args[]){
>             Child c = new Child();
>             c.method();
>         }
>     }
>         
>     class Parent{
>         int x = 10;
>     }
>         
>     class Child extends Parent{
>         int x = 20;
>             
>         void method(){
>             System.out.println("x=" + x);
>             System.out.println("this.x=" + this.x);
>             System.out.println("super.x=" + super.x);
>         }
>     }
>         
>     // x=20
>     // this.x=20
>     // super.x=10
>     ```
>
> * super() - 조상 클래스의 생성자
>
>   * this()와 마찬가지로 super() 역시 생성자이다.
>
>   * this()는 같은 클래스의 다른 생성자를 호출하는데 사용되지만, super()는 조상 클래스의 생성자를 호출하는데 사용된다.
>
>   * Object클래스를 제외한 모든 클래스의 생성자 첫 줄에 생성자.this() 또는 super()를 호출해야 한다. 그렇지 않으면 컴파일러가 자동적으로 'super();'를 생성자의 첫줄에 삽입한다.
>
>     > 1. 클래스 - 어떤 클래스의 인스턴스를 생성할 것인가?
>     > 2. 생성자 - 선택한 클래스의 어떤 생성자를 이용해서 인스턴스를 생성할 것인가?
>
>     ```java
>     class PointTest{
>     	public static void main(String args[]){
>             Point3D p3 = new Point3D();
>             System.out.println("p3.x=" + p3.x);
>             System.out.println("p3.y=" + p3.y);
>             System.out.println("p3.z=" + p3.z);
>         }
>     }
>             
>     class Point{
>         int x=10;
>         int y=20;
>                 
>         Point(int x, int y){
>             // 생성자 첫 줄에서 다른 생성자를 호출하지 않기 떄문에 컴파일러가 'super();'를 여기에 삽입한다. 클래스의 기본 생성자인 Object()를 의미한다.
>             this.x = x;
>             this.y = y;
>         }
>     }
>             
>     class Point3D extends Point{
>         int z = 30;
>                 
>         Point 3D(){
>             this(100, 200, 300); // Point3D(int x, int y, int z)를 후출
>         }
>                 
>         Point3D(int x, int y, int z){
>             super(x,y); // Point(int x, int y)를 호출한다.
>             this.z = z;
>         }
>     }
>             
>     // p3.x = 100
>     // p3.y = 200
>     // p3.z = 300
>     ```



#### - 메소드 오버라이딩

> * 오버라이딩
>
>   * 조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것을 오버라이딩이라고 한다.
>   * 상속받은 메서드를 그대로 사용하기도 하지만, 자손 클래스 자신에 맞게 변경해야하는 경우에 조상의 메서드를 오버라이딩이라고 한다.
>
> * 오버라이딩 조건
>
>   > 자손 클래스에서 오버라이딩하는 메소드는 조상 클래스의 메서드와
>   >
>   > - 이름이 같아야 한다.
>   > - 매개변수가 같아야 한다.
>   > - 반환타입이 같아야 한다.
>   >
>   > => 한마디로 선언부가 서로 일치해야 한다.
>   >
>   > 하지만 접근 제어자(access modifier)와 예외(exception)은 제한된 조건 하에섬나 다르게 변경할 수 있다.
>
>   > 조상 클래스의 메서드를 자손 클래스에서 오버라이딩할때
>   >
>   > 1. 접근 제어자를 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다.
>   > 2. 예외는 조상 클래스의 메서드보다 많이 선언할 수 없다.
>   > 3. 인스턴스메서드를 static메서드 또는 그 반대로 변경할 수 없다.
>
>   ```java
>   class Point{
>       int x;
>       int y;
>           
>       String getLocation(){
>           return "x : " + x + " y : " + y;
>       }
>   }
>       
>   class Point3D extends Point{
>       int z;
>           
>       String getLocation(){ // 오버라이딩
>           return "x : " + x + " y : " + y + " z : " + z;
>       }
>   }
>   ```



#### - 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)

> dynamic은 runtime의 동의어로 사용되며, dispatch는 어떤 메소드를 호출할지 결정하는 것이다.



#### - 추상 클래스

> * 클래스 내에 추상 메서드가 선언되어 있음을 의미한다.
>
> * 아직 완성되지 않은 메서드가 존재하는 '미완성 설계도' 이므로 인스턴스를 생성할 수 없다.
>
>   ```java
>   abstract class AbstractTest{ // 추상 클래스(추상 메서드를 포함한 클래스)
>       abstract void move(); // 추상 메서드(구현부가 없는 메서드)
>   }
>   ```
>
> * 추상 메서드가 없는 클래스도 abstract를 붙여서 추상 클래스로 만드는 경우도 있다.
>
>   ```java
>   public abstract class WindowAdapter
>   	implements WindowListener, WindowStateListener, WindowFocusListener{
>   		public void WindowOpened(WindowEvent e){}
>       	public void WindowClosing(WindowEvent e){}
>       	public void WindowClosed(WindowEvent e){}
>       	public void WindowIconified(WindowEvent e){}
>   	}
>   ```



#### - final 키워드

> * final은 '마지막의' 또는 '변경될 수 없는' 의 의미를 가지고 있으며 거의 모든 대상에 사용될 수 있다.
>
> * 변수에 사용됨녀 값을 변경할 수 없는 상수가 되며, 메서드에 사용되면 오버라이딩을 할 수 없게 되고 클래스에 사용되면 자신을 확장하는 자손클래스를 정의하지 못하게 된다.
>
>   > final이 사용될 수 있는 곳 - 클래스, 메서드, 멤버변수, 지역변수
>
>   | 제어자 | 애상     | 의미                                                         |
>   | ------ | -------- | ------------------------------------------------------------ |
>   | final  | 클래스   | 변경될 수 없는 클래스. 확장될 수 없는 클래스가 된다. 그래서 final로 지정한 클래스는 다른 클래스의 조상이 될 수 없다. |
>   |        | 메서드   | 변경될 수 없는 메서드, final로 지정된 메서드는 오버라이딩을 통해 재정의 될 수 없다. |
>   |        | 멤버변수 | 변수 앞에 final이 붙으면, 값을 변경할 수 없는 상수가 된다.   |
>   |        | 지역변수 | 변수 앞에 final이 붙으면, 값을 변경할 수 없는 상수가 된다.   |
>   
>   ```java
>   final class FinalTest{ // 조상이 될 수 없는 클래스
>       final int max_size = 10; // 값을 변경할 수 없는 멤버변수(상수)
>       
>       final void getMaxSize(){ // 오버라이딩할 수 없는 메서드(변경불가)
>           final int LV = max_size; // 값을 변경할 수 없는 지역변수(상수)
>           return max_size;
>       }
>   }
>   ```



#### - Object 클래스

> * 모든 클래스 상속 계층도의 **최상위**에 있는 조상클래스이다.
>
> * 다른 클래스로부터 상속 받지 않은 모든 클래스들은 자동적으로 Object클래스로부터 상속받게 함으로써 모든 클래스의 조상이 되도록 한다.
>
> * 만일 다른 클래스로부터 상속을 받는다고 하더라도 상속계층도를 따라 조상클래스, 조상클래스의 조상클래스를 찾아 올라가다 보면 결국 마지막 최상위 조상은 Object 클래스일 것이다.
>
>   ```java
>   class Tv{
>       
>   }
>   
>   class CaptionTv extends Tv{
>       
>   }
>   ```
>
> * 그래서 자바의 모든 클래스들은 Obejct 클래스의 멤버들을 상속 받기 때문에 Object 클래스에 정의된 멤버들을 사용할 수 있다.




전체 출처: 자바를 다루는 기술, 자바의 정석

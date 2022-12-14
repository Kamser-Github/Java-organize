# 클래스 내부 구성요소

## 필드(field)
```
객체의 속성값을 지정할 수 있는 "클래스"에 포함된 변수
[비교] 지역변수(local variable)는 메서드에 포함된 변수
```

>필드
```
○ 상위 중괄호가 클래스인 경우
○ Heap 메모리에 저장
○ Heap 메모리에 들어가는 필드값은 미입력시 강제 초기화
- 기본자료형
    숫자타입 Default : 0
    boolean Default : false
- 참조자료형
            Default : null
```
>지역변수
```
○ 상위 중괄호가 메서드인 경우
○ Stack 메모리에 저장
○ Stack 메모리에 들어가는 지역변수는 강제 초기화가 없다.
○ 초기화 없이 사용시 오류 발생
```
## 메서드(Method)
> 메서드를 사용해야하는 이유   

### 1. 높은 재사용성   
    한번 만들어 놓으면 몇번이고 재사용이 가능하며
    다른 프로그램에서도 사용이 가능하다.
### 2. 중복된 코드제거
    반복적으로 나타나는 문장을 메소드로 만들어서 사용하면
    중복제거,변경사항이 발생시 메소드만 수정하면 되므로
    관리가 편하고 , 오류 발생 가능성이 낮다.
### 3. 코드의 모듈화를 통해 코드 가독성 향상
    내용이 없는 메서드를 작업단위(모듈화)로 만들어 놓고
    하나씩 완성해나가면서 프로그램을 구조화한다.

### `메서드의 정의`
```java

int add (int x , int y){ //메소드 선언부
    int result = x + y;           \
    return result; // 결과를 반환  | 메소드 구현부
}                                 /

반환타입 : int
메소드 명 : add
매개변수 : int x, int y

특히 메소드명은 주의해야한다.
메소드 선언부를 변경하게 되면
호출되는 모든 곳도 다 같이 변경해야된다.
```
> 매개변수 선언
```
메서드가 작업하기에 필요한 값을 입력받기위한 것이며
" , " 로 구분한다.
타입이 같다고 하더라도 변수의 타입은 생략이 불가하다
필요한 값이 없으면 생략이 가능하다.
```
> 매서드 명
```
메서드 이름은 동사가 많으며
메서드 명을 보고 기능을 알수있도록 
함축적이고 의미있게 지어야한다
```
> 반환타입
```
메소드는 반드시 반환타입을 작성해야하며
반환타입이 없을 경우에는 void를 작성한다.
반환타입이 void 일경우 return이 생략이 가능하다
```
> ### return문
```
반환 타입이 void가 아닐경우 반드시 구현부 안에 'return 반환값'
반환타입이 없는 void의 경우 생략시
컴파일러가 자동으로 넣어준다.
이 들어가야하며 출력 반환값은 최대 하나만 가능하다
```
`반환타입과 리턴타입은 일치하거나 자동 형변환이 가능해야한다`

### `메소드 호출`
```
실제 입력 값 : (전달)인자 argument
매소드가 필요한 자료형 : 매개변수 parameter

>> 인자값이 매개변수타입과 일치하거나 자동형변환이 가능한 것
```
` 결국 반환타입,리턴타입,저장 변수타입은 다 동일해야한다`

### `매개변수의 유효성검사`
> 매소드의 경우 모든 경우의 수에 반환을 넣어야한다.
```java

int findIndex(int[] arr,int findNum){
    for(int i=0 ; i<arr.length ; i++){
        if(arr[i]==findNum)
            return findNum;
    }
    //여기서 모든 경우의 수에 반환값이 있어야하므로
    return 0; //이걸 넣어야한다.
}
```

### `기본형 매개변수와 참조형 매개변수`
> 매서드의 매개변수 전달 기법(parameter passing)   

1. Call By Value(값 전달 기법)
    ```
    실제 값을 전달하는 방법
    int a = 10 , int b = 20;
    int total = sum ( a, b)
    실제 데이터가 매개변수로 복사전달된다.
    따라서 데이터의 기억공간은 개별로 적용된다.
    ```

2. Call By Reference(번지 전달 기법)
    ```
    int[] arr = {10,20,30};
    int total = sum (arr)
    참조값 ( 주소 )가 sum에 전달이되며
    같은 주소로 동일한 객체를 가리키게된다.
    ```

> 객체 멤버변수를 변경하려면 어떻게 해야될까?
```
기본형 매개변수 변수의 값을 읽기만 할수있다 
참조형 매개변수 변수의 값을 읽고 해당 주소의 값도 변경가능하다.
```
__예시__
```java
class Data {
    int x;
}
public class ParameterComparing {
    public static void main(String[] args){
        Data d = new Data();
        d.x = 10;
        changePrimitive(d.x);
        //x = 1000;
        System.out.println(d.x);
        //x = 10;
        --
        changeReference(d);
        //x = 500;
        System.out.println(d.x);
        //x = 500;
    }
    static void changePrimitive(int x){
        x = 1000;
        System.out.println("change Primitive: "+x);
    }
    static void changeReference(Data a){
        a.x = 500;
        System.out.println("change Reference: "+a.x);
    }
}
/*
기본 자료형은 값을 복사해서 전달하지만

참조 자료형은 참조값을 전달하게 되므로
참조값이 있으면 해당 객체에 접근하여 수정이 가능하다.
```
### `반환타입이 참조형일경우`
> 반환타입이 참조형일경우 "반환값은 객체의 주소"다
```java
class Data { int x; }

public class ReturnReference {
    public static void main(String[] args){
        Data baseData = new Data();
        baseData.x = 10;
        Data copyData = copyData(baseData);
        System.out.println(copyData.x);
        //x = 10;
    }
    //해당 주소에 값을 복사해서 반환을 객체로하면
    //그 객체의 주소를 전달하기때문에
    //인스턴스객체 주소가 copyData에 저장이 되었기에
    //매소드가 끝나도 해당 인스턴스 객체는 사라지지 않는다.
    static Data copyData(Data data){
        Data tmp = new Data();
        tmp.x = data.x;
        return tmp;
    }
}
```
## 클래스 매서드와 인스턴스 매서드
> static => 클래스 , non static => 인스턴스   

```
클래스를 호출하게 되면
static이 붙은 매서드와 변수는 
method Area static zone에 저장된다.
따라서 객체를 생성하지 않고도 
클래스명.메소드명,클래스명.변수명 으로 사용이 가능하다

static이 붙지 않은 멤버는 객체를 생성하지 않으면
메모리에 올라와 있지 않기에 사용할수 없으며 
static 메소드나 변수는 따라서 인스턴스 멤버를 사용할수가 없다

반대로 인스턴스 멤버는 static 멤버를 사용할수 있는데
인스턴스 멤버를 사용한다는 이야기는 결국 메모리에 올라와있다는 뜻이기에
이미 static은 메모리에 무조건 올라와 있을수 밖에 없다.
```
`클래스 매서드나 변수는 인스턴스 멤버를 사용할수없다.`   
`인스턴스 멤버는 클래스 멤버를 사용할수 있다.`
> 클래스 생성시 static 여부
```
모든 인스턴스에서 공용으로 사용하는 것에 static을 붙인다
 : 모든 객체는 매서드가 공용이고 멤버변수만 다르다.
 : 즉 같은 값을 공용으로 사용해야한다면 static을 붙여야한다.

매서드내에서 인스턴스변수를 사용하지 않는다면 static을 고려한다.
 : 인스턴스 멤버 변수를 사용해야하는 경우라면 static을 붙이면 안되고
 : 반대로 인스턴스 멤버를 사용하지 않은 메서드라면 static을 고려할만하다.
```
## 오버로딩
-  -  -
> 변수와 마찬가지로 메서드도 같은 클래스내에 이름으로 구별된다.
```
기능이 같은 매서드가 매개변수 타입과 개수가 다르다고
새로운 이름을 만들어야하고 사용자는 그에 따라 불편함이 생긴다.

따라서 기능은 같은 메서드 하나의 이름에
매개변수 타입과 , 개수 , 순서가 다른 매서드를 만들수 있다.

즉 같은 이름의 메소드를 여러 개 정의 하는것 
매서드 오버로딩, 또는 오버로딩이라고 한다.
```
### `오버로딩 조건`

#### 1. 메서드 명이 같아야한다.
#### 2. 매개변수의 개수 또는 타입이 달라야한다.

__예시__
```java
public class Test {
    public static void main(Sring[] args){
        OverLoad ov = new OverLoad();
        ov.sum(34.6f,46);
        ov.sum(34.6f,88f);
        //이렇게 컴파일을 하면

        sum_float_int(float a,int b);
        sum_float_float(float a,float b);
        //이렇게 컴파일러가 매소드명을 구분한다.
    }
}
```
`오버로딩  :  정적바인딩이 되기에 속도저하가 없다`
>정적바인딩이란 ?
```
컴파일러가 컴파일 시점에서 호출될때 메서드가 이미 결정되어 있기에
해당 메서드를 찾아서 사용하면 된다.
따라서 오버로딩을 하더라도 속도 저하와는 상관이 없다.
```
# 생성자(Constructor)
## `생성자란 ?`
```
○ 인스턴스가 생성될 때 호출되는 '인스턴스 초기화 메서드'이다.
○ 인스턴스 변수의 초기화 작업에 주로 사용
○ 인스턴스 생성시에 실행되어야 할 작업을 위해서도 사용된다.
```
> 생성자의 특이점
```
1. 생성자의 이름은 클래스의 이름과 같아야한다.
2. 생성자는 리턴값이없다 
    ○ 메서드이지만 void를 안붙이는 이유는 모든 생성자가 return값이 없기에
      void를 생략할수 있게 한것.
```
`연산자 new가 인스턴스 생성한 것이지 생성자는 초기화만 할뿐이다.`

## `기본 생성자`
```
클래스내에 생성자가 없을경우 컴파일러가 기본 생성자를 추가하여 컴파일한다.

주의할점 : 매개변수 있는 생성자를 만들경우
            컴파일러는 기본생성자를 만들어주지 않는다.
```
## `매개변수 있는 생성자-오버로딩`
```java
인스턴스 초기화에 필요한 매개변수를 받을수 있다.
따라서 ,
        클래스를 작성할때 다양한 생성자를 제공하는것이
        별도에 초기화를 하지 않도록 하는것이 바람직하다.

public class Book {
    String name;
    int price;
    int kind;

    class Book(){...}
    class Book(String name){...}
    class Book(String name,int price){...}
    class Book(String name,int price,int kind){...}
}
```
## `private 생성자 매서드`
```
private 접근 제어로 객체를 생성할수 없다는 뜻이되므로
객체를 생성하지 않고 사용할수있게 모든 클래스 멤버가 static이 되어야한다.

ex ) Math,System ...

항상 static 멤버는
클래스 이름.클래스메서드 로 static이라는걸 표시해야한다.
```
## `생성자를 호출하는 this(),자기 자신을 가리키는 참조변수 this`
> ### this()
```java
this()는 

자신이 가지고 있는 생성자중에서 
매개변수를 확인하고 해당 생성자를 호출한다.

따라서 중복코드를 제거하고, 유지보수가 간단해진다.

주의할점은 this()는 항상 먼저 초기화를 해야하는데.

생성자는 클래스가 생성될 때 호출이 되므로
클래스 생성이 완료 되지 않은 상태에서 
생성자메서드 코드가 아니라면 오류가 발생한다.
디폴트 생성자에서 생성이 완료되는 것이 아니라 this()를 사용해
다른 생성자를 호출하므로 항상 this()가 먼저와야한다.

class Texi {
    int standardPrice ;
    int addPrice ;
    int peopleLimit ;

    Texi (){
        this(3800,150,4);
    }
    Texi (int standardPrice){
        this.standardPrice = standardPrice;
    }
    Texi (int standardPrice,int addPrice){
        this(standardPrice);
        this.addPrice = addPrice;
    }
    Texi (int standardPrice,int addPrice,int peopleLimit){
        this(standardPrice,addPrice);
        this.peopleLimit = peopleLimit;
    }
}
서로 기본 생성자로 초기화를 해도 값을 넣어줄수 있게 할수있으며
다양한 생성자를 만들어도 중복코드가 발생하지 않게 할수 있다.
```
### this.
```java
자기 자신을 참조변수이며 주소를 가지고 있다.
인스턴스 객체가 만들어질때 생성이 되며

1.매개변수와 인스턴스 변수를 구분할때 사용
2.주소를 반환

2번 예시

class Person {

    ...
    ...

    Person returnItSelf(){
        return this;
    }
}
public static void main(String[] args){

    Person noName = new Person();
    Person p = noName.returnItSelf();
    System.out.println(p);
    System.out.println(noName);

    //둘의 참조값은 같다.
}
```
## `변수의 초기화`
> ### 멤버변수의 초기화 방법
```
1. 명시적 초기화(explicit initialization)
2. 생성자(constructor)
3. 초기화 블럭(initialization block)
    - 인스턴스 초기화 블럭 : 인스턴스 변수를 초기화 하는데 사용 
    - 클래스 초기화 블럭   : 클래스 변수를 초기화 하는데 사용
```
> ### 명시적 초기화
```java
변수를 선언과 동시에 초기화 하는것을 명시적 초기화라 한다.
가장 기본이면서 간단한 초기화 방법이고
여러 초기화 방법중에서 가장 우선적으로 고려되어야 한다.

class Home {
    int door = 3;           //기본형 변수의 초기화
    Room room = new Room(); //참조형 변수의 초기화
}
보다 복잡한 초기화 작업이 필요할때에는
초기화 블럭, 또는 생성자를 사용해야한다.
```
>### 초기화블럭
```java
클래스 초기화 블럭      - 클래스 변수의 복잡한 초기화에 사용된다.
인스턴스 초기화 블럭    - 인스턴스 변수의 복잡한 초기화에 사용된다.

초기화 블럭 내에는 메서드 내에서와 같이 
        조건문,반복문,예외처리구문등 자유롭게 사용할 수 있다.

static {
    //클래스 초기화 블럭
}
--
{
    //인스턴스 초기화 블럭
}
```
> ### 멤버변수의 초기화 시기와 순서
```
클래스 변수의 초기화 시점 - 클래스가 처음 로딩될때 단 한번 ! 초기화
인스턴스 변수의 초기화 시점 - 인스턴스가 생성될 때마다 각 인스턴스별로 초기화

클래스 변수의 초기화 순서
    기본값 => 명시적 초기화 => 클래스 초기화 블럭 (1회)

인스턴스 변수의 초기화순서
    기본값 => 명시적 초기화 => 인스턴스 초기화 블럭 => 생성자 (매회)
```
---
layout: post
title: 자바의 정석 스터디 - 객체지향
subtitle: 객체지향프로그래밍 Ⅰ
categories: study
tags: JAVA
comments: true
published: true
---

## 자바의 정석
>자바의 정석 스터디 1주차 (2021-09-13 ~ )
>Ch06 - 객체지향프로그래밍 Ⅰ 정리

## 목차
### 1.  객체 지향 언어
- 객체지향언어의 역사
- 객체지향 언어

### 2. 클래스와 객체
- 클래스와 객체의 정의와 용도
- 객체와 인스턴스
- 객체의 구성요소 - 속성과 기능
- 인스턴스의 생성과 사용
- 객체 배열
- 클래스의 또 다른 정의

### 3. 변수와 메서드
- 선언위치에 따른 변수의 종류
- 클래스변수와 인스턴스 변수
- 메서드
- 메서드 선언과 구현
- 메서드의 호출
- return 문
- JVM 메모리의 구조
- 기본형 매개변수와 참조형 매개변수
- 참조형 반환타입
- 재귀 호출(recusive call)
- 클래스 메서드(static method)와 인스턴스 메서드
- 클래스 맴버와 인스턴스 맴버간의 참조와 호출

### 4.  오버로딩
- 오버로딩이란?
- 오버로딩의 조건
- 오버로딩의 예
- 오버로딩의 장점
- 가변인자(varargs)와 오버로딩

### 5. 생성자
- 생성자란?
- 기본 생성자(defalut constructor)
- 매개변수가 있는 생성자
- 생성자에서 다른 생성자 호출하기 - this(), this
- 생성자를 이용한 인스턴스의 복사

### 6. 변수의 초기화
- 변수의 초기화
- 명시적 초기화
- 초기화 블럭
- 맴버변수의 초기화 시기와 순서

---

<br/>

### 1.  객체 지향 언어

<br/>

#### 객체지향 언어의 역사
**과학 실험이나 미사일 발사 실험과 같은 모의실험 목적으로 사용**

>실제 세계 - >가상세계를 컴퓨터 속에 구현  -> 객체지향이론 탄생

<br/>

**객체지향이론 ❓**
> 실제 셰계는 사물(객체)로 이루어져 있으며, 발생하는
모든 사건들은 사물간의 상호작용이다.

- 객체 지향 이론은 상속, 캡슐화 , 추상화 개념을 중심으로 점차 구체적으로 발전 되었으며 1960년대 중반에 객체지향이론을 프로그래밍언어에 적용한 **시뮬라**라는 최초의 객체지향 언어가 탄생하였다.

- FORTRAN , COBOL과 같은 절차적 언어가 주류를 이루다 , 1980년 C++을 비롯하여 여러 객체 지향언어가 발표되면서 본격적으로 객체 지향언어가 대두됨.

- 제임스 고슬링에 의해 자바가 1995년에 발표되고 1990년대 말에 인터넷 발전과 함께 크게 유행하면서 객체지향언어는 프로그래밍 언어의 주류가됨.

<br/>

**객체 지향 언어의 주요 특징**

1. 코드의 재사용성이 높다
    - 새로운 코드를 작성할 떄 , 기존의 코드를 이용하여 쉽게 작성가능
<br/>  
2. 코드의 관리가 용이하다.
    - 코드간의 관계를 이용해서 적은 노력으로 쉽게 코드를 변경 할 수 있다.
<br/>
3. 신뢰성이 높은 프로그래밍을 가능하게 한다
    - 제어자와 메서드를 이용해서 데이터를 보호하고 올바른 값을 유지하도록 하며, 코드의 중복을 제거하여 코드의 불일치로 인한 오동작을 방지할 수 있다.
<br/>

>상속, 다형성은 객체지향 개념의 핵심이다.
>
>너무 객체지향에 얽매여서 고민하기 보다는 프로그램을 기능적으로 작성 후 객체지향적 코드로 개선 할 수 있을지를 고민하면서 리펙토링 하는것이 좋다.    

<br/>

---

### 2. 클래스와 객체

**클래스 ❓**
>객체를 정의해놓은 것, 객체의 설꼐도 또는 틀

<br/>

**객체 ❓**
>실제로 존재하는 것, 사물 또는 개념, 객체가 가지고 있는 기능과 속성에 따라 다름
>
>**프로그래밍**에서 객체는 클래스에 정의된 내용대로 메모리에 생선된 것을 뜻한다.

<br/>

**클래스와 객체의 관계 ❓**

| 클래스 | 객체 |
| --- | --- |
| 제품설계도 | 제품 |
| TV 설계도 | TV |
| 붕어빵 기계  | 붕어빵 |

<br/>

 클래스를 정의하고 클래스를 통해 객체를 생성하는 이유는 설계도를 통해서 제품을 만드는 이유와 같다. 하나의 설계도만 잘 만들어 놓으면 제품을 만드는 일이 쉬워진다. 매번 고민 할 필요 없이 설계도대로만 만들면 되기 때문이다.

 <br/>

**즉, 객체 생성시 클래스로부터 객체를 생성해서 사용하면 된다.**
또한, JDK에서는 프로그래밍을 위한 유용한 클래스(Java API)를 기본적으로 제공하고 있으며, 이 클래스들을 이용하여 원하는 기능의 프로그램을 보다 쉽게 작성할 수 있다.
<br/>

**API ❓**
> 응용 프로그램 프로그래밍 인터페이스로 프로그래밍 언어를 제어 할 수있게 만든 인터페이스 이다. 보통 Public 으로 API로 만들어 둔다.

<br/>


**객체와 인스턴스❓**

>클래스로부터 객체를 만드는 과정을 클래스의 인스턴스화 라고 하며, 어떤 클래스로부터 만들어진 객체를 그 클래스의 인스턴스라고 한다.

객체가 인스턴스의 포괄적인 의미라면 **인스턴스는 어떤 클래스로부터 만들어진 것인지 강조하는 보다 구체적인 의미를 갖고 있다.**

<br/>

**클래스 → 인스턴스화 → 인스턴스(객체)**
- 객체와 인스턴스는 보통 같은 의미로 보아도 무방하지만, 위 처럼 문맥에 따라 구별하여 사용하는 것이 좋다.

<br/>

**객체의 구성요소 - 속성과 기능**
>객체는 속성과 기능, 두 종류의 구성요소로 이루어져 있으며, 일반적으로 객체는 다수의 속성과 기능을 갖는다. 즉, 객체는 속성과 기능의 집합이라고 할 수 있다.<br/>
>
>속성(property) 맴버 변수(member variable), 특성(attribute), 필드(field), 상태(state)
기능(function) 메서드(method), 함수(function), 행위(behavior)

<br/>
예를 들어 TV라는 객체는 다음과 같이 속성과 기능으로 분리할 수 있다.
- 속성: 크기,길이,높이,볼륨,채널 등
- 기능: 켜기,끄기,볼륨 업, 볼륨 다운, 채널 변경 등

코드로 본다면 다음과 같다.

```

Public Class TV{
	int channel;
    //속성
    
    public int channelUp(){
    //기능
    	this.channel++;
    }
}

```

<br/>

**인스턴스의 생성과 사용**

객체의 속성과 기능을 사용하려면, 인스턴스를 생성해야 사용 할 수 있다.
객체의 생성 방법은 여러가지가 있지만 일반적으로는 아래와 같이 작성한ㄷ

> 클래스명 변수명; // 클래스의 참조변수 선언 <br/>
> 변수명 = new 클래스명(); // 클래스의 객체 생성후, 객체의 주소를 참조변수에 저장;<br/>
>
> Tv t;<br/>
> t = new Tv();<br/>

<br/>

Tv클래스 만들기 실습

- Tv.class

```

package ch06_createInstance;

public class Tv {
    
    //Tv의 속성을 정의합니다.(맴버변수(=인스턴스맴버))
    String color; //색상
    boolean power; // 전원 상태(on/off)
    int channel; //채널
    
    //Tv의 기능(메서드)
    void power() {
        power = !power; //Tv의 전원을 끄는 기능
    }
    
    void channelUp() {
        channel++; //Tv의 채널을 높이는 기능
    }
    
    void channelDown() {
        channel--; //Tv의 채널을 낮추는 기능
    }
    
}

```

<br/>

- TvExample.class

```

package ch06_createInstance;


public class TvExample {
    public static void main(String[] args) {
        
        Tv tv;  // Tv객체를 생성하기 위해 변수 tv 생성후
        tv = new Tv(); // new 연산자를 통해 인스턴스를 생성
        
        //일반적으로 **Tv tv =  new Tv();** 와 같이 작성
        
        
        //인스턴스변수 tv로 기능(메서드에 아래와 같이 호출)
        
        tv.channel = 7; //클래스 인스턴스 맴버 channel에 7을 셋팅
        tv.channelDown(); //정의해둔 기능에 의해 채널 값 7이 -1된다.
        
        System.out.printf("현재 채널의 값 : %d" , tv.channel);
    }
}


```

<br/>

TvExample를 차례로 살펴보자

1. Tv tv; <br/>
		- Tv클래스 타입의 참조변수 tv를 선언했다. 이제 메모리에 참조변수 tv의 공간이 마련된다. 아직 인스턴스가 생성되지 않았으므로 참조변수로 아무것도 할수 없다.

2. tv = new Tv(); <br/>
		- 연산자 new에 의해 Tv클래스의 인스턴스가 메모리에 생긴다. 고유의 주소값을 가지며. 이 때 멤버변수는 각 자료형에 해당하는 기본값으로 초기화된다.(String color = null; ,boolean power = null; ,int Channel = 0; )
		-  대입 연산자(=) 에 의해서 객체의 **주소값**이 참조변수 tv에 저장된다. 이제 참조변수 tv를 통해 Tv의 인스턴스에 접근이 가능하다. (Tv의 인스턴스: 인스턴스변수: color,power,channel / 메서드 : power(), channelUp(), channelDown())        
3.  tv.channel = 7; <br/>
		- 참조변수 tv에 저장된 주소에 있는 인스턴스의 멤버변수 channel에 7을 저장한다. 참조변수로의 접근은 도트연산자(.)을 통해 위와같이 가능하다.
        
4. tv.channelDown() <br/>
		- 참조변수 t가 참조하고 있는 Tv의 인스턴스의 channelDown메서드를 호출한다. 멤버변수 channel값을 1만큼 감소시킨다. 따라서 channel의 값은 6이 된다.

5. System.out.printf("현재 채널의 값 : %d" , tv.channel); <br/>
		- 참조변수 tv가 참조하고 있는 channel의 값을 출력한다. 현재 값은 6이니 **현재 채널의 값 : 6** 이 출력된다.
        
<br/>

> 위와같이 인스턴스는 참조변수를 통해서 접근하며 참조 변수의 타입은 인스턴스의 타입과 일치 해야한다.

<br/>

다음은 같은 클래스에서 두개의 참조변수로 객체를 생성해보는 예제이다.
<br/>

- Tv.class

```

package ch06_createInstance;

public class Tv {
    
    //Tv의 속성을 정의합니다.(맴버변수(=인스턴스맴버))
    String color; //색상
    boolean power; // 전원 상태(on/off)
    int channel; //채널
    
    //Tv의 기능(메서드)
    void power() {
        power = !power; //Tv의 전원을 끄는 기능
    }
    
    void channelUp() {
        channel++; //Tv의 채널을 높이는 기능
    }
    
    void channelDown() {
        channel--; //Tv의 채널을 낮추는 기능
    }
    
}

```

- TvExample2.class

```

package ch06_createInstance;


public class TvExample2 {
    public static void main(String[] args) {
        
        Tv tv1 = new Tv(); // 변수이름 tv1인 Tv객체 생성 
        Tv tv2 = new Tv(); // 변수이름 tv2인 Tv객체 생성 
        
        System.out.printf("tv1의 현재 채널의 값 : %d\n" , tv1.channel);
        System.out.printf("tv2의 현재 채널의 값 : %d\n" , tv2.channel);
        
        tv1.channel = 7;
        System.out.printf("tv1의 현재 채널의 값 : %d로 변경 하였습니다\n" , tv1.channel);
        
        System.out.printf("현재 채널의 값 : %d\n" , tv1.channel);
        System.out.printf("현재 채널의 값 : %d\n" , tv2.channel);
    }
}

```

> **실행결과** <br/>
> tv1의 현재 채널의 값 : 0 <br/>
> tv2의 현재 채널의 값 : 0 <br/>
> tv1의 현재 채널의 값 : 7로 변경 하였습니다 <br/>
> 현재 채널의 값 : 7 <br/>
> 현재 채널의 값 : 0 <br/>

</br>


1. Tv tv1 = new Tv(); <br/> Tv tv2 = new Tv(); <br/>
		- tv1과 tv2는 같은 클래스로부터 생성 되었을지라도, 생성시 다른 주소값을 부여받게된다.

2. tv1.channel = 7; <br/>
		- 따라서 위의 코드는 tv1이 참조하고 있는 참조변수 channel에만 7의 값이 셋팅된다.
<br/>

>즉 , 같은 클래스로부터 생성 되었을지라도 인스턴스 속성(멤버변수)의 값은 서로 다른 값을 유지할 수 있으며, 메서드의 내용은 모든 인스턴스에 대해 동일하게 작동한다.

<br/>

다음은 참조변수 tv1의 값을 tv2에 대입해보는 예제이다.

- Tv.class

```

package ch06_createInstance;

public class Tv {
    
    //Tv의 속성을 정의합니다.(맴버변수(=인스턴스맴버))
    String color; //색상
    boolean power; // 전원 상태(on/off)
    int channel; //채널
    
    //Tv의 기능(메서드)
    void power() {
        power = !power; //Tv의 전원을 끄는 기능
    }
    
    void channelUp() {
        channel++; //Tv의 채널을 높이는 기능
    }
    
    void channelDown() {
        channel--; //Tv의 채널을 낮추는 기능
    }
    
}

```

- TvExample2.class

```

package ch06_createInstance;


public class TvExample3 {
    public static void main(String[] args) {
        
        Tv tv1 = new Tv(); // 변수이름 tv1인 Tv객체 생성 
        Tv tv2 = new Tv(); // 변수이름 tv2인 Tv객체 생성 
        
        System.out.printf("tv1의 현재 채널의 값 : %d\n" , tv1.channel);
        System.out.printf("tv2의 현재 채널의 값 : %d\n" , tv2.channel);
        
        tv2 = tv1; // t1의 주소값을 t2에 대입한다. 즉, 둘의 주소값이 같아진다.
        tv1.channel = 7;
        System.out.printf("tv1의 현재 채널의 값 : %d로 변경 하였습니다\n" , tv1.channel);
        
        
        
        System.out.printf("현재 채널의 값 : %d\n" , tv1.channel);
        System.out.printf("현재 채널의 값 : %d\n" , tv2.channel);
    }
}

```

<br/>

>**실행결과** <br/>
>tv1의 현재 채널의 값 : 0 <br/>
>tv2의 현재 채널의 값 : 0 <br/>
>tv1의 현재 채널의 값 : 7로 변경 하였습니다 <br/>
>현재 채널의 값 : 7 <br/>
>현재 채널의 값 : 7 <br/>

<br/>

1. Tv tv1 = new Tv(); <br/> Tv tv2 = new Tv(); <br/>
		- tv1과 tv2는 같은 클래스로부터 생성 되었을지라도, 생성시 다른 주소값을 부여받게된다.

2. tv2 = tv1; <br/>
		- 이 코드에서 tv1의 인스턴스의 주소값과 tv2의 인스턴스 주소값이 같아진다. tv2가 원래 가지고 있던 주소 값은 사라진다. 즉, tv2가 참조하고 있던 인스턴스는 더이상 사용 할 수 없다.
        
3. tv1.channel = 7; <br/>
		- tv1가 참조하고있는 인스턴스 멤버 channel값이 7이된다. (tv2도 동일)

4. System.out.printf("현재 채널의 값 : %d\n" , tv1.channel); <br/>
        System.out.printf("현재 채널의 값 : %d\n" , tv2.channel); <br/>
        - tv1, tv2 동일한 주소값에 7이라는 값이 셋팅되었으므로, 두 값 모두 7이 출력된다.

<br/>

>둘 이상의 참조변수가 하나의 인스턴스를 참조하는 것은 가능하지만 하나의 참조 변수로 여러개의 인스턴스를 가리키는 것은 가능하지 않다.

<br/>

**인스턴스의 생성과 사용**

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

<br/>


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

**클래스의 또 다른 정의**

- 프로그래밍적인 관점에서 클래스의 정의와 의미를 살펴보도록 하자.

1. 클래스 - 데이터와 함수의 결합
프로그래밍언어에서 데이터 처리를 위한 데이터 저장형태의 발전과정은 다음과 같다.
<br/>

변수 -> 배열 -> 구조체 -> 클래스
<br/>

- 변수: 하나의 데이터를 저장할 수 있는 공간
- 배열: 같은 종류의 여러 데이터를 하나의 집합으로 저장할 수 있는 공간
- 구조체 서로 관련된 여러 데이터를 종류에 관계없이 하나의 집합으로 저장할 수 있는 공간
- 클래스 데이터와 함수의 결합( 구조체 + 함수 )
<br/>

> 변수와 함수를 유기적으로 연결시켜 작업을 간단하고 명료해질 수 있도록 점점 변화됨.

<br/>

2. 클래스 - 사용자정의 타입
사용자 정의 타입이란, 프로그래밍언어에서 제공하는 자료형 외에 서로 관련된 변수들을 묶어서 하나의 타입으로 새로 추가하는 것을 사용자정의 타입(user-defined-type) 이라고 한다.
<br/>
자바에서는 클래스가 곧 사용자 정의 타입이다.

또한 아래와 같은 조건이 주어져 있을때, 객체지향언어는 데이터의 추가적 조건들을 반영하기 용이하다

> **1. 시분초는 모두 0보다 크거나 같아야 한다.**
> **2.시의 범위는 0~23, 분과 초의 범위는 0~59이다.**

위의 조건을 준수하여 코드를 작성해보자

```

package ch06_createInstance;

public class Time {
	
	private int hour;
	private int minute;
	private float second;
	
	public int getHour() {
		return hour;
	}
	public int getMinute() {
		return minute;
	}
	public float getSecond() {
		return second;
	}
	
	public void setHour(int h) {
		if (h<0|| h>23) {
			return;
		}
		hour = h;
	}
	public void setMinute(int m) {
		if (m<0 || m>59) {
			return;
		}
		minute = m;
	}
	public void setSecond(float s) {
		
		if (s < 0.0f || s > 59.99f) {
			return;
		}
		 second = s;
	}
	
}


```

<br/>
위와같이 시간 구성요소인 (hour, minute, second) 변수를 선언하고 시간을 설정하는 set~ 메서드를 통해 시간을 셋팅한다. 셋팅하는 메서드에 if문으로 유효성을 점검후 유효한 값일때에만 인스턴스 멤버변수에 저장한다.

--- 

### 변수와 메서드

**선언위치에 따른 변수의 종류**

<br/>

| 변수의 위치 | 선언위치 | 생성시기 |
| --- | --- | --- |
| 클래스변수 | 클래스 영역 | 클래스가 메모리에 올라갈 때 |
| 인스턴스변수 | 클래스 영역 | 인스턴스가 생성되었을 떄 | 
| 지역변수 | 클래스 영역 이외(메서드,생성자,초기화 블럭 내부) | 변수 선언문이 수행되었을 때 |

<br/>

- 클래스 변수
	- 클래스 변수를 선언하는 방법은 인스턴스 변수 앞에 static을 붙인다.
    - 인스턴스 변수가 독립적인 저장공간을 갖는 인스턴스 변수와는 달리, 클래스변수는 모든 인스턴스가 공통된 저장공간을 공유한다. 따라서 **공통적인 값을 유지해야하는 속성의 경우, 클래스 변수로 선언한다.**
    - 클래스 변수는 인스턴스 변수와 달리 인스턴스를 생성하지 않고 언제라도 바로 사용 할수 있다.('클래스이름.클래스변수')
    - 클래스가 메모리에 '로딩' 될 떄 생성되어 프로그램 종료시 까지 유지 되며 public을 앞에 붙이면 프로그램 어디에서나 접근 가능한 전역변수의 성격을 갖는다.

<br/>

- 인스턴스 변수
	- 클래스 영역에 선언되며, 클래스의 인스턴스 생성시 만들어진다.
    - 인스턴스가 생성되어야 사용 가능하다.
    - 인스턴스 변수는 독립적인 저장곤간을 가지므로 서로 다른 값을 가질 수 있다.
    - 인스턴스마다 고유한 상태를 유지해야하는 속성의 경우 인스턴스변수로 선언한다.
    
<br/>

- 지역변수
	- 메서드 내에 선언된다. 메서드내에서만 사용가능하다.
    - 메서드가 종료되면 소멸되어 사용 할 수 없다.(실행블록 {} 종료시)
    - 대표적으로 for문에 관례적으로 사용하는 'int i' 같은 변수를 지역변수라 한다.

<br/>

**클래스 변수와 인스턴스 변수**

카드 클래스를 정의하여 클래스 변수와 인스턴스 변수의 차이를 알아보자

> 카드는 무늬, 숫자, 폭, 높이의 속성을 갖는다.

<br/>

- Card.class

```
package ch06_variableAndMethod;

public class Card {
	
	String kind; //무늬
	int number; //숫자
	
	static int width = 100; //폭 
	static int height = 250; // 높이
}

```
<br/>

> 무늬(kind)랑 숫자(number)는 카드 마다 다를 수 있기에 인스턴스 변수, 폭과 높이는 카드 모두가 같은 값을 가지므로 클래스변수로 선언한다.

<br/>

```

package ch06_variableAndMethod;

public class CardExample {
	public static void main(String[] args) {
		
		System.out.println("Card.width = " + Card.width);
		System.out.println("Card.height = " + Card.height);
		
		Card c1 = new Card();
		c1.kind = "Heart";
		c1.number = 7; 
		//카드객체1 - 하트 7생성
		
		Card c2 = new Card();
		c2.kind = "Spade";
		c2.number = 4;
		//카드객체2 - 스페이드 4생성
		
		System.out.printf("c1은 %s,%d 이며 높이는 %d 폭은 %d 입니다.\n", c1.kind, c1.number, Card.height, Card.width);
		System.out.printf("c2은 %s,%d 이며 높이는 %d 폭은 %d 입니다.\n", c2.kind, c2.number, Card.height, Card.width);
        
		/*
        인스턴스 변수를 통해서 클래스변수에 접근 할 수 있지만 일반적으로는 클래스.클래스변수로 제어해야 이클립스에서 		 경고를 보내지 않는다.
        */
		
		System.out.printf("c1의 높이와 폭을 각각 80, 50으로 변경합니다.\n");
		System.out.println();
        
		c1.width = 50;
		c1.height = 80;
		
		System.out.println("변경 후");
		System.out.printf("c1은 %s,%d 이며 높이는 %d 폭은 %d 입니다.\n", c1.kind, c1.number, Card.height, Card.width);
		System.out.printf("c2은 %s,%d 이며 높이는 %d 폭은 %d 입니다.\n", c2.kind, c2.number, Card.height, Card.width);
	}
}

```

클래스 변수는 '클래스이름.클래스변수' 로 호출해야한다.(인스턴스 변수로 호출시, 올바른 클래스 멤버변수 호출법이 아니라고 경고를줌)<br/>
클래스 변수 width와 height는 c1,c2 인스턴스 모두 공유 하기 떄문에 인스턴스변수 c1.width, c1.height 만 변경한다해도 인스턴스 c2도 참조하는 값이 같기 때문에 바뀐 값이 동일하게 적용된다.
<br/>
> 클래스 변수는 모든 인스턴스가 하나의 저장곤간을 공유하므로 항상 공통된 값을 갖는다.

<br/>

**메서드**

'**메서드(Method)**'는 특정 작업을 수행하는 일련의 문장들을 하나로 묶은 것, 수학의 함수와 유사함. 호출 시 메서드의 과정은 일체 몰라도 됨, 필요한 값, 결과만 알면 된다.
<br/>

**메서드를 사용하는 이유 ❓**

1. 높은 재사용성

2. 중복 코드의 제거

- Add.class

```
package ch06_variableAndMethod;

public class Add {
	
	int a = 7;
	int b = 6;
	int c = 13;
	int d = 9;
	
	//두개의 정수값을 받아 더하는 메서드
	public int plus (int a, int b) {
		return a + b;
	}
}

```

- AddExample.class 

```
package ch06_variableAndMethod;

public class AddExample {
	public static void main(String[] args) {
		int result;
		Add add = new Add();
		
		
		result = add.a + add.b;
		result = add.c + add.d; //중복되는 연산이 보인다.
		
		//메서드를 만들면 값을 주고 호출만 하면 끝이다.
		result = add.plus(add.a, add.b);
		
		
	}
}

```
<br/>

> 코드 수정시에도 반복되는 작업일시 메서드 부분만 고치면 되고, 중복또한 제거가 된다. 코드 유지보수 측면에서 훨씬 효울적인 코드가 된다.

<br/>

3. 프로그램의 구조화

프로그램 작성시 하나의 메서드에는 수많은 코드를 넣어 관리 하게 된다면 구조가 매우 복잡해질 뿐더러 나중에 관리 하기가 힘들어 진다. 따라서 프로그램의 구조화를 시키기위해서라도 메서드를 작업단위로  만들고 관리 하는것은 필수불가결하다.

<br/>

```

package ch06_variableAndMethod;

public class AddExample2 {
	public static void main(String[] args) {
		int result;
		double divideResult;
		Add add = new Add();
		
		result = add.plus(10, 20);
		System.out.println("더하기 : " + result);
		result = add.minus(10, 5);
		System.out.println("빼기 : " + result);
		result = add.multiple(2, 3);
		System.out.println("곱하기 : " + result);
		divideResult = add.divide(10, 3);
		System.out.println("나누기 : " + divideResult);
	
		
	}
}

```
<br/>

> 실행시키는 곳에서는 단순히 호출만 하면된다.

<br/>

**메서드의 선언과 구현**

메서드는 크게 선언부와 구현부로 나누어져 있다.

```

**선언부 : 반환타입 메서드 이름(타입 변수명, 타입 변수명, ... )**{
	
    // 구현부 : 메서드 호출시 수행될 코드
}

```

<br/>

- **메서드 선언부(method declaration , method header)**
	- 메서드의 선언부는 '메서드의 이름' 과 '매개변수 선언' 그리고 '반환 타입'으로 구성되어 있으며, 메서드가 작업을 수행하기 위해 어떤 값들을 필요로 하고 작업의 결과로 어떤 타입의 값을 반환하는 지에 대한 정보를 제공한다.
<br/>

- **매개변수 선언(parameter declaration)**
	- 메서드가 작업을 수행하는데 필요한 값을 제공, 변수간의 구분은 쉽표를 사용, 매개변수의 타입은 생략할 수 없음
    - 매개변수에 배열이나 , 참조변수를 사용해도 됨, 매개변수를 전혀 받지 않을경우 생략가능
<br/>

- **메서드의 이름(method name)**
	- 메서드의 이름또한 변수의 명명규칙대로 작성하면된다.
    - 동사인 경우가 많다.
    - 함축적이고 의미있는 이름을 명명하도록 노력해야한다.
    
- **반환타입(return type)**    
	- 메서드의 작업수행 결과로 생기는 값이다.
    - 반환 값이 없는 경우 **void** 있는 경우 **반환받을 타입** 을 메서드 이름 앞에 명시해주면 된다.    
<br/>    

- **메서드 구현부(return type)** 
	- 메서드 구현부는 실행블록({ }) 안의 코드를 말한다.
<br/>

- **return문**        
	- 리턴타입이 void가 아닌 경우 반드시 메서드의 반환값이 return 값으로 주어져야한다.
    - 리턴타입은 반환타입과 일치하거나 적어도 자동 형변환이 가능한 것이 어야 한다.
    - 매개변수는 여러개 일수 있어도 반환 값은 **최대 하나**만 허용 된다.

<br/>
**JVM의 메모리구조**

![JVM메모리구조](https://user-images.githubusercontent.com/85389189/133498489-062b57ce-448e-4736-9e81-4f7c1fc3f1c9.png)




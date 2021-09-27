---
layout: post
title:  "면접 질문 리스트"
subtitle:   "면접 질문을 모아 둡니다."
categories: etc
tags: etc
comments: true
---
## 개요
> 면접을 위한 정리

- 목차
   - 쓰레드의 임계영역


***

## 쓰레드 임계영역
----
- 멀티스레드가 구현된 프로그램 안에서 두 개 이상의 쓰레드가 동시에 어떤 기능을 수행함에 있어 두개의 쓰레드가 만약 어떤 자원(변수) 같이 공유해서 사용하는 경우가 있다고 하자.
<br/>
- 각각의 쓰레드가 이 자원(변수) 특정한 값으로 수정하는 기능이 있다면 동시에 접근하는 이유로 인하여 이 자원의 값이 제대로 된 값을 유지하지 못하는 경우가 있을 수 있다.
<br/>
- 이 경우 한번에 하나의 Thread에게만 접근을 허용하고 싶다고 하는 영역을 "임계영역"이라고 한다.
<br/>
- 자바에서는 이러한 임계영역의 처리를 위하여 아래와 같은 내용은 제공한다.
synchronized 키워드를 제공
<br/>
- 임계 영역에 접근하는 기능을 갖고 있는 메소드 앞에 synchronized 키워드를 붙이면 자동으로 임계영역 설정이 되어 한번에 하나의 쓰레드에게만 접근을 허용할 수 있다.
<br/>
- 즉 멀티쓰레드가 구현된 프로그램안에서 두개 이상의 쓰레드 동시에 어떤 일을 수행하지만 임계영역에 어떤 쓰레드가 먼저 접근하면 lock을 걸어 다른 쓰레드가 동시에 접근 못하도록 관리 된다.
<br/>
- 또, 메소드전체를 synchronized 할 수도 있고, 메소드의 일부분만 synchronized 할 수도 있다.

<br/>

```

public synchronized 리턴타입 someMethod(매개변수...)
{
	명령어
}
public 리턴타입 someMethod(매개변수)
{
	명령어1;
	명령어2;

	synchronized{
		명령어3;
	}

	명령어4;
}


```

## 임계영역 예제

- 50만원 모금액에 도달할 때 까지 5명의 기부자가 경쟁적으로 돈을 입금하는 것. 동시에 입금이 안되도록 하기 위해 synchronized 메소드 사용

- 임계영역 설정 하기 위해서는 synchronized를 메소드에 붙여야 한다.

<br/>

- 계좌 클래스

```

package com.sun.test01;

public class Account {
	private int balance;

	public int getBalance() {
		return balance;
	}

	public synchronized void deposit(int amount)
	{
		balance = balance + amount;
		//System.out.println("현재잔액 : "+balance);
	}
}



```

- 기부자 클래스

```

package com.sun.test01;

public class Donation extends Thread{
	private String name;
	private Account account;

	public Donation(String name, Account account) {
		super();
		this.name = name;
		this.account = account;
	}

	@Override
	public void run() {
		// TODO Auto-generated method stub

		for(int i = 1 ; ; i++)
		{
			if (account.getBalance() >= 500000)
				break;

			System.out.println(name+"의"+i+"번째 입금");
			account.deposit(1000);

			try {
				Thread.sleep(100);
			}catch (Exception e) {
				// TODO: handle exception
			}
		}
	}
}


```

- main 클래스

```
package com.sun.test01;

public class DonationTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Account account = new Account();
		Donation donation1 = new Donation("홍길동",account);
		Donation donation2 = new Donation("김동동",account);
		Donation donation3 = new Donation("박자바",account);
		Donation donation4 = new Donation("정프로",account);
		Donation donation5 = new Donation("이강의",account);

		donation1.start();
		donation2.start();
		donation3.start();
		donation4.start();
		donation5.start();

		try {
			donation1.join();  //객체명.join()은 이것이 다 끝난 뒤에 실행하라고 하는 메소드
			donation2.join();
			donation3.join();
			donation4.join();
			donation5.join();
		}catch (Exception e) {
			// TODO: handle exception
		}

		System.out.println("총 모금액 : "+account.getBalance());
	}

}


```

***

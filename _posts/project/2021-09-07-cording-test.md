---
layout: post
title:  "코딩테스트를 위한 준비"
subtitle:   "코딩테스트 정리"
categories: etc
tags: etc
comments: true
---
# 이것이 코딩 테스트다

<br/>

**깃: [https://github.com/naru92/cording_test](https://github.com/naru92/cording_test)**

<br/>

##### 목차

<br />

[1. 복잡도](#1.복잡도)
- [시간복잡도](#시간-복잡도)
- [빅오(Big-O) 표기법](#빅오(Big-O)-표기법)
- [시간과 메모리 측정](#시간과-메모리-측정)
- [최신 출제 경향과 준비 방향](#최신-출제-경향과-준비-방향)

2. [그리디 알고리즘](#그리디-알고리즘)

## 1.복잡도

**복잡도는 알고리즘의 성능 나타내는 척도이다.**

- 시간복잡도 : 특정한 크기의 입력에 대하여 알고리즘이 얼마나 오래걸리는지
- 공간복잡도 : 특정한 크기의 입력에 대하여 얼마나 많은 메모리를 차지하는지

> 동일한 기능을 수행하는 알고리즘이 있다면 일반적으로 복잡도가 낮을수록 좋은 알고리즘이다.

<br/>

효율적인 알고리즘을 사용한다고 했을 때 보통 시간 복잡도와 공간 복잡도는 일종의 거래관계가 성립한다. 메모리를 조금 더 많이 사용하는 대신에 반복되는 연산을 생략하거나, 더 많은 정보를 관리하면서 계산의 복잡도를 줄일 수 있다. (메모리제이션)

<br />


### 시간 복잡도

- 알고리즘 문제를 풀 때 단순히 복잡도라 함을 시간 복잡도를 의미함
- 시간안에 동작 하는 코드를 만들어야함, 넘을시는 시간 초과

<br />

### 빅오(Big-O) 표기법

-O(N) : N에 비례한 연산횟수, N 만큼 연산횟수도 증가

```

public class Complexity {
		public static void main(String[] args) {

			int[] array = {3, 5, 1, 2, 4}; // 5개의 데이터 (N = 5)
			int summary = 0;

			// 모든 데이터를 하나씩 확인하며 합계를 계산
			for(int x : array) {
				summary += x;
			}

			System.out.println(summary);
		}

}

```
아래의 코드도 a+n의 출력 함수를 무시하고보면 연산횟수는 1이다
시간 복잡도는 O(1)로 표현

```

int a = 5
int b = 7

System.out.println(a + b);

```
아래의 코드는 리스트 변수의 길이가 N개일때, O(N2)의 시간 복잡도를 가진다.
2중 반복문을 이용하여 각 원소에 대하여 다른 모든 원소에 대한 곱셈결과를 매번 출력하고 있기 때문이다. 따라서 N * N 만큼의 연산이 필요하다는것을 유추 할 수 있다.

- 하지만 모든 2중 반복문의 시간복잡도가 O(N2)는 아니다. 만약 소스코드가 내부적으로 다른 함수를 호출한다면 내부 함수의 시간 복잡도 까지 고려해야하므로, 소스코드를 정확히 분석 할 줄 알아야한다.

> 일반적으로 코딩 테스트에서는 최악의 경우에 대한 연산 횟수가 가장 중요함.
그러니 최악의 경우의 시간 복잡도를 우선적으로 고려해야한다.

```

public class Complexity1 {
		public static void main(String[] args) {

			int[] array = {3, 5, 1, 2, 4}; // 5개의 데이터 (N = 5)
			int count = 0;

			// 모든 데이터를 하나씩 확인하며 합계를 계산
			for(int i : array) {
				for(int j : array) {

					int temp = i * j ;
					System.out.println(temp);
					count++;
				}
			}			
			System.out.println("실행숫자 : " +  count);
		}


}

```

---

**시간 복잡도 표**

| 빅오표기법 | 명칭|
| --- | --- |
| O(1) | 상수시간(Constant time) |
| O(logN) | 로그시간(Log time) |
| O(N) | 선형시간 |
| O(NlogN) | 로그 선형시간 |
| O(N2) | 이차시간 |
| O(N3) | 삼차시간 |
| O(2n) | 지수시간 |

- 위에 있을수록 빠른 순서

<br />

일반적으로 O(N3)를 넘어가면 문제풀이에서 사용하기 어렵다. 연산횟수가 10억을 넘어가면 C언어를 기준으로 통상 1초이 시간이 소요된다. 이때 N의 크기가 5,000이 넘는다면 족히 10초 이상의 시간이 걸릴 수 있다. 코딩 테스트에서 시간제한은 1 ~ 5초 가량이므로 연산횟수가 10억을 넘는다면 오답 판정을 받을 수있다.

<br />

|  | N이 1,000일때의 연산 횟수 |
| --- | --- |
| O(1) | 1,000 |
| O(logN) | 10,000 |
| O(N2) | 1,000,000 |
| O(N3) | 1,000,000,000 |

<br />

>보통 시간 복잡도에서의 '연산'은 프로그래밍 언어에서 지원하는 사칙연산, 비교연산 등과 같은 기본 연산을 의미한다. 예를 들어 두 정수 a와 b를 더하는 더하기 연산뿐만 아니라, 두 정수 a와 b의 값을 비교하는 비교 연산 또한 한 번의 연산으로 취급한다

<br/>

시간 복잡도 분석은 문제 풀이의 핵심이다.

<br/>

**일반 적으로 문제를 풀 때 의 예시**

- N의 범위가 500인 경우: 시간 복잡도가 O(N3)인 알고리즘을 설계하면 문제를 풀 수 있다.
- N의 범위가 2,000인 경우: 시간 복잡도가 O(N2)인 알고리즘을 설계하면 문제를 풀 수 있다.
- N의 범위가 100,000인 경우: 시간 복잡도가 O(NlogN)인 알고리즘을 설계하면 문제를 풀 수 있다.
- N의 범위가 10,000,000 경우: 시간 복잡도가 O(N)인 알고리즘을 설계하면 문제를 풀 수 있다.

<br/>

**공간 복잡도**
공간 복잡도를 표기할 때도 시간 복잡도를 표기했던 것처럼 빅오 표기법을 이용한다.
도 또한 O(NlogN), O(N2) 등으로 표기한다. 다만, 앞서 시간 복잡도에서 1초라는 절대적인 제한이 있던 것 처럼, 메모리 사용량에도 절대적인 제한이 있다.

<br />
코딩 테스트 문제를 대부분 리스트(배열)를 사용해서 풀어야 한다.


- int a[1000] : 4KB
- int a[1000000] : 4MB
- int a[2000][2000] : 16MB

<br />

코딩 테스트에서는 보통 메모리 사용량을 128 ~ 512MB 정도로 제한한다.
다시 말해 일반적인 경우 데이터의 개수가 1,000만 단위가 넘어가지 않도록 알고리즘 설계를 해야한다는 의미이다. 만약 리스트의 크기가 1,000만 단위 이상이라면 잘못된 알고리즘을 설계 한 것이다.

### 시간과 메모리 측정

> 알고리즘을 공부하는 과정에서 시간을 측정하는 작업을 굉장히 많이 사용한다. 알고리즘의 소요시간을 확인해야 자신의 알고리즘이 제대로 작성 됐는지 체크 할 수 있다.

```

long beforeTime = System.currentTimeMillis(); //코드 실행 전에 시간 받아오기

//실험할 코드 추가

long afterTime = System.currentTimeMillis(); // 코드 실행 후에 시간 받아오기
long secDiffTime = (afterTime - beforeTime)/1000; //두 시간에 차 계산
System.out.println("시간차이(m) : "+secDiffTime);

```

<br />

### 최신 출제 경향과 준비 방향
![request매핑get지정호출](/assets/request매핑get지정호출.png)

- 그리디 구현 (다수)
- DFS/BFS 활용
- 다이나믹 프로그래밍
- 그래프 이론
- 정렬
- 이진 탐색


> 보통 절반 이상을 맞춰여 합격선에 들어간다.

<hr />

### 알고리즘 문제 풀이 사이트
<br/>

- [코드 시그널](https://app.codesignal.com)

>비교적 최근에 생김 알고리즘 문제풀이 및 해설을 제공, 초보자에게 적합
  단계별 문제 제공(게임처럼)

<br/>

- [코드포스](https://codeforces.com)

>가장 유명한 알고리즘 문제사이트, 2020년 기준으로 매주 1회이상 주기적으로 대회가 열림
rating 제도, 블루등급이 대체로 코딩테스트를 무난하게 통과

<br/>

- [정올](http://www.jungol.co.kr)

>국내 유명 문제 사이트로 , 정보 올림피아드 약자로 정보 올림피아드 기출문제를 만날 수 있는 사이트 , 다양한 기초문법 활용 단계를 제공, 입문자들도 빠르게 적응 가능

<br/>

-[BOJ Slack](https://acmicpc.slack.com)

>백준 온라인 저지 슬랙m 백준 온라인 저지에서 알고리즘 문제를 풀며 활동하고 있는 사람들이 모여있는곳, 알고리즘에 대한 이야기를 나눌수 있고 Q&A채널에는 질문도 가능하다.
SLACK에서 이용가능하다.

<br />
<hr />

##2.그리디 알고리즘

- ### 거스름돈
> 대표적인 그리디 알고리즘

<br />

*문제 . 1260원을 거슬러주자 화폐 종류는 각각 500,100,50,10 존재한다.*

---

풀이<br/>
```

public class Greedy {
//1260원 거슬러주기 사용화폐 500,100,50,10

	public static void main(String[] args) {

		int n = 1260;
		int count = 0;

		int[] coin_type = {500, 100, 50, 10};

		for(int coin : coin_type) {

			if (coin > n) {
				continue;
			}

			count += n / coin;
			n %= coin;
		}
		System.out.println(count);

	}

```
<br />

- ### 큰수의 법칙

```
	// 풀이 시간 30분
	// 시간제한 1초
	// 메모리 제한 128MB
	// 기출 2019 국가기관 코딩 테스트

	/*
	 - 입력조건
	 * 첫째 줄에 N(2<=N<=1000), M(1<=M<=10000),K(1<=K<=10000)의 자연수가 주어지며,
	   각 자연수는 공백으로 구분한다.
	 * 둘째 줄에 N개의 자연수가 주어진다. 각 자연수는 공백으로 구분한다. 단, 각각의 자연수는 1 이상
	   10,000 이하의 수로 주어진다.
	 * 입력으로 주어는 K는 항상 M보다 작거나 같다.

	 - 출력조건
	 * 첫째 줄에 사용자의 큰 수의 법칙에 따라 더해진 답을 출력한다.

	*/

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);

		//N, M,K 을 공백을 기준으로 구분하여 입력받기
		int n = scanner.nextInt();
		int m = scanner.nextInt();
		int k = scanner.nextInt();

		int[] arr = new int[n];

		// N개의 수를 공백을 기준으로 구분하여 입력 받기
		for(int i = 0; i< n ; i++) {
			arr[i] = scanner.nextInt();
		}

		Arrays.sort(arr); // 받은수들 정렬하기
		int first = arr[n - 1]; //가장 큰수
		int second = arr[n - 2];//두 번째로 큰 수

		//가장 큰 수가 더해지는 횟수 계산
		int cnt = (m / (k+1)) * k;
		cnt += m % (k+1);

		int result = 0;
		result += cnt * first; //가장 큰 수 더하기
		result += (m-cnt) * second; //두번째 큰 수 더하기

		System.out.println(result);

```

<br/>

---
- ### 1이 될때까지

```

		//문제. 1이 될때까지
		// 어떠한 수 N이 1이 될때까지 두 과정중 하나를 반복적으로 선택하여 수행하려고 합니다.
		// 단, 두번째 연산은 N이 K로 나누어 떨어질 떄만 선택할 수 있습니다.

		/*
		 * 1. N에서 1을 뻅니다
		 * 2. N을 K로 나눕니다
		 *
		 * N과 K가 주어 질때 n이 1이 될 때까지 1번 혹은 2번의 과정을 수행하는 최소 횟수를 구하는 프로그램을 작성하세요
		 * */
		long beforeTime = System.currentTimeMillis(); //코드 실행 전에 시간 받아오기
		Scanner sc = new Scanner(System.in);

		int n = sc.nextInt();
		int k = sc.nextInt();
		int result = 0;


		// 풀이 1
		  while(n != 1) {

		  if(n % k == 0) {
		  //k로 나눠지면 k로 나눔 n = n / k; result++;
		  } else { // k로 나눠지지않으면
		  -1을함 n = n-1; result++; }

		 }

		// 풀이 2
		while(true) {
			int target = (n / k) * k;
			result += (n - target);
			n = target;

			if(n < k) {
				break;
			}
			result += 1;
			n /= k;
		}


		result += (n-1);
		System.out.println(result);
		long afterTime = System.currentTimeMillis();
		long secDiffTime = (afterTime - beforeTime)/1000;
		System.out.println("시간차이(m) : "+secDiffTime);
		sc.close();
	}

```
<br/>

- 풀이1 : 가장 단순한 방법 n이 k로 나누어 떨어지면 k로 나누고 그렇지 않다면
         n-1을 해서 계속 루프를 돔
- 풀이2 : target이라는 변수로 n/k몫을 다시 k에 곱하여 n을뺀 k의 값을 구함
	       다시 n에서 target을 빼서 result변수에 그 나머지를 담음 후에 target의 값을 n에 대입.
				 한번에 나머지를 계산 함, 풀이 1과 달리 수가 커질수록 시간 복잡도는
				 NlogN 으로 훨씬 계산이 빠름

<br />


### 곱하기 혹은 더하기

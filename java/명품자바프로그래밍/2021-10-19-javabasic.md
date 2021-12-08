---
title: JAVA 기본 프로그래밍
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- java
toc: true
toc_sticky: true
toc_label: 목차
description: JAVA 기본 프로그래밍
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-10-19'
---

### 자바 프로그램의 기본구조
자바 프로그램은 여러 개의 클래스로 이루어진다. class 키워드로 클래스 이름을 선언하고 클래스 안에 필드와 메소드 코드를 작성한다.
public은 자바의 접근지정자로서 다른 모든 클래스에서 자유롭게 사용할 수 있다는 선언이다.

main()은 반드시 public, static, void 타입으로 선언되어야 하며, 한 클래스에 2개 이상의 main()을 작성할 수 없다.

````java
public class Hello2030 {
	
	public static int sum(int n, int m) {
		return n + m;
	}	
	//main() 메소드에서 실행 시작: 한 클래스에 1개의 main()을 작성
	//main()은 반드시 public, static, void 타입으로 선언
	public static void main(String[] args) {//public: 접근지정자(access specifier) -> 다른 모든 클래스에서 클래스 Hello2030을 자유롭게 사용할 수 있음

		int i = 20; //정수 타입(4바이트) -> 데이터 공간을 효율적으로 사용하기 위해 데이터 타입 지정
		int s;
		char a; //문자 타입(2바이트)
		
		s = sum(i, 10); //콜스택에 저장 //메소드 호출
		a='?';
		System.out.println(a);
		System.out.println("Hello");
		System.out.println(s);
	}
}
````

### 데이터 타입
자바에서 다룰 수 있는 데이터 타입은 boolean, char, byte, short, int, long, float, double의 8가지 기본 타입과 1가지 레퍼런스 타입이 있다. 레퍼런스는 C/C++의 포인터와 비슷하게 객체를 가리키지만, 실제 메모리 주소를 가지는 것은 아니다.
* 레퍼런스 타입의 용도: 배열에 대한 레퍼런스, 클래스에 대한 레퍼런스, 인터페이스에 대한 레퍼런스
* 무자열(String) 리터럴: 문자열 타입은 String 클래스 타입으로 자바의 기본 타입이 아니다.
* C/C++와 달리 자바에서 숫자를 참, 거짓으로 사용 불가 (예. while(1): x)
* null 리터럴: null은 기본 타입에 사용될 수 없고 객체 레퍼런스에 대입된다.

````java
int n = null; //오류
String str = null; //정상
````

* Java 10부터 지역 변수를 선언할 때 변수의 타입 대신 var 키워드를 사용할 수 있다. 반드시 변수 선언문에 초깃값이 주어져야 한다.

````java
public class CircleArea {

	public static void main(String[] args) {

		final double PI = 3.14; //원주율을 상수로 선언
		double radius = 10.0;
		double circleArea = radius * radius * PI;
		
		System.out.println("원의 면적 = " + circleArea);	
	}
}
````

### 키 입력
System.in은 키보드로부터 직접 입력받는 자바의 표준 입력 스트림 객체로서, 입력된 키에 해당하는 바이트 정보를 리턴한다. 이때 응용프로그램은 받은 바이트 정보를 문자나 숫자로 변환해야 하는 번거로움이 있으므로, 키보드에서 입력된 키를 문자나 정수, 실수, 문자열 등 사용자가 원하는 타입으로 변환해주는 Scanner 클래스를 사용하는 것이 효과적이다.
Scanner 클래스를 사용하려면 Scanner 클래스의 전체 경로명을 알려주는 import java.util.Scanner; 문이 필요하다. 개발자는 응용프로그램 전체에 Scanner 객체를 하나만 생성하고 공유하는 것이 바람직하다.

````java
import java.util.Scanner;

public class ScannerEx {
	public static void main(String[] args) {
		
		System.out.println("숫자 두 개를 입력하세요"); //Scanner 클래스는 사용자가 입력하는 키 값을 공백문자(' ', '\t', '\n')을 기준으로 분리하는 토큰 단위로 읽는다.
		Scanner scanner = new Scanner(System.in);
		
		int num1 = scanner.nextInt();
		int num2 = scanner.nextInt();
		
		System.out.println(num1+num2);

		scanner.close(); //scanner 객체 닫기
	}
}

````

### 연산
* 산술 연산자

````java
import java.util.Scanner;

public class ArithmeticOperator {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.print("정수를 입력하세요: ");
		int time = scanner.nextInt();
		int second = time % 60;
		int minute = (time/60) % 60;
		int hour = (time/60)/60;
		
		System.out.print(time + "초는 ");
		System.out.print(hour+"시간, ");
		System.out.print(minute+"분, ");
		System.out.println(second+"초입니다.");
		
		scanner.close();
	}
}
````

* 대입 연산자와 증감 연산자

````java
public class AssignmentIncDecOperator {
	public static void main(String[] args) {
		int a=3, b=3, c=3;
		//대입 연산자
		a += 3;
		b *= 3;
		c %= 2;
		System.out.println("a= "+a+", b="+b+", c="+c);
		
		int d=3;
		//증감 연산자
		a = d++;
		System.out.println("a="+a+", d="+d); //a=3, d=4
		a = ++d;
		System.out.println("a="+a+", d="+d); //a=5, d=5
		a = d--;
		System.out.println("a="+a+", d="+d); //a=5, d=4
		a = --d;
		System.out.println("a="+a+", d="+d); //a=3, d=3
	}
}
````

* 비교 연산자와 논리 연산자

````java
public class LogicalOperator {
	public static void main(String[] args) {
    // 비교 연산
		System.out.println('a'>'b');
		System.out.println(3 >= 2);
		System.out.println(-1 < 0);
		System.out.println(3.45 <= 2);
		System.out.println(3 == 2);
		System.out.println(3 != 2);
		System.out.println(!(3 != 2));
		
    //비교 연산과 논리 연산
		System.out.println((3>2) && (3>4));
		System.out.println((3!=2)||(-1>0));
		System.out.println((3!=2)^(-1>0)); //a와 b의 XOR 연산. a와 b가 서로 다를 때 true
	}
}
````

* 조건 연산자

````java
public class TernaryOperator {
	public static void main(String[] args) {
		int a=3, b=5;
		System.out.println("두 수의 차는 "+ ((a>b)?(a-b):(b-a)));		
````

* 비트 연산자

````java
public class BitOperator {

	public static void main(String[] args) {

		short a = (short)0x55ff;
		short b = (short)0x00ff;
		
		//비트 논리 연산
		System.out.println("[비트 연산 결과]");
		System.out.printf("%04x\n", (short)(a&b)); //비트 AND: 두 비트 모두 1이면 1. 그렇지 않으면 0
		System.out.printf("%04x\n", (short)(a|b)); //비트 OR: 두 비트 모두 0이면 0. 그렇지 않으면 1
		System.out.printf("%04x\n", (short)(a^b)); //비트 XOR: 두 비트가 다르면 1, 같으면 0
 		System.out.printf("%04x\n", (short)(~a)); //비트 NOT: 1을 0으로, 0을 1로 변환

 		byte c=20; //0x14
 		byte d=-8; //0xf8
 		
		System.out.println("[시프트 연산 결과]");
		System.out.println(c<<2); //c를 2비트 왼쪽 시프트. 최하위 비트에 항상 0 삽입 ->80
		System.out.println(c>>2); //c를 2비트 오른쪽 시프트. c가 양수이므로 최상위 비트에 0 삽입. 나누기 4 효과 ->5
		System.out.println(d>>2); //d를 2비트 오른쪽 시프트. d가 음수이므로 최상위 비트에 1 삽입. 나누기 4 효과 ->-2
		System.out.printf("%x\n", (d>>>2)); // d를 2비트 오른쪽 시프트. 최상위 비트에 항상 0 삽입. 나누기 효과 없음
		
		int x=2, y=10, z=0, opr=4;
		z=x++*2+--y+x*(y%2);
		System.out.println(z); //13
		System.out.println(x); //3
		System.out.println(y); //9
		System.out.println(opr++); //4
	}
}
````











* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

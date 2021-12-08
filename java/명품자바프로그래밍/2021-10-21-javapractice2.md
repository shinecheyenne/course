---
title: JAVA 기본 프로그래밍 실습문제
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
description: JAVA 프로그래밍 실습문제
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-10-21'
---

### 가위바위보 게임

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
    System.out.print("철수>>");
		String x = scanner.next();
		System.out.print("영희>>");
		String y = scanner.next();

		if(x.equals(y)) {	
			System.out.println("비겼습니다.");
		}
		else{
			if(x.equals("가위")) {
				if(y.equals("보"))
					System.out.println("철수가 이겼습니다.");
				else
					System.out.println("영희가 이겼습니다.");		
			}
			else if(x.equals("보")) {
				if(y.equals("바위"))
					System.out.println("철수가 이겼습니다.");
				else
					System.out.println("영희가 이겼습니다.");			
			}
			else if(x.equals("바위")) {
				if(y.equals("가위"))
					System.out.println("철수가 이겼습니다.");
				else
					System.out.println("영희가 이겼습니다.");			
			}
		}
    scanner.close();				
}
````


### 실습문제 1

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
    System.out.print("원화를 입력하세요(단위 원)>>");
		int won = scanner.nextInt();
		float dollar = won/1100;
		System.out.println(won+"원은 $"+String.format("%.1f", dollar)+"입니다.");

    scanner.close();				
}
````

### 실습문제 2

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("2자리수 정수 입력(10~99)");
		int num = scanner.nextInt();
		if( num%10 == num/10 ) {
			System.out.println("Yes! 10의 자리와 1의 자리가 같습니다.");
		} System.out.println("Yes! 10의 자리와 1의 자리가 다릅니다.");

    scanner.close();				
}
````


### 실습문제 3

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("금액을 입력하시오>>");
		int amount = scanner.nextInt();
		System.out.println("오만원권 "+ amount/50000 +"매"+"\n"+
							"만원권 "+ amount%50000/10000 +"매"+"\n"+
							"천원권 "+ amount%10000/1000 +"매"+"\n"+
							"백원권 "+ amount%1000/100 +"매"+"\n"+
							"오십원권 "+ amount%100/50 +"매"+"\n"+
							"십원권 "+ amount%50/10 +"매"+"\n"+
							"일원권 "+ amount%10 +"매"+"\n");

    scanner.close();				
}
````

### 실습문제 4

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("정수 3개 입력>>");
		int first = scanner.nextInt();
		int second = scanner.nextInt();
		int third = scanner.nextInt();
		
		//합계와 평균 구하기
		int sum = first+second+third;
		double average = (first+second+third)/3;
		System.out.println("합계는 "+sum+"입니다.");
		System.out.println("평균은 "+average+"입니다. ");
		
		//평균거리값으로 중간값 구하기
		double median1, median2;
		median1 = Math.min(Math.abs(first-average), Math.abs(second-average));
		median2 = Math.min(median1, Math.abs(third-average));

		
		if((first<average&&second<average)||(first<average&&third<average)||(third<average&&second<average)) {
		System.out.println("중간값은 "+(-median2+average)+"입니다. ");}
		else {
		System.out.println("중간값은 "+(median2+average)+"입니다. ");}

    scanner.close();				
}
````


````java
//교수님의 temp 변수를 이용한 중간값 구하기

import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		int max, min, mid;
		int temp;
		
		max = scanner.nextInt();
		mid = scanner.nextInt();		
		min = scanner.nextInt();
		
		if(max<mid) {
			temp=max;
			max=mid;
			mid=temp;
		}
		if(max<mid) {
			temp=max;
			max=min;
			min=temp;
		}
		if(mid<min) {
			temp=mid;
			mid=min;
			min=temp;
		}
		System.out.println(max+" "+mid+" "+min);

    scanner.close();				
}
````


### 실습문제 5

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("정수 3개를 입력하시오>>");
		int a = scanner.nextInt();
		int b = scanner.nextInt();		
		int c = scanner.nextInt();		
		
		if(a+b>c&&b+c>a&&a+c>b) {
			System.out.println("삼각형이 됩니다.");
		}

    scanner.close();				
}
````

### 실습문제 6

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("1~99 사이의 정수를 입력하시오>>");
		int num = scanner.nextInt();
		int tens = num/10;
		int rest = num%10;
		
		if(tens==3||tens==6||tens==9) {
			if(rest==3||rest==6||rest==9) {
				System.out.println("박수짝짝");
			}
			else {
				System.out.println("박수짝");
			}
		}
		else if(rest==3||rest==6||rest==9){
			System.out.println("박수짝");
		}

    scanner.close();				
}
````

### 실습문제 7

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("점 (x,y)의 좌표를 입력하시오>>");
		int x= scanner.nextInt();
		int y= scanner.nextInt();		
		if((x>=100 && x<=200) && (y>=100 && y<=200)){
			System.out.println("("+x+","+y+")는 사각형 안에 있습니다.");
		}

    scanner.close();				
}
````

### 실습문제 8

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("두 점 (x1, y1), (x2, y2)의 좌표를 차례로 입력하시오>>");
		int x1 = scanner.nextInt();
		int y1 = scanner.nextInt();		
		int x2 = scanner.nextInt();		
		int y2 = scanner.nextInt();	
		
		if((x1>=100&&x1<=200)||(x2>=100&&x2<=200)||(y1>=100&&y1<=200)||(y2>=100&&y2<=200)){
			System.out.println("충돌!!!");
		}

    scanner.close();				
}
````

### 실습문제 9

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.println("원의 중심(x, y)과 반지름 입력>>");
		int centerx = scanner.nextInt();
		int centery = scanner.nextInt();
		double radius = scanner.nextDouble();
		//final double PI = 3.14;
		
		System.out.print("점 입력>>");
		double x = scanner.nextFloat();
		double y = scanner.nextFloat();	
	
		double distance;
		distance = Math.sqrt(Math.pow((x-centerx),2)+Math.pow((y-centery),2));
		
		if(distance<=radius) {
			System.out.println("원 안에 있다.");
		}

    scanner.close();				
}
````

### 실습문제 10

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.println("첫번째 원의 중심과 반지름 입력>>");
		int x1 = scanner.nextInt();
		int y1 = scanner.nextInt();
		int radius1 = scanner.nextInt();
		System.out.println("두번째 원의 중심과 반지름 입력>>");
		int x2 = scanner.nextInt();
		int y2 = scanner.nextInt();
		int radius2 = scanner.nextInt();	
		
		double distance;
		distance = Math.sqrt(Math.pow(Math.abs((x1-x2)),2)+Math.pow(Math.abs((y1-y2)),2));
		
		if(distance<=(radius1+radius2)) {
			System.out.println("두 원은 서로 겹친다.");
		}

    scanner.close();				
}
````

### 실습문제 11-1

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.println("달을 입력하세요(1~12)>>");
		int month = scanner.nextInt();
		
		if(month==3||month==4||month==5){
			System.out.println("봄");
		}
		else if(month==6||month==7||month==8){
			System.out.println("여름");
		}
		else if(month==9||month==10||month==11){
			System.out.println("가을");
		}
		else if(month==12||month==1||month==2){
			System.out.println("겨울");
		}
		else {
			System.out.println("잘못입력");
		}

    scanner.close();				
}
````

### 실습문제 11-2

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.println("달을 입력하세요(1~12)>>");
		int month = scanner.nextInt();
		
		switch(month) {
		case 3:		case 4:		case 5:  
			System.out.println("봄");
			break;
		case 6:		case 7:		case 8:  
			System.out.println("여름");
			break;
		case 9:		case 10:		case 11:  
			System.out.println("가을");
			break;
		case 12:		case 1:		case 2:  
			System.out.println("겨울");
			break;      
		
		default:
			System.out.println("잘못입력");
		}

    scanner.close();				
}
````

### 실습문제 12-1

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("연산>>");
		float x = scanner.nextFloat();
		String oper = scanner.next();
		float y = scanner.nextFloat();
		char oper1 = oper.charAt(0);
		float result=0;

		if(oper1=='/') {
			if(y==0)
				System.out.println("0으로 나눌 수 없습니다.");
			else {
				result = x/y;
				System.out.println(Float.toString(x)+oper1+Float.toString(y)+"의 계산 결과는 "+result);
			}
		}
		else {
			if(oper1=='+') {
				result = x+y;
			}
			else if(oper1=='-') {
				result = x-y;
			}
			else if(oper1=='*') {
				result = x*y;
			}
			System.out.println(Float.toString(x)+oper1+Float.toString(y)+"의 계산 결과는 "+result);	
		}

    scanner.close();				
}
````

### 실습문제 12-2

````java
import java.util.Scanner;
public class Practice_1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
    
		System.out.print("연산>>");
		float x = scanner.nextFloat();
		String oper = scanner.next();
		float y = scanner.nextFloat();
		char oper1 = oper.charAt(0);
		float result=0;

		switch(oper1) {
			case '+':
				result = x+y;
				break;
			case '-':
				result = x-y;
				break;
			case '*':
				result = x*y;
				break;
			case '/':
				if(y==0) {
					System.out.println("0으로 나눌 수 없습니다.");
				}
				else {
					result = x/y;
				}
				break;

		}
		if(oper.equals('/')||y!=0)
					System.out.println(Float.toString(x)+oper1+Float.toString(y)+"의 계산 결과는 "+result);

    scanner.close();				
}
````

* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

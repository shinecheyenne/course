---
title: JAVA 클래스와 객체
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
description: JAVA 클래스와 객체
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-10-28'
---

## 클래스와 객체생성


````java
//클래스 선언: '접근 지정자' '클래스 선언' '클래스 이름'
public class Circle { 

  //필드(변수)
	int radius;
	String name;

  //생성자 메소드
	public Circle() {
    radius=1; name="";
  }
  
  //매개변수가 있는 생성자 (오버로딩)
  public Circle(int r, String n) {
      radius=r; name=n; //매개 변수로 필드 초기화
    }
	
  //메소드
	public double getArea() {
		return 3.14*radius*radius;
	}

	public static void main(String[] args) {
    //레퍼런스 변수 pizza 선언
		Circle pizza;
    //객체 생성
		pizza = new Circle();
		pizza.name = "자바피자";
		double area = pizza.getArea();
		System.out.println(pizza.name+"의 면적은 "+area);

		Circle donut = new Circle(2, "자바도넛");
		area = donut.getArea();
		System.out.println(donut.name+"의 면적은 "+area);
	}
}
````

* Rectangle 클래스 만들기 연습

````java
import java.util.Scanner;

class Rectang {
	int width;
	int height;
	
	public int getArea() {
		return width*height;
	}
}

public class Rectangle{
	public static void main(String[] args) {
		Rectang rect = new Rectang();
		Scanner scanner= new Scanner(System.in);
		System.out.print(">> ");
		rect.width = scanner.nextInt();
		rect.height = scanner.nextInt();
		System.out.println("사각형의 면적은 "+rect.getArea());
		scanner.close();

	}
}
````


## 생성자(constructor)

### 생성자의 특징

- 생성자의 이름은 클래스의 이름과 동일하여야 하며, 객체가 생성될 때 객체의 초기화를 위해 자동으로 호출되는 특별한 메소드이다.
- 매개변수의 개수와 타입만 다르다면 생성자는 여러 개 작성(오버로딩)할 수 있다.
- new를 통해 객체를 생성할 때 객체당 한 번만 호출된다.
- 생성자에 리턴 타입을 지정할 수 없다. (return문을 사용할 수 없다는 뜻은 아니다.)
- 생성자는 객체가 생성될 때 반드시 호출된다. (생성자를 작성하지 않으면 컴파일러가 자동으로 기본 생성자 삽입)

### 기본 생성자(default constructor)

````java
class Circle{
public Circle(){}
}
````

- 매개변수와 실행 코드가 없어 아무 일도 하지 않고 단순 리턴하는 생성자이다.
- 생성자가 없는 클래스는 있을 수 없다. 생성자를 작성하지 않으면 컴파일러가 자동으로 기본 생성자를 삽입한다.

### this 레퍼런스
객체 자신을 가리키는 레퍼런스이다.

- 객체의 멤버 변수와 메소드 변수의 이름이 같은 경우

````java
public class Circle{
int radius;
public Circle(int radius){ this.radius=radius; } //this.radius: 멤버 radius / radius: 매개변수 radius
public int getRadius(){ return radius; } 
}
````

- 메소드가 객체 자신의 레퍼런스를 반환할 때

````java
public Circle getMe(){ return this; } //getMe 메소는 객체 자신의 레퍼런스 리턴
````

### this()로 다른 생성자 호출

- 다른 메소드 호출 시 객체 자신의 레퍼런스를 전달할 때
this()는 클래스 내에서 생성자가 다른 생성자를 호출할 때 사용하는 자바 코드이다.

- this()는 반드시 생성자 코드에서만 호출할 수 있다.
- this()는 반드시 같은 클래스 내 다른 생성자를 호출할 때 사용된다.
- this()는 반드시 생성자의 첫 번째 문장이 되어야 한다.

````java
public class Book{
 String title;
 String author;

 void show() { System.out.println(title+" "+author); }

 public Book(){
  this("", "");
  System.out.println("생성자 호출됨");
 }

 public Book(String title){
  this(title, "작자미상");
 }

 public Book(String title, String author){
  this.title = title;
  this.author = author;
 }

 public static void main(String [] arg) {
  Book littlePrince = new Book("어린왕자", "생텍쥐페리");
  Book loveStory = new Book("춘향전");
  Book emptyBook = new Book();
  loveStory.show();
 }
}

//실행 결과
//생성자 호출됨
//춘향전 작자미상
````

## static 멤버

### non-static 멤버와 static 멤버

static 멤버(클래스 멤버)는 객체를 생성하지 않고도 사용할 수 있는 멤버이다. 클래스당 하나만 생성되는 멤버로서 동일한 클래스의 모든 객체들이 공유한다. static 멤버는 main() 메소드가 실행되기 전에 이미 생성되므로 static 멤버가 포함된 객체를 생성하기 전에도 사용할 수 있다. 
반면 non-static 멤버(인스턴스 멤버)는 객체가 생길 때 객체마다 생기며, 다른 객체들과 공유하지 않는다. 

### static 멤버의 활용

- 객체.static 멤버
- 클래스명.static 멤버 : static 멤버는 클래스당 하나만 있기 때문에 클래스 이름으로 바로 접근 가능하다.
- 모든 클래스에서 공유하는 전역 변수와 전역 함수를 만들 때 활용. static 멤버를 가진 대표적인 클래스로 java.lang.Math 클래스가 있다. 

````java
Math m = new Math(); //오류. 생성자 Math()는 private으로 선언되어 있어 객체 생성 불가
int n = m.abs(-5);

int n = Math.abs(-5)//클래스 이름 Math로 static 멤버를 직접 호출
````

- 공유 멤버를 만들 때 활용

### static 메소드의 제약조건
- static 메소드는 static 멤버만 접근할 수 있다.
- static 메소드는 객체 없이도 존재하므로 this를 사용할 수 없다.

## final

- final 클래스: 클래스는 상속되지 않는다.
- final 메소드: 메소드를 오버라이딩 할 수 없다.
- final 필드: 상수로서 초기화 이후 값을 수정할 수 없다.
   
   
## 예제: MonthSchedule

````java
import java.util.Scanner;

class Day{
	private String work;
	public void set(String work) {this.work=work;}
	public String get() { return work;}
	public void show() {
		if(work==null) System.out.println("없습니다.");
		else System.out.println(work+"입니다.");
	}
}

public class MonthSchedule {
	//field
	int days;
	private Day [] d;
	Scanner scanner = new Scanner(System.in);
	
	//constructor
	public MonthSchedule() {
	}
	public MonthSchedule(int days) {
		this.days = days;
		this.d = new Day[days];
		for (int i=0;i<days;i++) {
			d[i]=new Day();
		}
	}
	//method
	
	void input() {
		System.out.println("날짜(1~30)?");
		int day = scanner.nextInt();
		System.out.println("할일(빈칸없이입력)?");
		String work = scanner.next();
		d[day-1].set(work);
	}
	void view() {
		System.out.println("날짜(1~30)?");
		int day = scanner.nextInt();
		d[day-1].show();
	}
	void finish() {
		scanner.close();
		System.out.println("프로그램을 종료합니다. ");
		System.exit(0);;
	}
	
	public void run() {
		
		System.out.println("이번달 스케쥴 관리 프로그램 ");
		
		while (true) {
			System.out.println("할일(입력: 1, 보기: 2, 끝내기: 3)>>");
			int option = scanner.nextInt();

			switch(option) {
			case 1: input(); break;
			case 2: view(); break;
			case 3: finish();
			}
		}
	}
	public static void main(String[] args) {
		MonthSchedule april = new MonthSchedule(30);
		april.run();
	}
}
````

## 예제: Booking System

````java
import java.util.Scanner;

class SeatArr{
	private String [] names = new String[10];	
	
	////생성자 
	public SeatArr(){
		for (int i=0;i<10;i++) {
			this.names[i]="---";
		}
	}
	////메소드
	public void setSeat(String name, int no) {
		for(int i=0;i<10;i++) {
			this.names[no-1]=name;
		}
	}
	public String getNames() {
		String result="";
		for(int i=0;i<10;i++) {
			result += this.names[i];
		}
		return result;
	}
	public String [] getSeat() {
		return this.names;
	}
}

public class Reservation2 {
	int type;
	String typeS [] = {"S","A","B"};	
	Scanner scanner = new Scanner(System.in);
	private SeatArr s [];
	
	////생성자 
	public Reservation2() {
		this.s = new SeatArr[3];
		for (int i=0;i<3;i++) {
			s[i]=new SeatArr();
		}
	}
	
	public void booking() {
		System.out.println("좌석구분 S(1), A(2), B(3)>>");
		int type = scanner.nextInt();
		System.out.print(typeS[type-1]+"> "+s[type-1].getNames());
		System.out.println("\n이름>>");
		String name = scanner.next();
		System.out.println("번호>>");
		int no = scanner.nextInt();
		s[type-1].setSeat(name, no);
	}
	
	public void view() {
		for(int i=0;i<3;i++) {
			System.out.print("\n"+typeS[i]+"> "+s[i].getNames());
		}
		System.out.println("\n<<<조회를 완료하였습니다.>>>");
	}
	
	public void cancellation() {
		System.out.println("좌석구분 S(1), A(2), B(3)>>");
		int type = scanner.nextInt();
		System.out.print(typeS[type-1]+"> "+s[type-1].getNames());
		System.out.println("\n이름>>");
		String name = scanner.next();
		s[type-1].getSeat()[java.util.Arrays.asList(s[type-1].getSeat()).indexOf(name)]= "---";
	}
	
	public void end(){
		System.exit(0);
	}
	
	void run() {
		System.out.println("명품콘서트홀 예약 시스템입니다.");
		
		while(true) {			
			System.out.println("예약:1, 조회:2, 취소:3, 끝내기:4>>");
			int option= scanner.nextInt();
			
			switch(option) {
			case 1: booking(); break;
			case 2: view(); break;
			case 3: cancellation(); break;
			case 4: end();
			}
		}
	}	
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Reservation2 r = new Reservation2();
		r.run();
	}
}
````


* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

---
title: JAVA 상속
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
description: JAVA 상속
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-11-09'
---

### 상속과 생성자

- 슈퍼 클래스의 기본 생성자가 자동 선택 
명시적 지시가 없으면, 서브 클래스의 생성자가 기본 생성자이든 매개변수를 가진 것이든, 슈퍼 클래스에 만들어진 기본 생성자가 선택된다.

- super()를 이용하여 명시적으로 슈퍼 클래스의 생성자 선택
super()는 반드시 생성자의 첫 라인에 사용한다.


* 예제

````java
class Point{
	private int x, y;
	public Point() { //super()를 지정하지 않으면 기본생성자가 호출됨
		this.x = this.y = 0;
	}
	public Point(int x, int y) {
		this.x = x;
		this.y = y;
	}
	public void showPoint() {
		System.out.println("("+x+","+y+")");
	}
}

class ColorPoint extends Point{ //Point를 상속받은 ColorPoint 선언
	private String color;
	public ColorPoint(int x, int y, String color) {
		super(x,y); //Point의 생성자 Point(x,y)호출
		this.color = color;
	}
	public void showColorPoint() {
		System.out.print(color);
		showPoint(); //Point 클래스의 showPoint() 호출
	}
}

public class SuperEx {
	public static void main(String[] args) {
		ColorPoint cp = new ColorPoint(5,6,"blue");
		cp.showColorPoint();
	}
}
//blue(5,6)

````

### 업캐스팅과 다운캐스팅::타입 변환

- 업캐스팅

서브 클래스의 객체에 대한 레퍼런스를 슈퍼 클래스 타입으로 변환하는 것을 업캐스팅(upcasting)이라고 한다. 업캐스팅은 슈퍼 클래스의 레퍼런스로 서브 클래스의 객체를 가리키게 한다.

````java

Person p;
Student s = new Student()
p=s;

````

위 코드에서 슈퍼 클래스 타입의 레퍼런스 p가 서브클래스 객체 s를 가리키도록 치환되는 것이 업캐스팅이다. 레퍼런스 p로는 Person 클래스의 멤버만 접근할 수 있다.

- 다운캐스팅

````java

Person p = new Student(); //업캐스팅
Student s = (Student)p; //다운캐스팅

````

다운캐스팅은 업캐스팅과 달리 명시적으로 타입 변환을 지정해야 한다.

- 예제

````java

class Person{
	void info() {
		System.out.println("사람입니다.");
	}
}

class Child extends Person{
	int age = 3;
	void info() {
		System.out.println("아이입니다.");
	}
}

class Adult extends Person{
	void info() {
		System.out.println("어른입니다.");
	}
}

class Whoisit{
	public void iam(Person member) {
		member.info();
	}
}


public class UpandDown {
	public static void main(String[] args) {
		Whoisit w = new Whoisit();
		
		w.iam(new Child()); //아이입니다.
		w.iam(new Adult()); //어른입니다.

		Person p = new Child();//업캐스팅
		//p.age = 6; //컴파일 오류. age는 Person의 멤버가 아님.
		Child c = (Child)p; //다운캐스팅
		System.out.println(c.age); //3 다운캐스팅함으로써 Child클래스 내 필드에 접근 가능
		c.age = 5;
		System.out.println(c.age); //5
    
    Person [] parr = {new Child(), new Adult()};
		for(Person a:parr) {
			a.info(); //아이입니다. \n 어른입니다.
		} 
		
	}
}

````

* instanceof는 객체에 대한 레퍼런스만 사용한다. instanceof 연산자의 결과 값은 boolean 값으로, 레퍼런스가 가리키는 객체가 해당 클래스 타입의 객체이면 true, 아니면 false를 반환한다.

### 오버라이딩

- 메소드 오버라이딩은 동적 바인딩을 유발시키며, 상속을 통해 '하나의 인터페이스에 서로 다른 내용 구현'이라는 객체 지향의 다형성을 실현하는 도구이다.
- 동적 바인딩은 실행할 메소드를 컴파일 시 결정하지 않고 실행 시에 결정하는 것을 말한다.
- 메소드를 오버라이딩할 때 슈퍼 클래스의 메소드와 동일한 원형으로 작성한다.
- 슈퍼 클래스 메소드의 접근 지정자보다 접근의 범위를 좁혀 오버라이딩 할 수 없다.
- static이나 private 또는 final로 선언된 메소드는 서브 클래스에서 오버라이딩할 수 없다.
- 예시

````java

class SuperClass{
	private int x; 
	private int y;
	
	public SuperClass() {
	}
	
	public SuperClass(int x, int y) {
		this.x = x; this.y = y;
	}
	
	public void sinfo() {
		System.out.print(x+"+"+y);
	}
}

class SubClass extends SuperClass{
	private int r;
	
	public SubClass(int x, int y, int r) {
		super(x,y);
		this.r = r;
	}
	
	public void info() {
		super.sinfo(); //static binding
		System.out.println("="+r);
	}
	
	@Override
	public void sinfo() {
		System.out.println("overriding");
	}
}

public class methodOverriding {
	public static void tinfo(SuperClass s) {
		s.sinfo();
	}
	
	public static void main(String[] args) {
		SubClass s = new SubClass(1,2,3);
		s.info(); //1+2=3

		SuperClass ss = new SubClass(1,2,3);
		ss.sinfo(); //overriding -> Dynamic binding
		
		tinfo(new SubClass(1,2,3)); //overriding
	}
}

````

- Linked List 를 이용한 오버라이딩 예시

````java

class Shape{
	public Shape next;
	public Shape() { next=null;}
	
	public void draw() {
		System.out.println("Shape");
	}
}

class Line extends Shape{
	public void draw() {
		System.out.println("Line");
	}
}

class Rect extends Shape{
	public void draw() {
		System.out.println("Rect");
	}
}

class Circle extends Shape{
	public void draw() {
		System.out.println("Circle");
	}
}

public class UsingOverride {
	public static void main(String[] args) {
		Shape start, last, obj;
		start = new Line();
		last = start;
		obj = new Rect();
		last.next = obj;
		last = obj;
		obj = new Line();
		last.next = obj;
		last = obj;
		obj = new Circle();
		last.next = obj;
		
    Shape p = start;
		while(p !=null) {
			p.draw();
			p = p.next;
		}
	}
}

````

### 추상 클래스

- 추상 클래스는 객체를 생성할 수 없다.
- 추상 클래스는 추상 메소드를 통해 서브 클래스가 구현할 메소드를 명료하게 알려주는 인터페이스의 역할을 한다.
- 설계와 구현 분리

### 인터페이스

- class implements interface
- 인터페이스는 객체의 기능을 모두 공개한 표준화 문서와 같은 것으로, 클래스들이 기능을 서로 다르게 구현할 수 있도록 하는 클래스의 규격선언이며, 클래스의 다형성을 실현하는 도구이다.
- 구성: 상수, 추상메소드(public abstract), default메소드(public), private메소드, static메소드(public, private). 필드(멤버 변수)를 만들 수 없으며, protected 접근 지정 선언이 불가하다.
- 인터페이스는 객체를 생성할 수 없다.
- 인터페이스 타입의 레퍼런스 변수는 선언 가능하다.
- 인터페이스끼리 상속된다. 다중 상속을 허용한다.
- 인터페이스를 상속받아 작성한 클래스는 인터페이스의 모든 추상 메소드를 구현하여야 한다. 이때 다중 인터페이스 구현이 가능하다.


* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

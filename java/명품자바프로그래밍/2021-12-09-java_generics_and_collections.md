---
title: JAVA 제네릭과 컬렉션
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
description: JAVA 제네릭과 컬렉션
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-12-09'
---


### 컬렉션(Collections)의 개념

객체들의 컨테이너. 배열과 달리 가변 크기로서 객체를 쉽게 삽입, 삭제, 검색할 수 있다.

<img src="images/collections_interface_class.png"  width="600" height="400"/>

- 컬렉션은 제네릭(generics) 기법으로 만들어져 있다. 컬렉션 클래스의 이름에는 타입 매개변수(\<E\>, \<K\>, \<V\> 등)가 포함되며, 타입 매개변수 대신 Integer 등의 구체적인 타입을 지정하면 지정된 타입만 다룰 수 있는 구체화된 클래스가 된다.
- 컬렉션은 여러 타입의 값을 다룰 수 있도록 한 자료 구조이지만, 사용할 때는 지정된 특정 타입의 값만 저장 가능하다. 
- 컬렉션의 요소는 객체들만 가능하다.

````java

Vector<int> v = new Vector<int>(); //컴파일 오류
Vector<Integer> v = new Vector<Integer>();

````

#### 제네릭 (Generics)
  
특정 타입만 다루지 않고, 여러 종류의 타입으로 변신할 수 있도록 클래스나 메소드를 타입 매개변수(generic type)를 이용하여 일반화하는 기법으로 클래스 코드를 찍어내듯이 생산할 수 있도록 일반화시키는 도구이다.
\<E\>: Element, \<T\>: Type, \<V\>: Value, \<K\>: Key 

  

### 제네릭 컬렉션 활용
  
#### Vector\<E\>

````java
  
import java.util.Vector;

class Point{
	private int x, y;
	public Point(int x, int y) {
		this.x=x; this.y=y;
	}
	public String toString() {
		return String.format("(%d, %d)", x,y);
	}
}

public class practice7_1 {
	public static void main(String[] args) {
		
		//1) Vector<Integer> 컬렉션 활용
		Vector<Integer> v = new Vector<Integer>();
		
		v.add(4);v.add(-1);v.add(1, 0);

		System.out.println("벡터 내의 요소 객체 수: "+v.size());
		System.out.println("벡터의 현재 용량: "+v.capacity());
		
		int sum =0;
		for(int i=0;i<v.size();i++) {
			System.out.print(v.get(i)+" ");
			sum += v.get(i);
		}
		System.out.println("\n벡터에 있는 정수 합: "+sum);
		
		//2) Vector<Point> 컬렉션 활용
		Vector<Point> vp= new Vector<>();
		
		vp.add(new Point(2,3));vp.add(new Point(-5,20));vp.add(new Point(30,-8));
		
		vp.remove(1);
		
		for(int i=0;i<vp.size();i++) {
			System.out.print(vp.get(i));
		}
		
		Vector<Integer> v2 = new Vector<>();
		v2.add(3); v2.add(100);
		
		//boolean addAll(Collection<? extends E>c)
		v.addAll(v2);
		for(int i=0;i<v.size();i++) {
			System.out.print(v.get(i)+" ");
		}
		
		//Vector<E> 클래스의 주요 메소드
		//boolean add(E element) / void add(int index, E element)
		//void clear() / boolean contains(Object o) / E elementAt(int index) / int indexOf(Object o) /
		// boolean isEmpty() / E remove(int index) / boolean remove(Object o) / void removeAllElements() / Object [] toArray()
	}
}

````
  
#### Array\<E\>

Vector 클래스와 거의 동일하지만, ArrayList는 스레드 간 동기화를 지원하지 않아 다수의 스레드가 동시에 ArrayList에 요소를 삽입하거나 삭제할 때 데이터가 훼손될 우려가 있다. (멀티스레드 동기화를 위한 시간 소모가 없어 Vector보다 속도가 빠르다. 단일 스레드 응용에 더 효과적)

#### 컬렉션 순차 검색을 위한 Iterator

Vector, ArrayList, LinkedList, Set과 같이 요소가 순서대로 저장된 컬렉션에서 요소를 순차 검색할 때 java.util 패키지의 Iterator\<E\> 인터페이스를 사용한다.

````java

Vector<Integer> v = new Vector<Integer>();
Iterator<Integer> it = v.iterator(); //벡터 v의 요소를 순차 검색할 Iterator 객체 리턴 (!!다음에 사용할 때 다시 설정해줘야 함)
while(it.hasNext()){
  int n = it.next();
  ...
}

//boolean hasNext() / E next() / void remove()

````

#### HashMap\<K,V \>

Vector\<E\>나 ArrayList\<E\>에 비해 요소의 삽입, 삭제, 요소 검색이 빠르다.

- 주요 메소드: void clear(), boolean contiansKey(Object key), boolean containsValue(Object value), V get(Object key), boolean isEmpty(), Set\<K\> keySet(), v put(K key, V value), V remove(Object key), int size()

````java

Set<String> keys = h.keySet();
Iterator<String> it = keys.iterator();
while(it.hasNext()){
  String key = it.next();
  String value = h.get(key);
}

````


* 예제 7-7 HashMap에 객체저장

````java

import java.util.*;

class Student{
	private int id;
	private String tel;
	public Student(int id, String tel) {this.id=id;this.tel=tel;}
	public int getId() {return id;}
	public String getTel() {return tel;}
}

public class HashMapStudentEx {
	public static void main(String[] args) {
		HashMap<String, Student> map = new HashMap<>();
		map.put("A", new Student(1, "0101"));map.put("B", new Student(1, "0202"));map.put("C", new Student(1, "0303"));
		
		Scanner scan = new Scanner(System.in);
		
		while(true) {
			System.out.print("검색할 이름?");
			String name = scan.nextLine();
			
			if(name.equals("exit")) break;
			
			Student student = map.get(name);
			if(student == null) System.out.println(name+"은 없는 사람입니다.");
			else System.out.println("id: "+student.getId()+", 전화: "+student.getTel());
		}
		scan.close();
	}
}

````

#### LinkedList\<E\>

맨 앞과 맨 뒤를 가리키는 head, tail 레퍼런스를 가지고 있어, 맨 앞이나 맨 뒤, 중간에 요소의 삽입이 가능하며 인덱스를 이요하여 요소에 접근할 수도 있다.

#### Collections 클래스

sort(), reverse(), max(), min(), binarySearch()등과 같이 컬렉션을 다루는 메소드를 지원한다. Collections 클래스의 메소드는 모두 static 타입이므로 Collections 객체를 생성할 필요는 없다.
Collections 클래스는 int, char, double등의 기본타입과 String 클래스 등 java.lang.Comparable을 상속받는 element에 대해서만 작동한다. 따라서 사용자가 클래스를 작성하는 경우 java.lang.Comparable을 상속받아야 한다.
 
 
* 예제 7-8 Collections 클래스 활용

````java

import java.util.*;

public class practice7_8 {
	static void printList(LinkedList<String> l) {
		Iterator<String> it = l.iterator();

		while(it.hasNext()) {
			String e = it.next();
			String sep;
			if(it.hasNext()) sep = " -> ";
			else sep="\n";
			System.out.print(e+sep);
		}
	}
	
	public static void main(String[] args) {
		LinkedList<String> myList = new LinkedList<>();
		
		myList.add("트랜스포머");myList.add("스타워즈");myList.add("매트릭스");myList.add(0,"터미네이터");myList.add(2,"아바타");

		Collections.sort(myList);
		printList(myList);
		Collections.reverse(myList);
		printList(myList);
		int index = Collections.binarySearch(myList, "아바타");
		System.out.println(index);
	}
}

````


### 제네릭 만들기

#### 제네릭 클래스

* 제네릭 클래스 작성

````java

public class MyClass<T>{
  T val;
  void set(T a){
    val = a;
  }
  T get(){
    return val;
  }

````

* 제네릭 클래스에 대한 레퍼런스 변수 선언/객체생성

제네릭 클래스에 구체적인 타입을 대입하여 구체적인 객체를 생성하는 과정을 구체화라 한다. 제네릭의 구체화에는 기본 타입은 사용할 수 없다.
또한, 제네릭 클래스 내에서 제네릭 타입을 가진 객체의 생성은 허용되지 않는다. 컴파일 시, 컴파일러가 구체적인 타입을 알 수 없어 호출될 생성자를 결정할 수 없고, 어떤 크기의 메모리를 할당해야 할 지 알 수 없기 때문이다. 

````java

MyClass<String> s = new MyClass<String>();

````

* 제네릭 스택 만들기

````java

class GStack<T>{
	int tos;
	Object [] stck;
	
	public GStack() {
		tos = 0;
		//제네릭 매개변수로 객체나 배열을 생성할 수 없으므로 Object 배열을 생성하여 실제 타입의 객체를 요소로 삽입한다.
		stck = new Object[10]; 
	}
	
	public void push(T item) {
		if(tos==10) 
			return;
		stck[tos]=item; //업캐스팅
		tos++;
	}
	
	public T pop() {
		if(tos==0)
			return null;
		tos--;
		return (T) stck[tos]; //타입 매개변수 타입으로 캐스팅
	}
}

public class MyStack {
	public static void main(String[] args) {
		GStack<String> stringStack = new GStack<>();
		
		stringStack.push("seoul"); stringStack.push("busan"); stringStack.push("LA");
		
		for(int i=0;i<3;i++) 
			System.out.println(stringStack.pop());
		
		GStack<Integer> intStack = new GStack<Integer>();
		
		intStack.push(1);intStack.push(3);intStack.push(5);
		
		for(int i=0;i<3;i++) 
			System.out.println(intStack.pop());
	}
}

````


#### 제네릭과 배열

- 제네릭 클래스 또는 인터페이스 타입의 배열은 선언할 수 없다. 제네릭 타입의 배열 '선언'은 허용.

````java

GStack<Integer>[] gs = new GStack<Integer>[10]; //컴파일 오류
public void myArray(T[] a){...} //정상

````

- 제네릭 메소드

````java

class GenericMethodEx{
  //타입 매개변수는 메소드의 리턴 타입 앞에 선언된다.
  static <T> void toStack(T[]a, GStack<T>gs){
    for (int i=0;i<a.length;i++){
      gs.push(a[i]);
  }
}

````

* 제네릭 메소드 예제

````java

public class GenericMethodEx {
	
	public static <T> GStack<T> reverse(GStack<T> a){
		GStack<T> s = new GStack<>();
		while(true) {
			T tmp;
			tmp = a.pop();
			if(tmp==null) break;
			else s.push(tmp);
		}
		return s;
	}

	public static void main(String[] args) {
		GStack<Double> gs = new GStack<>();
		
		for(int i=0;i<5;i++) {
			gs.push(new Double(i));
		}
		//컴파일러는 제네릭 메소드 reverse()의 타입 매개변수를 Double로 유추
		gs = reverse(gs);
		for(int i=0;i<5;i++) {
			System.out.print(gs.pop()+" ");
		}
	}
}

````

#### 제네릭의 장점

- 동적으로 타입이 결정되지 않고, 컴파일 시 타입이 결정되므로 보다 안전
- 런타임 타입 충돌 문제 방지
- 개발 시 타입 캐스팅 절차 불필요
- ClassCastException 방지



* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

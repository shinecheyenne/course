---
title: JAVA 제네릭과 컬렉션_실습문제7
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
description: JAVA 제네릭과 컬렉션_실습문제7
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-12-07'
---

### Open Challenge _단어테스트

````java

import java.util.*;

public class Word {
	private String eng;
	private String kor;
	public Word(String eng, String kor) {
		this.eng=eng;this.kor=kor;
	}
	public String getEng() { return eng;}
	public String getKor() { return kor;}
}


public class Open_Challenge {
	String name;
	Vector<Word> v;
	Scanner scan = new Scanner(System.in);

	public Open_Challenge(String name) {
		this.name=name; 
		v = new Vector<>();
		v.add(new Word("fiction", "허구"));
		v.add(new Word("fear", "두려움"));
		v.add(new Word("sentimental", "감상적인"));
		v.add(new Word("sky", "하늘"));
		v.add(new Word("here", "여기"));
		v.add(new Word("goodbye", "안녕"));
		v.add(new Word("star", "별"));
		v.add(new Word("family", "가족"));
		v.add(new Word("society", "사회"));
		v.add(new Word("magic", "마법"));
		v.add(new Word("animal", "동물"));
		v.add(new Word("gun", "총"));
		v.add(new Word("science", "과학"));
	}
	private void error(String msg) {
		System.out.println(msg);
	}
	
	private void quit() {
		System.out.println("Say goodbye to "+name+"!");
	}
	private void add() {
		System.out.println("Enter 'stop' to exit.");
		while(true) {
			System.out.println("Enter (English Korean) word>>");
			String eng = scan.next();
			if(eng.equals("stop")) break;
			String kor = scan.next();
			v.add(new Word(eng, kor));
		}
	}
	private int[] randomG_4(int size) {
		int [] rani = new int[4];
		
		for(int i=0;i<4;i++) {
			rani[i]=(int)(Math.random()*size);
			for(int j=0;j<i;j++) {
				if(rani[j]==rani[i]) i--;
			}
		}
		return rani;
	}
	
	int input=0;
	public int input(int a, int b) {
		try {
			input = scan.nextInt();
			if(input!=-1 && (input<a || input>b)) {throw new ArrayIndexOutOfBoundsException();}
		}  catch(InputMismatchException e) {
			scan.nextLine();
			error("Enter Integer>>");
			input(a,b);
		} catch(ArrayIndexOutOfBoundsException e) {
			scan.nextLine();
			error("Try again>>");
			input(a,b);
		}
		return input;
	}
	
	private void quiz() {
		System.out.println("We have "+v.size()+" word prepared for you. Press -1 to quit.");

		while(true) {
			int [] myRan = randomG_4(v.size());
			int [] idxRan = randomG_4(4);
			
			System.out.println(v.get(myRan[0]).getEng()+"?");
			System.out.printf("(1)%s (2)%s (3)%s (4)%s :>",
					v.get(myRan[idxRan[0]]).getKor(),v.get(myRan[idxRan[1]]).getKor(),
					v.get(myRan[idxRan[2]]).getKor(),v.get(myRan[idxRan[3]]).getKor());
			int answer = input(1,4);
			if(answer==-1) break;
			
			if(v.get(myRan[0]).getKor().equals(v.get(myRan[idxRan[answer-1]]).getKor()))
				System.out.println("Excellent!");
			else System.out.println("Wrong!!");
		}		
	}
	public void run() {
		System.out.println("*** Hello! This is English Word Test "+name+" ***");
		
		while(true) {
			System.out.println("Word Quiz:1, Add word:2, exit:3>>");
			switch(input(1,3)) {
				case 1: quiz(); break;
				case 2: add(); break;
				case 3: quit(); return;
			//	default: error("Try again!");
			}
		}
	}
	
	public static void main(String[] args) {
		Open_Challenge g = new Open_Challenge("My English");
		g.run();
	}
}

````

### 문제 6 _도시 정보 입출력

````java

import java.util.*;

class Location{
	private String name;
	private String longitude;
	private String latitude;
	
	public Location(String name, String longitude, String latitude) {
		this.name=name;this.longitude=longitude;this.latitude=latitude;
	}
	
	public String getName() {return name;}
	public String getLon() {return longitude;}
	public String getLat() {return latitude;}
}


public class exercise7_6 {
	Scanner scan = new Scanner(System.in);
	HashMap<String, Location> city = new HashMap<>();
	
	void input() {
		System.out.println("Enter city name, longitude and latitude.");

		for(int i=0;i<2;i++) {
			System.out.println(">>");
			String input = scan.nextLine();
			StringTokenizer st = new StringTokenizer(input, ",");
			
			String name = st.nextToken().trim();
			String longitude = st.nextToken().trim();
			String latitude = st.nextToken().trim();
			
			city.put(name, new Location(name, longitude, latitude));
		}
	}
	
	void print() {
		Set<String> keys = city.keySet();
		Iterator<String> it = keys.iterator();
		while(it.hasNext()) {
			Location c = city.get(it.next());
			System.out.println(c.getName()+" "+c.getLon()+" "+c.getLat());
		}
		System.out.println("--------------------------------");
	}
	
	
	void process() {
		while(true) {
			System.out.println("Name of the city>>");
			String cname = scan.nextLine();
			if(cname.equals("stop")) break;
			
			if(city.containsKey(cname)) System.out.println(city.get(cname).getName()+" "+city.get(cname).getLon()+" "+city.get(cname).getLat());
			else System.out.println("No such city");
		}
	}
	
	void run() {
		input();
		print();
		process();
	}
	
	public static void main(String[] args) {
		exercise7_6 g = new exercise7_6();
		g.run();
	}
}

````

### 문제 8 _포인트 관리

````java

import java.util.*;

public class exercise7_8 {

	static void print(HashMap<String, Integer>h) {
		 Set<String> keys = h.keySet();
		 Iterator<String> it = keys.iterator();
		 
		 while(it.hasNext()) {
			 String tmp=it.next();
			 System.out.print(String.format("(%s, %d) ", tmp, h.get(tmp)));
		 }
	}
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		HashMap<String, Integer> mmp = new HashMap<>();
		
		System.out.println("Mileage Management Program");
		
		while(true) {
			System.out.println("\nEnter your name and mileage>>");
			String name = scan.next(); int score = scan.nextInt();
			
			if(mmp.containsKey(name)) mmp.put(name, mmp.get(name)+score);
			else mmp.put(name, score);
			
			print(mmp);
			
			if(name.equals("stop")) break;
		}
	}
}

````

### 문제 9 _스택 구현

````java

import java.util.*;

interface IStack<T>{
	T pop();
	boolean push(T ob);
}

class MyStack<T> implements IStack<T>{
	Vector<T> v = new Vector<>();
	
	@Override
	public T pop(){
		if(v.size()!=0)
			return v.remove(v.size()-1);
		return null;
	}
	
	@Override
	public boolean push(T ob) {
		return v.add(ob);
	}
}

public class exercise7_9 {
	public static void main(String[] args) {
		IStack<Integer> stack = new MyStack<Integer>();
		
		for(int i=0;i<10;i++) stack.push(i);
		while(true) {
			Integer n = stack.pop();
			if(n==null) break;
			System.out.print(n+" ");
		}
	}
}

````

### 문제 10 _그래픽편집기

````java

import java.util.*;

public class exercise7_10 {
	Scanner scan = new Scanner(System.in);
	Vector<Shape> v = new Vector<>();
	
	void add() {
		System.out.println("Line(1), Rect(2), Circle(3)>>");
		int op = scan.nextInt();
		
		switch(op) {
			case 1: v.add(new Line()); break;
			case 2: v.add(new Rect()); break;
			case 3: v.add(new Circle()); break;
			default: break;
		}
	}
	
	Shape delete() {
		System.out.println("Enter index of what's to be deleted>>");
		int idx = scan.nextInt();
		if(idx<v.size() && idx>=0) return v.remove(idx);
		else System.out.println("No element"); return null;	
	}
	
	void view() {
		Iterator<Shape> it = v.iterator();
		while(it.hasNext()) {
			System.out.println(it.next());
		}
	}
	
	void choice(int op) {
		switch(op) {
			case 1: add(); break;
			case 2: delete(); break;
			case 3: view(); break;
		}
	}
	
	void startMenu() {
		System.out.println("Graphic editor Beauty");
		
		while(true) {
			System.out.println("insert(1), delete(2), view(3), exit(4)>>");
			int op = scan.nextInt();

			switch(op) {
				case 1: add(); continue;
				case 2: delete(); continue;
				case 3: view(); continue;
			}
			
			if(op==4) System.out.println("Say Goodbye to Beauty"); break;	
		}
	}
	
	public static void main(String[] args) {
		exercise7_10 g = new exercise7_10();
		g.startMenu();
	}
}

````

### 문제 11 _나라와수도 맞추기

````java

import java.util.*;

public class exercise7_11_2 {
	Scanner scan = new Scanner(System.in);
	HashMap<String, String> h = new HashMap<>();
	Set<String> keys = h.keySet();

	
	public exercise7_11_2() {

		h.put("Korea", "Seoul");
		h.put("China", "Beijing");
		h.put("Japan", "Tokyo");
		h.put("USA", "Washington");
		h.put("Hungary", "Budapest");
		h.put("Canada", "Ottawa");
		h.put("France", "Paris");
		h.put("Germany", "Berlin");
		h.put("Egypt", "Cairo");
	}

	
	void startMenu() {
		System.out.println("Guessing Capital");
		
		while(true) {
			System.out.println("Input:1, Quiz:2, Quit:3>>");
			int op = scan.nextInt();
			
			switch(op) {
				case 1: input(); continue;
				case 2: quiz(); continue;
			}
			if(op==3) System.out.println("Exit the game."); break;
		}
	}
	
	boolean checkCountry(String s) {
		Iterator<String> it = keys.iterator();
		
		if(h.containsKey(s)) return true;
		else return false;

	}
	
	boolean checkAnswer(String q, String a) {
		Iterator<String> it = keys.iterator();
		
		if(h.containsKey(q)) return h.get(q).equals(a);
			return false;
	}
	
	void input() {
		System.out.println("We have "+h.size()+"countries and capitals in our database.");
		
		while(true) {
			System.out.println("Enter "+(h.size()+1)+"th country and its capital>>");

			String name = scan.next();
			if(name.equals("stop")) break;
			String cap = scan.next();
			
			if(checkCountry(name)) System.out.println(name+" already exists.");
			else {
				h.put(name, cap);
			}
		}
	}
	
	void quiz() {
		Iterator<String> it = keys.iterator();
		
		while(it.hasNext()) {
			String question = it.next();
			System.out.println("Where is the capital city of "+question+"?");
			String answer= scan.next();
			if(answer.equals("stop")) break;
			if(checkAnswer(question, answer)) System.out.println("yeah! you rock!");
			else System.out.println("Wrong answer");
		}
	}
	
	public static void main(String[] args) {
		exercise7_11_2 g = new exercise7_11_2();
		g.startMenu();
	}
}

````

### 문제 13 _명령 실행

````java

import java.util.*;

public class test {
	Scanner scan = new Scanner(System.in);
	Vector<String> commands = new Vector<>();
	HashMap<String, Integer> h = new HashMap<>();
	String result;

	private void mov(String a, String b) {
		if(h.containsKey(b)) h.put(a, h.get(b));
		else h.put(a, Integer.parseInt(b));
	}
	
	private void add(String a, String b) {
		if(h.containsKey(a)) {
			if(h.containsKey(b)) h.put(a, h.get(a)+h.get(b));
			else h.put(a, h.get(a)+Integer.parseInt(b));
		}
	}
	
	private void sub(String a, String b) {
		if(h.containsKey(a)) {
			if(h.containsKey(b)) h.put(a, h.get(a)-h.get(b));
			else h.put(a, h.get(a)-Integer.parseInt(b));
		}
	}
	
	private void jn0(String a, String b) {
		while(h.containsKey(a) && h.get(a)!=0) {
			Iterator<String> cit = commands.iterator();
			
			for(int i=0;i<Integer.parseInt(b);i++) {
				cit.next();
			}
			process(cit);
		}
	}
	
	private void exec(String s) {
		String[] sArr = s.split(" ");
		
		switch(sArr[0]) {
			case "mov": mov(sArr[1], sArr[2]); break;
			case "add": add(sArr[1], sArr[2]); break;
			case "sub": sub(sArr[1], sArr[2]); break;
			case "jn0": jn0(sArr[1], sArr[2]); break;
			case "prt": prt(sArr[1], sArr[2]); break;
		}
	}
	
	private void prt(String a, String b) {
		result = a;
	}
	
	private void process(Iterator<String> cit) {
		while(cit.hasNext()) {
			exec(cit.next());
		}
	}
	
	private void result() {
		System.out.printf("[prt %s 0]\n",result);
		Set<String> keys = h.keySet();
		Iterator<String> it= keys.iterator();
		while(it.hasNext()) {
			String s = it.next();
			System.out.printf("%s:%d ",s.toUpperCase(),h.get(s));
		}	
		System.out.println("\nThe result is "+h.get(result)+", Good bye.");
	}
	
	private void run() {
		System.out.println("This is Supercom. Please enter statements and 'go' to get the result.");
		
		while(true) {
			System.out.print(">>");
			String str = scan.nextLine(); commands.add(str);
			
			if(str.equals("go")) {process(commands.iterator()); result();break;}
		}
	}
	
	public static void main(String[] args) {
		test g = new test();
		g.run();
	}
}

````

* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

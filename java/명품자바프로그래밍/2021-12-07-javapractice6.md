---
title: JAVA 패키지_실습문제6
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
description: JAVA 패키지_실습문제6
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-12-07'
---

### Open Challenge _ Alphabet Histogram

````java

import java.util.Scanner;

public class Alphabet {
	private char name;
	private int count;
	
	public Alphabet(char name) {
		this.name = name;
	}
	
	public void setCount(int count) {
		this.count = count;
	}
	
	public String toString() {
		String dash = new String();
		for(int i=0;i<count; i++) {
			dash = dash.concat("-");
		}
		return name+dash;
	}
}


public class Histogram_UI {
	private Scanner scanner = new Scanner(System.in);
	private Alphabet [] als = new Alphabet[26];
	private String abc;
	
	public Histogram_UI(){
		for(int i = 97; i<123;i++) {
			als[i-97]= new Alphabet((char)i);
		}
		
        char[] a = new char [26];
        
        for(int i= 97;i<123;i++){
            a[i-97]=(char)i;
        }
        
        this.abc = new String(a);
	}
	
	void printInput() {
		System.out.println("영문 텍스트를 입력하고 세미콜론을 입력하세요.");
	}
	
	String readString() {
		StringBuffer sb = new StringBuffer();
		
		while(true) {
			String line = scanner.nextLine();
			if(line.equals(";"))
				break;
			sb.append(line);
		}
		return sb.toString();
	}
	
	void drawHistogram() {
		System.out.println("히스토그램을 그립니다.");
		for(Alphabet al : als) {
			System.out.println(al);
		}
	}
	
	public void countString() {
		String convertedString = convertString();

		for(int j=0;j<abc.length();j++) {
			int count=0;
			Alphabet al = new Alphabet(abc.charAt(j));
			
			for (int i=0;i<convertedString.length();i++) {
				if(convertedString.charAt(i) == abc.charAt(j)) {
					count++;
				}
			}
			al.setCount(count);
			als[j]=al;
		}
	}
	
	public String convertString() {
		String pattern = "[^a-zA-Z]";
		String convertedString= readString().toLowerCase().replaceAll(pattern,"");
		
		return convertedString;
	}
	
	public static void main(String[] args) {
		Histogram_UI hiui = new Histogram_UI();
		hiui.printInput();
		hiui.countString();
		hiui.drawHistogram();
	}
}

````

### 문제 6 _10초 근접게임

````java

import java.util.Calendar;
import java.util.Scanner;

public class Member {
	private String name;
	private int first;
	private int last;
	
	public Member(String name) {
		this.name = name;
	}
	public String getName() {
		return name;
	}
	public int getFirst() {
		return first;
	}
	public int getLast() {
		return last;
	}
	public void setName(String name) {
		this.name = name;
	}
	public void setFirst(int first) {
		this.first = first;
	}
	public void setLast(int last) {
		this.last = last;
	}
	
	public String toString() {
		return name;
	}
	
	public int result() {
		if(last==0) {last = 60;}
		return last - first;
	}
	
	public Member compareTo(Object obj) {
		Member m = (Member) obj;
		if(Math.abs(m.result()-10)>Math.abs(this.result()-10)) {
			return this;
		}
		else if(Math.abs(m.result()-10)<Math.abs(this.result()-10)) {
			return m;
		}
		else return new Member("both");
	}
}


public class exercise6 {
	private Scanner scan = new Scanner(System.in);
	
	public void printCal(Member m, int op) {
		Calendar cal = Calendar.getInstance();

		int second = (int)(cal.getTimeInMillis()%60000/1000);
				
		System.out.println("Current time(second) = "+second);
		
		if(op==0) m.setFirst(second);
		else if(op==1) m.setLast(second);
	}
	
	public void printGuide() {
		System.out.println("Whose guess is closer to 10 seconds?");
	}
	public void getTime(Member m) {
		System.out.println(m+ " press <Enter> to start>>");
		scan.nextLine();
		printCal(m, 0);
		System.out.println("press <Enter> after 10 seconds>>");
		scan.nextLine();
		printCal(m, 1);
	}
	
	public void run(Member m1, Member m2) {
		getTime(m1);
		getTime(m2);
		printResult(m1, m2);
	}
	
	public void printResult(Member m1, Member m2) {
		Member winner = m1.compareTo(m2);
		System.out.println(m1+": "+m1.result()+", "+m2+":  "+m2.result()+", The winner is "+winner);
	}
	
	public static void main(String[] args) {
		exercise6 g = new exercise6();
		g.printGuide();
		g.run(new Member("Hwang"), new Member("Lee"));
	}
}

````

### 문제 8 _문자열 회전

````java

public class exercise8 {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		String s = scan.nextLine();
		
		for (int i = 0;i<s.length()+1;i++) {
			System.out.println(s.substring(i, s.length())+s.substring(0, i));
		}
		
		scan.close();
	}
}

````

### 문제 9 _가위바위보

````java

import java.util.Scanner;

public class exercise9 {
	private Scanner scan = new Scanner(System.in);
	private String [] options = {"scissors", "rock", "paper"};
	private int userOption;
	private int comOption;
	
	public void printMenu() {
		System.out.println("user[scissors(1), rock(2), paper(3), quit(4)]>>");
		userOption = scan.nextInt();
		comOption = (int)(Math.random()*options.length+1);
		if (userOption<options.length+1) {
			System.out.println(String.format("user (%s): computer (%s)", options[userOption-1], options[comOption-1]));		
		}
	}
	
	public void printResult() {
		String msg="";
		int num = (userOption-comOption+2)%3;
		
		switch(num) {
		case 2: msg="It's a draw!";break;
		case 0: msg="You win!";break;
		case 1: msg="Computer win!";break;
		}
		System.out.println(msg);
	}
	
	public void run() {
		while(true) {
			printMenu();
			if(userOption==4) break;
			printResult();
		}
	}
	
	public static void main(String[] args) {
		exercise9 g = new exercise9();
		g.run();
	}
}

````

### 문제 10 _갬블링게임

````java

import java.util.Scanner;

public class Person {
	private String name;
	
	public boolean result() {
		int num1 = (int)(Math.random()*3+1);
		int num2 = (int)(Math.random()*3+1);
		int num3 = (int)(Math.random()*3+1);
		System.out.println(num1+" "+num2+" "+num3);
		return (num1==num2)&&(num2==num3);
	}
	
	public String toString() {
		return name;
	}
	
	public void setName(String name) {
		this.name = name;
	}
}


public class exercise10 {
	Scanner scan = new Scanner(System.in);
	Person [] persons = new Person [2];
	
	public exercise10(){
		for(int i=0;i<persons.length;i++) {
			persons[i]=new Person();
		}
	}
	
	public void printPerson() {
		for(int i=0;i<persons.length;i++) {
			System.out.printf("%d player's name: ", i+1);
			persons[i].setName(scan.next());
		}
	}
	
	public boolean game(Person p) {
		System.out.print("["+p+"]:");
		scan.nextLine();

		if(p.result()) {
			System.out.println(p+" win!");
			return false;
		} else {
			System.out.println("One more try!");
			return true;
		}
	}
	
	public void run() {
		printPerson();
		scan.nextLine();
		
		boolean result = true;
		while(result) {
			for(Person p:persons) {
				if(!game(p)) {
				result = false;
				break;}
			}
		}
	}
	
	public static void main(String[] args) {
		exercise10 g = new exercise10();
		g.run();
	}
}

````


### 문제 11 _문자 수정

````java

import java.util.Scanner;

public class exercise11 {
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		System.out.print(">>");
		StringBuffer sb = new StringBuffer(scan.nextLine());
				
		while(true) {
			System.out.print("Request:: ");
			String [] request = scan.nextLine().split("!");
			
			if(request[0].equals("stop") && request.length==1) break;
			
			int index = sb.indexOf(request[0]);
			
			if(index==-1) {
				System.out.println("We could not find your request");
			} else {
				sb.replace(index, index+request[0].length(), request[1]);
				System.out.println(sb);
			}
		}
		scan.close();
	}
}

````

### 문제12 _갬블링2

````java

import exercise10.Person;
import java.util.Scanner;

public class exercise12 {
	private Scanner scan = new Scanner(System.in);
	private Person [] persons;
	
	public exercise12(){
		this.persons = new Person[getSize()];
		
		for(int i=0;i<persons.length;i++) {
			persons[i]=new Person();
		}
	}
	
	public int getSize(){
		System.out.println("How many players in?");
		int size = scan.nextInt();
		return size;
	}
	
	public void printPerson() {
		for(int i=0;i<persons.length;i++) {
			System.out.printf("Player %d's name: ", i+1);
			persons[i].setName(scan.next());
		}
	}
	
	public boolean gamePrint(Person p) {
		System.out.print("["+p+"]:");
		scan.nextLine();

		if(p.result()) {
			System.out.println(p+" win!");
			return false;
		} else {
			System.out.println("One more try!");
			return true;
		}
	}
	
	public void run() {
		printPerson();
		scan.nextLine();
		
		boolean result = true;
		while(result) {
			for(Person p:persons) {
				if(!gamePrint(p)) {
				result = false;
				break;}
			}
		}
	}
	
	public static void main(String[] args) {
		exercise12 g = new exercise12();
		g.run();
	}
}

````


* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

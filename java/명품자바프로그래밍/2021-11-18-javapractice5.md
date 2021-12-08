---
title: JAVA 상속_실습문제5
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
description: JAVA 상속_실습문제5
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-11-18'
---

#### Open Challenge _ Fishing Game

````java

import java.util.Scanner;

//abstract class
abstract class GameObject {
	protected int distance;
	protected int x, y;
	public GameObject(int startX, int startY, int distance) {
		this.x = startX;
		this.y = startY;
		this.distance = distance;
	}
	public int getX() { return x; }
	public int getY() { return y; }
	public boolean collide(GameObject p) {
		if(this.x == p.getX() && this.y == p.getY())
			return true;
		else
			return false;
	}
	protected abstract void move();
	protected abstract char getShape();
}

//inherited to bear
class Bear extends GameObject{
	Scanner scanner = new Scanner(System.in);
	Bear(int startX, int startY, int distance){
		super(startX, startY, distance);
	}
	protected void move() {
		System.out.println("left(a), down(s), up(d), right(f) >>");
		String dir = scanner.next();
		
		switch(dir) {
		case "a": y -= 1; break;
		case "s": x += 1; break;
		case "d": x -= 1; break;
		case "f": y += 1; break;
		}
	}
	protected char getShape() {
		return "B".charAt(0);
	}
}

//inherited to fish
class Fish extends GameObject{
	Fish(int startX, int startY, int distance){
		super(startX, startY, distance);
	}
	protected void move() {
		int ran = (int)(Math.random()*4);
		switch(ran) {
		case 0: y -= 1; break;
		case 1: x += 1; break;
		case 2: x -= 1; break;
		case 3: y += 1; break;
		}
	}
	protected char getShape() {
		return "@".charAt(0);
	}
}

//game board
class Board{
	protected String [][] board = new String[10][20];
	
	public Board() {
		for (int i=0;i<10;i++) {
			for(int j=0;j<20;j++) {
				this.board[i][j] = "-";
			}
		}
	}
	
	public void showBoard() {
		for (int i=0;i<10;i++) {
			for(int j=0;j<20;j++) {
				System.out.print(board[i][j]);
			}
		System.out.println();
		}
	}
}

//Here goes the game
public class Game {
	private Board b;
	private Bear bear;
	private Fish fish;
	Scanner scanner = new Scanner(System.in);
	
	//instantiate GameObject to have a bear and fish & locate objects onto the board
	public Game() {
		int rx = (int)(Math.random()*10);
		int ry = (int)(Math.random()*20);
		this.b = new Board();
		this.bear = new Bear(0,0,0);
		this.fish = new Fish(rx,ry,0);
		b.board[bear.getX()][bear.getY()]= String.valueOf(bear.getShape());
		b.board[fish.getX()][fish.getY()]= String.valueOf(fish.getShape());
	}
	//move, move, move! One step at a time.
	void setLocation(GameObject obj) {
		int tmpx = obj.getX(); 
		int tmpy=obj.getY();
		b.board[obj.getX()][obj.getY()]= "-";
		obj.move();
		try {
			b.board[obj.getX()][obj.getY()]= String.valueOf(obj.getShape());
		} catch(ArrayIndexOutOfBoundsException e) {
			b.board[tmpx][tmpy]= String.valueOf(obj.getShape());
			obj.x = tmpx;
			obj.y = tmpy;
			System.out.println("Out of bounds! Try to move in another direction.");
		}
	}
	//execute the game
	void run() {
		System.out.println("**Bear goes Fishing.**");
		b.showBoard();
		fish.distance = 1;
		
		while(!bear.collide(fish)) {
			setLocation(bear);
			//fish moves twice after every 3 tries
			if((fish.distance-4)%5==0 || fish.distance%5==0) {
				setLocation(fish);
			}
			b.showBoard();
			fish.distance++;
			}
		System.out.println("Bear Wins!!");
	}
	//main method
	public static void main(String[] args) {
		Game g = new Game();
		g.run();
	}
}

````


### 문제 9 _ StackApp

````java

import java.util.Scanner;

interface Stack{
	int length();
	int capacity();
	String pop();
	boolean push(String val);
}

class StringStack implements Stack{
	//field
	private String [] s_stack;
	
	//constructor
	public StringStack(int size) {
		this.s_stack = new String[size];
	}
	
	//get method
	public String [] getStack() {
		return this.s_stack;
	}
	
	//number of elements
	public int length() {
		int length=0;
		for(String s:s_stack) {
			if(s!=null) {
				length++;
			}
		}
		return length;
	}

	//availability
	public int capacity() {
		return s_stack.length-length();
	}
	
	//pop
	public String pop() {
		String tmp = s_stack[length()-1];
		s_stack[length()-1]=null;
		return tmp;
	}

	//push
	public boolean push(String val) {
		if(capacity()>0) {
		s_stack[length()] = val;
		return true;}
		else {System.out.println("fully stacked"); return false;}
	}
}

public class StackApp {
	public static void main(String[] args) {
	
		Scanner scanner=new Scanner(System.in);
		System.out.println("size of your stack>>");
		int size = scanner.nextInt();
		
		StringStack s = new StringStack(size);
		
		while(s.capacity()>0) {
			System.out.println("let's push!>>");
			String str = scanner.next();
			
			if(str.equals("stop")) break;
			else s.push(str);
		}
		
		while(s.length()>0) {
			System.out.print(s.pop()+" ");
		}		
		scanner.close();
	}
}

````


### 문제 10 _ DictionaryApp

````java

import java.util.Arrays;

abstract class PairMap{
	protected String keyArray [];
	protected String valueArray [];
	abstract String get(String key);
	abstract void put(String key, String value);
	abstract String delete(String key);
	abstract int length();
}

class Dictionary extends PairMap{
	
	public Dictionary(int size) {
		this.keyArray = new String [size];
		this.valueArray = new String [size];
	}
	
	public int getIndex(String key) { //index
		return Arrays.asList(keyArray).indexOf(key);
	}
	
	public String get(String key) { //value 
		return valueArray[getIndex(key)];
	}
	
	public void put(String key, String value) {//store items
		if(length()==0) {
			keyArray[0] = key;
			valueArray[0] = value;
		}
		
		int count =0;
		for (int i = 0; i<keyArray.length;i++) {
			if(keyArray[i]==key) {
				valueArray[i]=value;
				count ++;
			}
		}
		
		if(count==0) {
			keyArray[length()] = key;
			valueArray[getIndex(key)] = value;
		}
	}
	
	public String delete(String key) {//delete
		String deleted = valueArray[getIndex(key)];
			valueArray[getIndex(key)] = null;

		return deleted; 
	}
	
	public int length() { //number of items
		int count=0;
		for (int i = 0; i<keyArray.length;i++) {
			if(keyArray[i]!=null) {
				count++;
			}
		}
		return count;
	}
}

public class DictionaryApp {
	public static void main(String[] args) {
		Dictionary dic = new Dictionary(10);
		dic.put("황기태",  "자바");
		dic.put("이재문", "파이선");
		dic.put("이재문", "C++");
		System.out.println("이재문의 값은 "+dic.get("이재문"));
		System.out.println("황기태의 값은 "+dic.get("황기태"));
		dic.delete("황기태");
		System.out.println("황기태의 값은 "+dic.get("황기태"));
	}
}

````


### 문제 12 _ GraphicEditor

````java

import java.util.Scanner;

abstract class Shape{
	private Shape next;
	public Shape() { next = null;}
	public void setNext(Shape obj) {next = obj;}
	public Shape getNext() {return next;}
	public abstract void draw();
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

public class GraphicEditor {
	private Shape start, last;
	private Scanner scanner = new Scanner(System.in);
	
	public GraphicEditor() {
		this.start = this.last = null;
	}
	
	private Shape createShape(int type) {
		Shape p = null;
		switch(type) {
		case 1: p= new Line(); break;
		case 2: p= new Rect(); break;
		case 3: p= new Circle(); break;
		}
		return p;
	}
	
	private void add(){//private access modifier since there is no chance to be called from outside
		Shape obj=null;
    
    //line 396-398: better keep to MVC(model, view, controller) pattern and write them in main method
		System.out.println("Line(1), Rect(2), Circle(3)>>");
		int type = scanner.nextInt();
		if(type<1 || type>3) {System.out.println("Type (1-3) only."); return;};
		if(start==null) {start = createShape(type); last = start;}
		else { obj = createShape(type); last.setNext(obj); last = obj;}
	}
	
	private void delete(){ 
  //can be implemented method with boolean-return value
		System.out.println("What item do you want to delete?[n-th]>>");
		int index = scanner.nextInt();
		try {
			Shape now = start; Shape pre = null;
		
			//1) empty
			if(start==null) {System.out.println("it's empty!");}
			else {
				//2) remove first element (single element case is also considered)
				if(index==1) {start = start.getNext();}
				//3) otherwise (last element and those int the middle)
				else { 
					int i=1;
					while(i<index) {
						pre = now;
						now = now.getNext();
						i++;
					}
					pre.setNext(now.getNext());
				}
			}
			
		} catch(NullPointerException e) {
            System.out.println("What you just typed does not exist.");
        }
	}
	
	private void viewall(){
		Shape p = start;
		while(p!=null) {
			p.draw();
			p= p.getNext();
		}
	}
	private void exit() {
		System.out.println("exit beauty");
		System.exit(0);
		scanner.close();
	}
	
	void run() {
		System.out.println("Let's begin beauty");
		
		while(true) {
		System.out.println("Add(1), Delete(2), View(3), Exit(4)>>");
		int option = scanner.nextInt();

			switch(option) {
				case 1: add(); break;
				case 2: delete(); break;
				case 3: viewall(); break;
				case 4: exit(); break;
			}
		}
	}
	
	public static void main(String[] args) {
		GraphicEditor g = new GraphicEditor();
		g.run();
	}
}

````


* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

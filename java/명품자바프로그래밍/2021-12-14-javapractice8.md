---
title: JAVA 스트림과 입출력_실습문제8
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
description: JAVA 스트림과 입출력_실습문제8
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-12-14'
---


### Open Challenge _행맨게임

````java

import java.io.*;
import java.util.*;

public class HangmanApp {
	private String filename;
	private Vector<String> wordVector = new Vector<>();
	private StringBuffer hiddenWord;
	private static int count;
	private static List<Integer> randoms;
	private int size;
	
	
	public HangmanApp(String filename, int size) {
		this.size = size;
		this.filename = filename;
		readFile();
	}
	
	//read file and insert all data to vector space
	private void readFile() {
		try {
			Scanner scanf = new Scanner(new FileReader(filename));
			while(scanf.hasNext()) {
				wordVector.add(scanf.nextLine().toLowerCase());
			}
		scanf.close();
		} catch (IOException e) {
			System.out.println("io error");
		}
	}
	
	//choose random word out of vector wordVector
	private String chooseRandomWord() {
		return wordVector.get((int)(Math.random()*wordVector.size()));
	}
	
	//set the random locations of blanks
	private List<Integer> getRandomidx(int length) {
		List<Integer> randoms = new ArrayList<Integer>();
		for(int i=0;i<length;i++) {
			randoms.add(i);
		}
		Collections.shuffle(randoms);
		return randoms;
	}
	
	//set blanks on random word for game
	private StringBuffer makeHidden(String randomWord) {
		hiddenWord = new StringBuffer(randomWord);
		randoms = getRandomidx(randomWord.length());

		if(randomWord.length()<size) { size = randomWord.length();}
		
			for (int i=0;i<size;i++) {
				hiddenWord.replace(randoms.get(i), randoms.get(i)+1, "_");
			}
		return hiddenWord;
	}
	
	//remove blank if the user's guess is right,
	//increase count if the guess is wrong and
	//show fail message if the user gives 5 wrong answers.
	private void checkAnswer(String randomWord, String guess) {
		boolean flag=false;
		
		if(randomWord.length()<size) { size = randomWord.length();}
		
		for (int i=0;i<size;i++) {
			if(randomWord.substring(randoms.get(i),randoms.get(i)+1).equals(guess)) {
				hiddenWord.replace(randoms.get(i), randoms.get(i)+1, guess);
				flag = true;
			}
		}
		if(flag==false) ++count;
		
		if(count==5) System.out.println("You've tried 5 times.. you failed.");
	}
	
	
	private void drawHangman() {
		StringBuffer first = new StringBuffer("     -----");
		StringBuffer second = new StringBuffer("     |   |");
		StringBuffer third = new StringBuffer("     o   |");
		StringBuffer fourth = new StringBuffer("         |");
		StringBuffer fifth = new StringBuffer("         |");
		StringBuffer sixth = new StringBuffer("   --------");
		
		if(count >0) fourth.replace(5, 6, "|"); 
		if(count>1) fourth.replace(4, 5, "/");
		if(count>2) fourth.replace(6, 7, "\\");
		if(count>3) fifth.replace(4, 5, "/");
		if(count>4) fifth.replace(6, 7, "\\");

		System.out.println(first+"\n"+second+"\n"+third+"\n"+fourth+"\n"+fifth+"\n"+sixth);
		
	}


	public void run() {
		Scanner scan = new Scanner(System.in);
		System.out.println("Let's play hangman!");
		String randomWord = chooseRandomWord();
		hiddenWord = makeHidden(randomWord);

		while(true) {
			System.out.println("**reference for test** "+randomWord);

			System.out.println(hiddenWord);
			System.out.print(">> ");
			String ans = scan.next().toLowerCase();
			checkAnswer(randomWord, ans);
			drawHangman();

			if(hiddenWord.indexOf("_")==-1  || count==5) {
				System.out.println(randomWord);
				System.out.println("Next(y/n)?");
				String choice = scan.next().toLowerCase();
				
				if(choice.equals("n")) break;
				else if(choice.equals("y")) {
					count = 0;
					randomWord = chooseRandomWord();
					hiddenWord = makeHidden(randomWord);
					continue;
				}
			}
		}
		scan.close();
	}
	
	public static void main(String[] args) {
		/*instantiate HangmanApp
		  enter 
		  filename that contains list of words and
		  number of blanks. you can increase the number to make this game harder.
		*/
		HangmanApp hm = new HangmanApp("words.txt", 4);
		hm.run();
	}
}

````

### 문제 7 _파일복사

````java

import java.io.*;

public class practice8_7 {
	public static void main(String[] args) {
		File src = new File("a.jpg");
		File dest = new File("b.jpg");
		
		try {
			FileInputStream fi = new FileInputStream(src);
			FileOutputStream fo = new FileOutputStream(dest);
			
			System.out.println(src.getName()+"를 "+dest.getName()+"로 복사합니다.");
			System.out.println("10%마다 *를 출력합니다.");
			
			byte [] buf = new byte[(int)Math.ceil(src.length()/10.0)];
			while(true) {
				int n = fi.read(buf);
				fo.write(buf, 0, n);	
				System.out.print("*");

				if(n<buf.length)
					break;
			}
			fi.close();
			fo.close();
			
		} catch(IOException e) {
			e.printStackTrace();
		}
	}
}

````

### 문제 11 _특정문자열로 시작하는 영어단어

````java

import java.util.*;
import java.io.*;

public class practice8_11 {
	Vector<String> v = new Vector<>();
	
	private boolean readWord() {
		System.out.println("words.txt is ready to print words.");
		try {
			Scanner scanner = new Scanner(new FileInputStream("words.txt"));
			while(scanner.hasNext()) {
				v.add(scanner.nextLine());
			}
			return true;
		} catch (IOException e) {
			return false;
		}
	}
	
	private int print(String word) {
		Iterator<String> it = v.iterator();
		int count=0;
		
		while(it.hasNext()) {
			String s = it.next();
			if(s.indexOf(word)==0) {
				System.out.println(s);
				count++;
			}
		}
		return count;
	}
	
	private void process() {
		Scanner scan = new Scanner(System.in);
		
		while(true) {
			System.out.print("word>> ");
			String word = scan.next();
			if(word.equals("stop")) {
				System.out.println("exit program");
				break;
			}
			if(print(word)==0) System.out.println("no such word");	
		}
		scan.close();
	}
	
	public void run() {
		if(readWord()) process();
	}
	
	public static void main(String[] args) {
		practice8_11 g = new practice8_11();
		g.run();		
	}
}

````


### 문제 12 _파일에 있는 단어 검색

````java

import java.io.*;
import java.util.*;

public class practice8_12 {
	Vector<String> v = new Vector<>();
	Scanner scan = new Scanner(System.in);

	private boolean completeVector() {
		System.out.println("If you type only file name, the file should be located in project folder");
		System.out.print("Enter file name>> ");
		String name= scan.next();
		
		try {
			Scanner scanf = new Scanner(new FileInputStream(name));
			
			while(scanf.hasNext()) {
				v.add(scanf.nextLine());
			}
			scanf.close();
			return true;

		} catch(IOException e) {
			e.printStackTrace();
			return false;
		}
	}  
	
	private void search() {
		scan.nextLine();

		while(true) {
			System.out.println("Enter word or sentence to be searched");
			String search = scan.nextLine();
			if(search.equals("stop")) {
				System.out.println("exit the program.");
				break;
			}
			
			for(int i=0;i<v.size();i++) {
				if(v.get(i).indexOf(search)!=-1) {
					System.out.printf("%4d: %s\n", i, v.get(i));
				}
			}
		}

	}

	private void run() {
		if(completeVector()) search();
	}
	
	public static void main(String[] args) {
		practice8_12 g = new practice8_12();
		g.run();
	}
}

````

### 문제 14 _파일탐색기

````java

import java.io.*;
import java.util.*;

public class exercise8_14 {
	private static String dirName;
	private Scanner scan = new Scanner(System.in);
	
	public exercise8_14(){
		dirName = "c:\\";
	}

	private String checkType(File dir) {
		String type ="";
		if(dir.isFile()) type = "dir";
		else type = "file";
		
		return type;
	}
	
	private void printDir(String dirName) {
		File dir = new File(dirName);
		File [] dirList = dir.listFiles();

		for(int i=0;i<dirList.length;i++) {
			System.out.printf("%4s\t%10d byte\t\t%s\n", checkType(dirList[i]), dirList[i].length(), dirList[i].getName());
			if(i==4 && dirList.length>10) {
				System.out.println("---생략---");
				i= dirList.length-3;
			}
		}		
	}
	
	private void makedir(String s) {
		File newFile = new File(dirName+"\\"+s);
		System.out.println(dirName+s);
		newFile.mkdir();
	}
	
	private void renamedir(String s1, String s2) {
		File f_s1 = new File(dirName+"\\"+s1);
		if(f_s1.exists()) f_s1.renameTo(new File(dirName+"\\"+s2));
	}
	
	private void movedir(String s) {
		if(s.equals("..")) {
			int index = dirName.lastIndexOf("\\");
			dirName = dirName.substring(0,index);
		} else {
			dirName +=("\\"+s);
		}
		
		File dir = new File(dirName);
		if(dir.exists()) {
			printDir(dirName);
		}
	}
	
	private void loop() {
		while(true) {
			System.out.println(">> ");
			String goTo = scan.nextLine();		
			StringTokenizer goToken = new StringTokenizer(goTo);
			
			String command = goToken.nextToken();
			
			if(command.equals("그만")) break;
			switch(command) {
			case "mkdir": makedir(goToken.nextToken()); break;
			case "rename": renamedir(goToken.nextToken(),goToken.nextToken()); break;
			default: movedir(goTo); break;
			
			}
		}
	}
	
	public void run() {
		System.out.println("***** 파일 탐색기입니다. *****");
		printDir(dirName);
		loop();
	}
	
	public static void main(String[] args) {
		exercise8_14 g = new exercise8_14();
		g.run();
	}
}

````

* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

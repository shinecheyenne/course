---
title: JAVA 반복문과 배열 실습문제
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
last_modified_at: '2021-10-28'
---


### Open Challenge: 카드 번호 맞추기 게임

````java
import java.util.Scanner;
import java.util.Random;
public class OpenChallenge {

	public static void main(String[] args) {
		Random r = new Random();
		int k = r.nextInt(100);
		
		Scanner scanner = new Scanner(System.in);
		System.out.println("수를 결정하였습니다. 맞추어 보세요\n0-99");
		
		while(true) {
			int userNumber = scanner.nextInt();
		
			if(userNumber<k) {
				System.out.println("더 높게");
				continue;}
			if(userNumber>k) {
				System.out.println("더 낮게");
				continue;}
			if(userNumber==k) {
				System.out.println("맞았습니다.\n다시 하시겠습니까?(y/n)");
				String text = scanner.next();
				if(text.equals("n")) {
					break;
				}
				else if(text.equals("y")) {
					continue;					
				}
			}
		}
		scanner.close();
	}
}
````


### 실습문제 1

````java
public class Practice_3 {
	
	//실습문제 1-1
	static int WhileT(int number) {	
		int sum=0, i=0;
		while(i<100) {
			sum = sum+i;
			i+=2;
			}
		return sum;
		}

	//실습문제 1-2
	static int WhileTest(int number) {
		int sum=0, i=0;
		while(i<number) {
			sum+=i;
			i+=2;
		}
		return sum;
		}

	//실습문제 1-3
	static int ForTest(int number) {
	int sum=0;
	for(int i=0;i<100;i+=2) {
		sum = sum+i;
	}
	return sum;
	}
	
	//실습문제 1-4
	static int DoWhileTest(int number) {
		int sum=0, i=0;
		do {
			sum+=i;
			i+=2;
		} while(i<number);
		return sum;
	}
	
	public static void main(String[] args) {
		int result = WhileTest(100);
		int result2 = DoWhileTest(100);
		int result3 = WhileT(100);
		int result4 = ForTest(100);
		System.out.print(result+"\n");
		System.out.print(result2+"\n");
		System.out.print(result3+"\n");
		System.out.print(result4+"\n");
	}
}
````


### 실습문제 2

````java
public class Practice_3 {
	public static void main(String[] args) {
		int n [][] = { {1}, {1,2,3}, {1}, {1,2,3,4}, {1,2} };
	
		for (int i=0;i<n.length;i++) {
			for(int j=0;j<n[i].length;j++) {
				System.out.print(n[i][j]+" ");
			}
			System.out.println();
		}
	}
}
````


### 실습문제 3

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("정수를 입력하시오>>");
		int size = scanner.nextInt();

		for(int i=size;i>0; i--) {
			for(int j=i;j>0;j--) {
				System.out.print("*");
			}
		System.out.println();
		}
	}
}
````


### 실습문제 4

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("소문자 알파벳 하나를 입력하시오>>");
		String text = scanner.nextLine();
		char myText = text.charAt(0);

		for(int j=0;j<myText-97+1;j++) {
		for(int i=97;i<=myText-j;i++) {
			System.out.print((char)(i));
		}
		System.out.println();
		}
	}
}
````


### 실습문제 5

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		int arr [] = new int[10];
		Scanner scanner = new Scanner(System.in);
		System.out.print("양의 정수 10개를 입력하시오>>");

		for(int i=0; i<arr.length;i++) {
			arr[i]= scanner.nextInt();
			if(i==0) {
				System.out.print("3의 배수는 ");
			}
			if(arr[i]%3!=0)
				continue;
			else {
				System.out.print(arr[i]+" ");}
			}
	}
}
````


### 실습문제 6

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		int [] unit = {50000, 10000, 1000, 500, 100, 50, 10, 1};

		Scanner scanner = new Scanner(System.in);
		System.out.print("금액을 입력하시오>>");
		int amount = scanner.nextInt();

		for(int i=0;i<unit.length;i++) {
			if(amount/unit[i]==0)
				continue;
			else {
			System.out.println(unit[i]+"원 짜리: "+amount/unit[i]+"개");
			amount=amount%unit[i];}
		}
	}
}
````


### 실습문제 7

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		int arr [] = new int[10];
		int sum=0;;
		for(int n=0;n<arr.length;n++) {
			int i = (int)(Math.random()*10+1);
			arr[n] = i;
			sum +=arr[n];
			if(n==0)
				System.out.print("랜덤한 정수들 : ");
			else {
			System.out.print(arr[n]+" ");
			}
		}
		System.out.println("\n평균은 "+sum/arr.length);
	}
}
````


### 실습문제 8

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("size?");
		int size = scanner.nextInt();
		int arr []= new int[size];

		    for (int i=0; i<size;i++){
		        int num = (int)(Math.random()*30+1);
		        int count=0;
		        for(int j=0;j<i;j++){
		            if(arr[j]==num){
		                count++;
		            }
		        }
		        if(count!=0){
		            i--;
		            continue;
		        }
		        arr[i]=num;

		        System.out.print(arr[i]+" ");
		    }
		scanner.close();
	}
}
````


### 실습문제 9

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		int arr [][]= new int [4][4];

		for (int i=0;i<arr.length;i++) {
			for(int j=0;j<arr[i].length;j++) {
				int num = (int)(Math.random()*10+1);
				arr[i][j]=num;
				System.out.print(arr[i][j]+" ");
			}
			System.out.println();
		}
	}
}
````


### 실습문제 10

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		int arr [][]= new int [4][4];
		int i,j,count = 0;
		
		while(count<10) {
			i=(int)(Math.random()*4);
			j=(int)(Math.random()*4);			
			if(arr[i][j]==0) {
				arr[i][j] = (int)(Math.random()*10+1);
				count++;
			}
		}
		
		for (int k=0;k<arr.length;k++) {
			for(int m=0;m<arr[k].length;m++) {
				System.out.print(arr[k][m]+" ");
			}
			System.out.println();
		}
	}
}
````


### 실습문제 11

````java
public class Average {
	public static void main(String[] args) {
		int sum=0;
		for(int i=0;i<args.length;i++)
			sum += Integer.parseInt(args[i]);
		System.out.println("average="+sum/args.length);
	}
}
````


### 실습문제 12

````java
public class Add {
	public static void main(String[] args) {
		int sum=0;

		for(int i=0;i<args.length;i++)
			try {
			//if(Integer.parseInt(args[i])%10==0) 
				sum+=Integer.parseInt(args[i]);
		}
		catch(NumberFormatException e) {
			continue;
		}	
		System.out.println(sum);
	}
}
````


### 실습문제 13

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);

		while(true) {
			System.out.print("369게임입니다. 1-99 숫자를 입력하세요>>");
	
			int num = scanner.nextInt();
			if((num/10)%3==0 && num>=10) {
				if((num%10)%3==0) {
					System.out.print("박수 짝짝");
				}
				else {System.out.print("박수 짝");
				}
			}
			else {
				if((num%10)%3==0) {
					System.out.println("박수 짝");
				}
				else {System.out.println("다시 입력하세요");
				}
			}
		}
	}
}
````


### 실습문제 14

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		String course [] = {"Java", "C++", "HTML5", "컴퓨터구조", "안드로이드"};
		int score [] = {95, 88, 76, 62, 55};
		int count = 0;

		Scanner scanner = new Scanner(System.in);

		while(true) {
		System.out.print("과목 이름>>");
		String name = scanner.nextLine();

		if(name.contentEquals("그만"))
			break;

		for(int i=0;i<course.length;i++) {
			if(name.contentEquals(course[i])) {
				System.out.println(course[i]+"의 점수는 "+score[i]);
			}
			else {
				count++;
			}
		}
		if(count==course.length) {
		System.out.println("없는 과목입니다.");
		}
		}
	}
}
````


### 실습문제 15

````java
import java.util.Scanner;
import java.util.InputMismatchException;
public class Practice_3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		while(true) {
			System.out.print("input two numbers>>");	
			try {
				int n = scanner.nextInt();
				int m = scanner.nextInt();
				System.out.print(n+"x"+m+"="+n*m);
				break;
			}
			catch(InputMismatchException e) {
				System.out.print("No float!");
				scanner.nextLine();			
			}	
		}
		scanner.close();
	}
}
````


### 실습문제 16

````java
import java.util.Scanner;
public class Practice_3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("컴퓨터와 가위 바위 보 게임을 합니다.");

		while(true) {
			System.out.println("가위 바위 보!>>");
			String user = scanner.nextLine();
			String str[]= {"가위", "바위","보"};
			String com = str[(int)(Math.random()*3)];
			String result="";
			
			if(user.equals("그만")) {
				System.out.println("게임을 종료합니다...");
				break;
			}
			
			System.out.print("사용자="+user+", 컴퓨터="+com);
			if(user.equals(com)) {
				System.out.println(". 비겼습니다.");
				continue;
			}
			else if((user.equals("가위")&&com.equals("보"))||(user.equals("보")&&com.equals("바위"))||(user.equals("바위")&&com.equals("가위"))) {
				System.out.println(". 이겼습니다.");
				continue;
			}
			else {
				System.out.println(". 졌습니다.");
				continue;
			}
		}			
	scanner.close();	
	}
}
````


* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

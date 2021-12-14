---
title: JAVA 입출력 스트림과 파일 입출력
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
description: JAVA 입출력 스트림과 파일 입출력
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-12-14'
---


### 문자 스트림

문자 스트림은 2바이트의 유니코드 문자를 단위로 입출력하는 스트림.

#### FileReader 이용

````java

//파일 입력 스트림 생성하고, c:\test.txt 파일을 연결한다.
FileReader fin = new FileReader("c:\\test.text");
int c;
//read()는 문자 하나를 읽어 리턴하며, 파일의 끝을 만나면 -1을 리턴한다.
while((c=fin.read() !=-1){
  System.out.print((char)c);
}

//블록(버퍼크기) 만큼 read (파일이 큰 경우)
//버퍼: 읽고 쓸 데이터를 저장하는 배열
//buf 에 실제 데이터 저장됨. n: 읽은 개수
//char [] buf = new char [1024];
//int n = fin.read(buf);

//스트림 닫기
fin.close();

````

#### 예외처리

````java

try{ ...
  } catch(FileNotFoundException e){...
  } catch(IOException e){...
  }
  
````

* FileReader로 텍스트 파일 읽기

````java

import java.io.*;

public class practice8_1 {
	public static void main(String[] args) {
		FileReader fin = null;
		try {
			fin = new FileReader("c:\\windows\\system.ini");
			int c;
			while((c=fin.read()) != -1) {
				System.out.print((char)c);
			}
			fin.close();
		} catch(IOException e) {
			System.out.println("입출력 오류");
		}
	}
}

````

#### InputStreamReader로 한글 텍스트 파일 읽기

````java

import java.io.*;

public class practice8_2 {
	public static void main(String[] args) {
		
		//바이트 스트림을 전달받아 문자 집합을 통해 문자 정보로 변환하는 스트림 객체
		InputStreamReader in = null;
		//바이트 파일 입력 스트림
		FileInputStream fin = null;
		
		try {
			fin = new FileInputStream("c:\\Temp\\hangul.txt");
			in = new InputStreamReader(fin, "MS949"); //바이트를 문자로 인코딩하기 위한 문자 집합 지정
			int c;
			
			System.out.println("인코딩 문자 집합은 "+in.getEncoding());
			while((c=in.read())!=-1) {
				System.out.print((char)c);
			}
			in.close();
			fin.close();
		} catch(IOException e) {
			System.out.println("입출력 오류");
		}
	}
}

````

#### FileWriter 이용한 텍스트 파일 쓰기

````java

import java.io.*;
import java.util.*;

public class practice8_3 {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		FileWriter fout = null;
		int c;
		try {
			//파일과 연결된 출력 문자 스트림 생성
			fout = new FileWriter("c:\\Temp\\test.text");
			while(true) {
				String line = scanner.nextLine();
				if(line.length()==0)
					break;
				fout.write(line, 0, line.length());
				fout.write("\r\n", 0,2);
			}
			fout.close();
		} catch(IOException e) {
			System.out.println("입출력 오류");
		}
		scanner.close();
	}
}

````

### 바이트 스트림

바이트 단위로 바이너리 데이터가 흐르는 스트림. 바이너리 데이터를 있는 그대로 입출력하기 때문에 이미지, 동영상 파일 입출력에 필수적이다.
InputStream / OutputStream : 추상 클래스, 바이트 입출력 처리를 위한 공통 기능을 가진 슈퍼 클래스
FileInputStream / FileOutputStream
DataInputStream / DataOutputStream

#### FileoutputStream 으로 바이너리 파일 쓰기

````java

import java.io.*;

public class practice8_5 {
	public static void main(String[] args) {
		byte b[] = {7, 51, 3, 4};
		
		try {
			FileOutputStream fout = new FileOutputStream("c:\\Temp\\test.out");
			for(int i=0;i<b.length;i++) 
				fout.write(b[i]);
			fout.close();
			} catch(IOException e) {
				System.out.println("오류");
				return;
			}
			System.out.println("저장완료");
		}
	}

````

#### FileInputStream으로 바이너리 파일 읽기

````java

import java.io.*;

public class practice8_6 {
	public static void main(String[] args) {
		byte b[] = new byte[6];
		try {
			FileInputStream fin = new FileInputStream("c:\\Temp\\test.out");
//			int n=0, c;
//			while((c=fin.read())!=-1) {
//				b[n]=(byte)c;
//				n++;
//			}
			//최대 배열 b의 크기만큼 바이트를 읽음
			fin.read(b);
			
			//배열 b[]의 바이트 값을 모두 화면에 출력
			for(int i=0;i<b.length;i++)
				System.out.print(b[i]+" ");
			fin.close();
		} catch(IOException e) {
			System.out.println("오류");
		}
	}
}

````

### 버퍼 입출력

````java

import java.io.*;
import java.util.Scanner;

public class BufferedIOEx{
  public static void main(String[] args){
    FileReader fin = null;
    int c;
    try{
      fin = new FileReader("c:\\...");
      //버퍼 출력 스트림 생성. 20바이트 크기의 버퍼를 가지고, 표준 출력 스트림(System.out)에 연결하여 화면에 출력하는 버퍼 스트림 생성
      //버퍼 스트림 클래스의 생성자는 모두 바이트 스트림 또는 문자 스트림과 연결하여 사용한다.
      BufferedOutputStream out= new BufferedOutputStream(System.out ,5);
      while((c=fin.read())!=-1){ //파일 끝을 만날 때까지 문자를 하나씩 읽는다.
        out.write(c); //읽은 문자를 버퍼 출력 스트림에 쓴다. 출력 스트림과 연결된 화면에 출력된다.
      }
      new Scanner(System.in).nextLine();
      out.flush();//버퍼에 남아 있던 문자 모두 출력
      fin.close();
      out.close();
    } catch(IOException e){
        e.printStackTrace();
    }
  }
}

````

### 블록 단위로 파일 복사

````java

import java.io.*;

public class practice8_11 {
	public static void main(String[] args) {
		File src = new File("c:\\Windows\\Web\\Wallpaper\\Theme1\\img1.jpg");
		File dest = new File("c:\\Temp\\copyimg.jpg");
		
		try {
			FileInputStream fi = new FileInputStream(src);
			FileOutputStream fo = new FileOutputStream(dest);
			
			byte [] buf = new byte[1024*10];
			while(true) {
				int n = fi.read(buf);
				fo.write(buf, 0, n);
				if(n<buf.length)
					break;
			}
			fi.close();
			fo.close();
			System.out.println(src.getPath()+"를 "+dest.getPath()+"로 복사함");
		} catch(IOException e) {
			System.out.println("파일 복사 오류");
		}
	}
}

````

* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

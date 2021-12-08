---
title: JAVA 시작하기
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
description: JAVA 시작하기
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-10-12'
---

## 자바의 플랫폼 독립성, WORA(Write Once Run Anywhere)
하드웨어 독립적인 바이트 코드와 이를 실행하는 자바 가상 기계에 의해 한 번 프로그램을 작성하면 어느 플랫폼에서도 자바 프로그램을 실행시킬 수 있는데, 이를 WORA(Write Once Run Anywhere)라고 한다.

### 바이트 코드
자바 가상 기계에서만 실행되는 기계어로서, 어떤 CPU와도 관계없는 바이너리 코드(binary code)이다. 자바 컴파일러는 자바 소스 프로그램을 컴파일하여 바이트 코드로 된 클래스 파일을 생성한다. 이 클래스 파일은 컴퓨터의 CPU에 의해 직접 실행되지 않고, 자바 가상 기계가 인터프리터 방식으로 실행시킨다.
오라클에서 배포하는 JDK(Java Development Kit)에는 자바 클래스 파일을 디어셈블(diassemble)하여 바이트 코드를 볼 수 있는 도구(javap)를 제공한다.

### 자바 가상 기계
서로 다른 플랫폼에서 자바 프로그램이 실행되는 동일한 환경을 제공한다.

## 자바 설치
자바 프로그램을 개발하고 실행하기 위한 환경은 JDK/JRE에서 제공하며, IDE 환경을 제공하는 도구에는 이클립스, 인텔리J 등이 있다.
* JDK 설치 후 시스템 환경변수편집
<img src="/images/Inkedsetting.jpg"  width="600" height="400"/>
<img src="/images/Inkedpath.jpg"  width="600" height="400"/>
* cmd 창에서 javac(자바 컴파일러) 확인
<img src="/images/Inkedjavac.jpg"  width="600" height="400"/>

## 소스와 클래스 파일
클래스 파일(.class)에는 반드시 하나의 자바 클래스만 들어 있다. 하나의 자바 소스 파일에 작성된 클래스 중 오직 한 클래스만 public으로 선언할 수 있다. 소스 파일 내에 public으로 선언된 클래스의 이름으로 자바 소스 파일을 저장해야 한다.

## 실행 코드 배포
자바 응용프로그램은 한 개의 클래스 파일 또는 다수의 클래스 파일로 구성된다. 다수의 클래스 파일을 jar 파일 형태로 압축하여 배포하거나 실행할 수 있다. 자바 프로그램은 class 키워드의 클래스 선언으로 시작하며, 클래스 내에서 모든 변수나 메소드를 정의한다. 자바의 실행은 main() 메소드부터 시작되며, 하나의 클래스 파일에 두 개 이상의 main() 메소드가 있을 수 없다.

## Hello2030 출력 예제

````java
public class Hello2030 {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		// 하나의 클래스에는 하나의 main()만 존재
		//출력값[void]: 출력값이 없다, public: 실행 권한(모두)
		int n = 2030;
		System.out.println("헬로" + n);//out:객체
	}
}
````
````java
// 출력 
헬로2030
````

* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

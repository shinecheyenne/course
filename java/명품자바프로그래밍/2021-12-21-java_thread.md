---
title: JAVA 스레드와 멀티태스킹
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
description: JAVA 스레드와 멀티태스킹
article_tag1: 
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: java
last_modified_at: '2021-12-21'
---


### 멀티스레딩

하나의 응용 프로그램을 동시처리가 가능한 여러 작업으로 분할하고 작업의 개수만큼 스레드를 생성하여 작업을 처리하도록 하는 기번으로, 모든 스레드는 응용 프로그램 내의 자원과 메모리를 공유하므로 통신에 따른 오버헤드가 작고, 스레드 사이의 문맥 교환이 빠르다.
즉, 멀티스레딩은 응용 프로그램이 다수의 스레드를 가지고 다수의 작업을 동시에 처리함으로써, 한 스레드가 대기하는 동안 다른 스레드를 실행하여 시간 지연을 줄이고 자원의 비효율적 사용을 개선한다.

자바의 경우 사용자가 자바 응용프로그램을 실행시키면, JVM에 실행되고 JVM은 응용 프로그램을 실행시킨다. 하나의 응용 프로그램 당 하나의 JVM이 실행되며 JVM은 멀티 스레딩을 지원하므로 응용 프로그램은 하나 이상의 자바 스레드(JVM에 의해 스케줄되는 실행 단위 코드 블록)를 생성할 수 있다.
스레드를 관리하는 일은 모두 JVM에 의해 이루어지며 사용자는 스레드 코드 작성, JVM에 스레드를 생성하고 스레드 코드를 실행하도록 요청하는 두 가지 작업을 하여야 한다.

### 스레드 코드 작성

#### Thread 클래스 이용

1) 스레드 클래스 작성: Thread 클래스 상속
2) 스레드 코드 작성: run() 메소드 오버라이딩. 스레드는 run()에서부터 실행을 시작하고 run()이 종료하면 스레드도 종료한다.
3) 스레드 객체 생성
4) 스레드 시작: start() 메소드 호출. 생성된 스레드 객체를 스케줄링이 가능한 상태로 전환하도록 JVM에 지시. 스케줄링에 의해 스레드가 선택되면 JVM에 의해 run()메소드가 호출됨
 
- sleep(long mills): 스레드가 잠을 자면 JVM은 다른 스레드를 실행시킨다. 스레드는 sleep() 동안 발생하는 InterruptedException예외를 처리할 try-catch 블록을 반드시 가져야 한다.

- 예제1

````java

import java.awt.*;
import javax.swing.*;

class TimerThread extends Thread{
	private JLabel timerLabel;
	
	public TimerThread(JLabel timerLabel) {
		this.timerLabel = timerLabel;
	}
	
	@Override
	public void run() {
		int n = 0;
		while(true) {
			timerLabel.setText(Integer.toString(n));
			n++;
			try {
				Thread.sleep(1000);
			} catch(InterruptedException e) {
				return; //예외가 발생하면 스레드 종료
			}
		}
	}
}

public class ThreadTimerEx extends JFrame{
	public ThreadTimerEx() {
		setTitle("Thread를 상속받은 타이머 스레드 예제");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.setLayout(new FlowLayout());
		
		JLabel timerLabel = new JLabel();
		timerLabel.setFont(new Font("Gothic", Font.ITALIC, 80));
		c.add(timerLabel);
		
		TimerThread th = new TimerThread(timerLabel);
		
		setSize(300,170);
		setVisible(true);
		
		th.start();
	}
	public static void main(String[] args) {
		new ThreadTimerEx();
	}
}

````

- 예제2

````java

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class RandomThread extends Thread{
	private Container contentPane;
	private boolean flag = false;
	
	public RandomThread(Container contentPane) {
		this.contentPane = contentPane;
	}
	public void finish() {flag = true;}
	
	@Override
	public void run() {
		while(true) {
			int x = ((int)(Math.random()*contentPane.getWidth()));
			int y = ((int)(Math.random()*contentPane.getHeight()));
			JLabel label = new JLabel("java");
			label.setSize(80,30);label.setLocation(x, y);
			contentPane.add(label); contentPane.repaint();
			
			try {
				Thread.sleep(300);
				if(flag==true) {
					contentPane.removeAll();
					label = new JLabel("finish");
					label.setSize(80,30); label.setLocation(100,100);label.setForeground(Color.RED);
					contentPane.add(label); contentPane.repaint();
					return;
				}
			}catch(InterruptedException e) {return;}
		}
	}
}
public class ThreadFinishFlagEx extends JFrame{
	private RandomThread th; //스레드 레퍼런스
	
	public ThreadFinishFlagEx() {
		setTitle("ThreadFinishFlagEx 예제");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.setLayout(null);
		
		c.addMouseListener(new MouseAdapter() {
			@Override
			public void mousePressed(MouseEvent e) {
				th.finish();
			}
		});
		setSize(300,200);setVisible(true);
		
		th = new RandomThread(c);
		th.start();
	}
	public static void main(String[] args) {
		new ThreadFinishFlagEx();
	}
}

````

#### Runnable 인터페이스 이용

Runnable 인터페이스를 이용하여 스레드를 작성하면 Thread 클래스를 이용하는 것과 달리 다른 클래스를 상속받을 수 있는 유연성을 확보할 수 있다.

````java

interface Runnable{
  public void run();

````

- 예제1

````java

import java.awt.*;
import javax.swing.*;

class TimerRunnable implements Runnable{
	private JLabel timerLabel;
	
	public TimerRunnable(JLabel timerLabel) {
		this.timerLabel = timerLabel;
	}
	public void run() {
		int n = 0;
		while(true) {
			timerLabel.setText(Integer.toString(n));
			n++;
			try {
				Thread.sleep(1000);
			} catch(InterruptedException e) {
				return;
			}
		}
	}
}
public class RunnableTimerEx extends JFrame{
	public RunnableTimerEx() {
		setTitle("Runnable을 구현한 타이머 스레드 예제");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.setLayout(new FlowLayout());
		
		JLabel timerLabel = new JLabel();
		timerLabel.setFont(new Font("Gothic", Font.ITALIC, 80));
		c.add(timerLabel);
		
		//스레드 코드로 작동할 run()이 구현된 Runnable 객체 생성
		TimerRunnable runnable = new TimerRunnable(timerLabel);
		//스레드 객체 생성
		Thread th = new Thread(runnable);
		
		JButton btn = new JButton("kill Timer");
		btn.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				th.interrupt(); //타이머 스레드 강제 종료
				JButton btn = (JButton)e.getSource();
				btn.setEnabled(false); //버튼 비활성화
			}
		});
		c.add(btn);
		
		setSize(250,150);
		setVisible(true);
		
		th.start();
	}
	public static void main(String[] args) {
		new RunnableTimerEx();
	}
}


````

- 예제2

````java

import java.awt.*;
import javax.swing.*;

class FlickeringLabel extends JLabel implements Runnable{
	private long delay;
	public FlickeringLabel(String text, long delay) {
		super(text); //JLabel 생성자 호출
		this.delay = delay;
		setOpaque(true);
		
		Thread th = new Thread(this);
		th.start();
	}
	@Override
	public void run() {
		int n=0;
		while(true) {
			if(n==0) setBackground(Color.YELLOW);
			else setBackground(Color.GREEN);
			if(n==0) n=1;
			else n=0;
			try {
				Thread.sleep(delay);
			} catch(InterruptedException e) {
				return;
			}
		}
	}
}
public class FlickeringLabelEx extends JFrame{
	public FlickeringLabelEx() {
		setTitle("FlickeringLabelEx 예제");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.setLayout(new FlowLayout());
		
		FlickeringLabel fLabel = new FlickeringLabel("깜박", 500);
		JLabel label = new JLabel("안깜박");
		FlickeringLabel fLabel2 = new FlickeringLabel("여기도 깜박", 300);
		
		c.add(fLabel);c.add(label);c.add(fLabel2);
		setSize(300,150);setVisible(true);
	}

	public static void main(String[] args) {
		new FlickeringLabelEx();
	}
}

````

### 스레드 동기화

다수의 스레드가 공유 데이터에 동시 접근하는 경우 스레드 동기화가 필요하다. 스레드 동기화랑 공유 데이터에 접근하고자 하는 다수의 스레드가 서로 순서대로 충돌 없이 공유 데이터에 배타적이고 독점적으로 접근하기 위해 상호 협력하는 것을 말한다.
스레드 동기화는 synchronized로 동기화 블록 지정을 하거나, wait()-notify() 메소드로 스레드 실행 순서를 제어할 수 있다.

#### synchronized 키워드

synchronized 키워드는 스레드 동기화를 위한 장치로서 임의의 코드 블록을 동기화가 설정된 임계 영역으로 지정한다. 메소드 전체나 코드 블록을 임계 영역/동기화 블록으로 지정하여, 한 스레드가 코드 블록에 먼저 진입하면 다른 스레드는 대기한다. synchronized 블록은 진입할 때 락(lock)이 걸리고 빠져나올 때 풀리는(unlock) 동작이 자동으로 이루어지도록 컴파일된다.

- 예제

````java

public class SychronizedEx {
	public static void main(String[] args) {
		SharedBoard board = new SharedBoard();
		
		Thread th1 = new StudentThread("kitae", board);
		Thread th2 = new StudentThread("hyosoo", board);
		
		th1.start();
		th2.start();
	}
}

class SharedBoard{
	private int sum = 0;
	synchronized public void add() {
		int n = sum;
		Thread.yield(); //현재 실행 중인 스레드 양보
		n+=10;
		sum = n;
		System.out.println(Thread.currentThread().getName()+":"+sum);
	}
	public int getSum() {return sum;}
}

class StudentThread extends Thread{
	private SharedBoard board;
	
	public StudentThread(String name, SharedBoard board) {
		super(name);
		this.board = board;
	}
	@Override
	public void run() {
		for(int i=0;i<10;i++) {
			board.add();
		}
	}
}

````

#### wait()-notify()/notifyAll() 이용한 스레드 동기화

synchronized 키워드를 이용하하여 공유 데이터에 스레드가 순차적으로 접근하도록 처리한 경우라도 공유 메모리를 통해 두 스레드가 데이터를 주고받을 때, 공유 메모리에 대해 두 스레드가 동시에 접근하는 producer-consumer 문제가 발생하는 경우 여전히 동기화가 필요하다.
java.lang.Object 클래스는 스레드 동기화를 위한 메소드 wait(), notify(), notifyAll()을 제공한다. 이 메소드를 호출하는 코드는 synchronized로 지정되어 있어야 하며, 그렇지 않으면 실행 시 예외가 발생한다. 모든 객체는 Object 클래스를 상속받으므로, 자바는 모든 객체가 동기화 객체가 될 수 있다.

- wait() : 다른 스레드가 이 객체의 notify()를 불러줄 때까지 대기한다.
- notify() : 이 객체에 대기 중인 스레드를 깨워 RUNNABLE 상태로 만든다.
- notifyAll() : 모든 스레드를 깨운다.

- 예제

````java

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class MyLabel extends JLabel{
	private int barSize = 0;
	private int maxBarSize;
	
	public MyLabel(int maxBarSize) {
		this.maxBarSize = maxBarSize;
	}
	@Override
	public void paintComponent(Graphics g) {
		super.paintComponent(g);
		g.setColor(Color.MAGENTA);
		int width = (int)(((double)(this.getWidth()))/maxBarSize*barSize);
		if(width==0) return;
		g.fillRect(0, 0, width, this.getHeight());
	}
	
	synchronized public void fill() {
		if(barSize == maxBarSize) {
			try {
				wait();
			} catch(InterruptedException e) {return;}
		}
		barSize++;
		repaint();
		notify();
	}
	synchronized public void consume() {
		if(barSize ==0) {
			try {
				wait();
			} catch(InterruptedException e) {return;}
		}
		barSize--;
		repaint();
		notify();
	}
}

class ConsumerThread extends Thread{
	private MyLabel bar;
	public ConsumerThread(MyLabel bar) {
		this.bar =bar;
	}
	@Override
	public void run() {
		while(true) {
			try {
				sleep(200);
				bar.consume();
			} catch(InterruptedException e) { return;}
		}
	}
}

public class TabAndThreadEx extends JFrame{
	private MyLabel bar = new MyLabel(100);
	
	public TabAndThreadEx(String title) {
		super(title);
		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		Container c = getContentPane();
		c.setLayout(null);
		bar.setBackground(Color.ORANGE);bar.setOpaque(true);bar.setLocation(20, 50);bar.setSize(300,20);
		c.add(bar);
		
		c.addKeyListener(new KeyAdapter(){
			@Override
			public void keyPressed(KeyEvent e) {
				bar.fill();
			}
		});
		setSize(350,200); setVisible(true);
		
		c.setFocusable(true); c.requestFocus();
		ConsumerThread th = new ConsumerThread(bar);
		th.start();
	}
	public static void main(String[] args) {
		new TabAndThreadEx("아무 키나 빨리 눌러 키 채우기");
	}
}


````

* 참고자료: 명품 JAVA Programming, 황기태.김효수 지음, 생능출판

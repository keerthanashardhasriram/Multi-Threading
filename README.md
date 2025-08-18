# Multi-Threading
Multi Tasking: Operating multiple tasks at the same time.
Basically classified into 2 types:
1. Process
2. Threads
let us say that there are 3 Softwares running on an OS which present on Hard ware layer.
Haerd ware consists of :  CPU  and  RAM
1. CPU : processing and execution takes place here.
2. RAM : acts as a temporary storage unit for processing.

Real-time example for Multi Tasking is Web-Server : ->Handling request from client n number of clients.
-> sending and receving messages in whatsapp.

OS supports multiple softwares working at the same time which means it supports Multi Tasking.

Multi Tasking is the ability of CPU to perform multiple tasks simultaneously with continuous context switching between the task
CPU follows a concept called as time-sharing each process runs for a short peiod of time one by one. Software runs parallely by sharinng the time in CPU.

We can alos divide the task into small units called as Threads.
In the same task, we can have  multiple task running at the same time.
Thread is program level where as process is OS level.

Multi-Threading:
It is the system where multiple Threads are created from a process through which the computer power increases.
If you want to execute 2 methods at the same time then we use threads.
We cannot execute normal objects in multiple threads or normal objects can not be executed simultaneously.

There are 2 types of creating a thread: 
1. By extending a Thread class.
2. By implementing a Runnable Interface.



1. By extending a Thread class.

Java provides a Thread class to acheive thread programming. It contains Thread based libraries.
Thread class provides constructors and methods to create and perform Thread operations.
A thread object can be created by extending its class to a Thread class.
Thread class is present in java.lang since JDK 1.0

Applications: Animations, video game, defence, servers


To create a Thread by extending a Thread class.
1. Create a class, make it a child of Thread class.
2. Override run().
3. Instantiate the thread and invoke start(). 

We can only create a new thread by using start() in the main() where the execution of new thread begins.
start() is present in Thread class, it only invokes the run() on the thread object.
run() should be present in every thread to start a new thread.
run() is used to do an action for a thread.

All threads cannot run at the same time, so threads go for time sharing.
Many processes will be allocated with computer resources in time slots.
Schedular is responsible to allow which thread to execute at what time.

package Snippets;

public class ThreadA extends Thread{
	public void run() {
		for (int i = 1; i <= 5; i++) {
			System.out.println("Thread A");
		}
	}
}


package Snippets;

public class ThreadB extends Thread{
	public void run() {
		for (int i = 1; i <= 5; i++) {
			System.out.println("Thread B  ");
		}
	}
}



package Snippets;

public class Demo1 {
public static void main(String[] args) {
		
		ThreadA a=new ThreadA();
		ThreadB b=new ThreadB();
		
		a.start();
		b.start();
	}
}

Output:
Thread B  
Thread B  
Thread B  
Thread B  
Thread A
Thread A
Thread A
Thread A
Thread A
Thread B  

Thread has 3 properties: 
1. Thread Id: If you want to identify a thread uniquely, we use ThreadId, the id for a thread will be given by jvm only. It is global. It i private in Thread class. It is read only not writeonly we have getId() in java.

2. Thread Name: Usec to identify the Thread easily. It is global. It i private in Thread class. It has getName() and setName()
3. Thread priority: It is global. It i private in Thread class. It has getPriority() (used to get the priority of the currrent thread) and setPriority() (used to set the priority of the currrent thread).
   So here 5 is the default priority, Thread schedular gives the priority to the thread. Different schedular has different algorithms. We can only suggest the Schedular 
   It is mostly that a thread with less running time will get the highest priority
Java Thread Priority Constants:
These constants are used to set the priority of a thread, which helps the Thread Scheduler decide the execution order (though not guaranteed, especially in JVMs that ignore priority).

    /**
     * The minimum priority that a thread can have.
     */
    public static final int MIN_PRIORITY = 1;

    /**
     * The default priority that is assigned to a thread.
     */
    public static final int NORM_PRIORITY = 5;

    /**
     * The maximum priority that a thread can have.
     */
    public static final int MAX_PRIORITY = 10;


   package Snippets;

public class Demo1 {
public static void main(String[] args) {
		
		ThreadA a=new ThreadA();
		ThreadB b=new ThreadB();
		
		//a.start();
		//b.start();
		System.out.println("A "+a.getId());
		System.out.println("B "+b.getId());
		System.out.println("A, Before setname() "+a.getName());
		a.setName("Thread A");
		System.out.println("A, After setname() "+a.getName());
		System.out.println("B, Before setname() "+b.getName());
		b.setName("Thread B");
		System.out.println("B, After setname() "+b.getName());
		
		System.out.println("A, Before setPriority() "+a.getPriority());
		a.setPriority(7);
		System.out.println("A, After setPriority() "+a.getPriority());
		System.out.println("B, Before setPriority() "+b.getPriority());
		b.setPriority(9);
		System.out.println("B, After setPriority() "+b.getPriority());
	}
}

Output:
A 21
B 22
A, Before setname() Thread-0
A, After setname() Thread A
B, Before setname() Thread-1
B, After setname() Thread B
A, Before setPriority() 5
A, After setPriority() 7
B, Before setPriority() 5
B, After setPriority() 9

Thread Schedular:Present as principal inside the jvm
1. start() is used to register the Thread with Thread Schedular, it will create a new stack
2. then start() allocates new call stack for a thread
3. then it invokes run(), run() is used to do an action for a thread.

   run() is present in Runnable Interface, in java.lang package since jdk 1.0. Runnable is a FunctionalInterface


package java.lang;

@FunctionalInterface
public interface Runnable {
    /**
     * Runs this operation.
     */
    void run();
}


2. By implementing a Runnable Interface.
   Thread is a class that implements Runnable and Runnable contains a method known as the run() method.
   Instead of extending a thread, we can also implement it through an interface called Runnable.

   This is the best approach to create a thread as it supports Multiple Inheritance with Interfaces.
   To create a thread using Runnable Interface:
   1. Create a class. Make it a child of Runnable
   2. Override run()
   3. Convert Runnable type to Thread type(by using overloaded cinstructor of Thread class)
   4. Invoke start()
   
In the Runnable Interface, start() is not present.
We cannot create a thread object by using a class name which is implemented with Runnable.
Thread class has many constructors, one of them accepts Runnable object as a parameter.
So, we need to create a runnable reference using class name as an object.
Then we need to pass this runnable object inside the Thread constructor and create a thread object.
After creating a thread object, we can call the start() and the execution.

package Snippets;

public class ThreadA1 implements  Runnable {

	@Override
	public void run() {
		for(int i=0;i<5;i++) {
			System.out.println("Multi threading 1");
		}
	}
	
}

package Snippets;

public class ThreadB1 implements Runnable{

	@Override
	public void run() {
		for(int i=0;i<5;i++) {
			System.out.println("Multi threading 2");
		}
		
	}

}
package Snippets;

public class TestAB1 {
public static void main(String[] args) {
	ThreadA1 a=new ThreadA1();
	ThreadB1 b=new ThreadB1();
	Thread t1=new Thread(a);
	Thread t2=new Thread(b);
	t1.start();
	t2.start();
}
}
Output:
Multi threading 1
Multi threading 1
Multi threading 2
Multi threading 2
Multi threading 2
Multi threading 2
Multi threading 2
Multi threading 1
Multi threading 1
Multi threading 1

Methods in Thread class:
1.currentThread(): returns a reference to the currently executing thread object. It is a static(). present in Thread class.
 /**
     * Returns the Thread object for the current thread.
     * @return  the current thread
     */
    @IntrinsicCandidate
    public static native Thread currentThread();

    
package Snippets;

public class TestAB1 {
public static void main(String[] args) {
	
	ThreadA c=new ThreadA();
	Thread t2=new Thread(c);

	System.out.println(t2.currentThread().toString());
	
}
}

Output:
Thread[#1,main,5,main]


2. yeild():
   It is a static native(). Its return type is void. native() are nothing but the implementations are taken from OS.
   pauses the thread and gives chance to other threads if the priority of other threads are high.
   If the priority of other threads are low or if there are no theads in the waiting state, then the same thread continuous its execution.
   If multiple threads are waiting with the same priority then, the order depends on the Thread Scheduler.

package Snippets;

public class ThreadA extends Thread{
	public void run() {
		for (int i = 1; i <= 5; i++) {
		
			System.out.println("Thread A");
		}
	}
}

 
package Snippets;

public class ThreadA1 implements  Runnable {

	@Override
	public void run() {
		for(int i=0;i<5;i++) {
			System.out.println("Multi threading 1");
			Thread.yield();
		}
	}
	
}


package Snippets;

public class ThreadB1 implements Runnable{

	@Override
	public void run() {
		for(int i=0;i<5;i++) {
			System.out.println("Multi threading 2");
			Thread.yield();
		}
		
	}

}

   package Snippets;

public class TestAB1 {
public static void main(String[] args) {
	ThreadA1 a=new ThreadA1();
	ThreadB1 b=new ThreadB1();
	ThreadA c=new ThreadA();
	Thread t2=new Thread(c);
	Thread t=new Thread(a);
	Thread t1=new Thread(b);
	t.start();
	t1.start();
	t2.start();
	
	t1.yield();

	Thread mt=t.currentThread();
	System.out.println(mt);

}
}

Output:
Multi threading 1
Thread A
Thread A
Thread A
Thread A
Thread A
Multi threading 2
Thread[#1,main,5,main]
Multi threading 1
Multi threading 2
Multi threading 1
Multi threading 2
Multi threading 1
Multi threading 2
Multi threading 1
Multi threading 2










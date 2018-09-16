---
layout: single
title:  "Notes on Thread Safety and race conditions"
date:   2018-06-08
categories: 
---


<b>What's thread safety?</b>

* Mechanisms and Methods to guarantee that parts of a programm, which is divided into many threads run corectly and without any unexpected side effects.
* Scheduling and Interleaving of threads shouldn't make a difference, and the threads can complete their work without errors and with the expected behaviour.

<h3>Race Conditions</h3> 

* The result of an operation depends on the timing and order of events in a programm
* Special case is the <b>Data Race</b> where multiple parallel threads want access to a shared variable at the same time which leads to unxpected results

<b>Types of Race Conditions</b>


* Read-Modify-Write - parallel running threads change the value of a shared variable based on the previous value of the same variable.
For example: 

```java    
    public class Main {

	private int number;


	private void incrementNumber() { // synchronize the method
		number++;

	}

	private int getNumber() {
		return number;

	}

	public static void main(String[] args) throws InterruptedException {
		final Main unsafe = new Main();

		for (int i = 0; i < 1000; i++) {

			new Thread(new Runnable() {

				@Override
				public void run() {
					try {
						Thread.sleep((int)(Math.random()*100));
					} catch (Exception e) {}
						unsafe.incrementNumber();

					
				}
			}, "T" + i).start();

		}
		Thread.sleep(1000);
		System.out.println("Final number should be 1000 : " + unsafe.getNumber());
	}

    }

```
So the expected number at the end should be 1000, but with every running the end result will be different in terms of value(eg. 996,998...) because the threads read the same value twice and then increment the same initial value.


* Check-Then-Act - concurent threads proof the condition of a shared variable and the change the value based on the initial proof 

```java

   public class CheckThenAct {

	private int number;

	//Semaphore s = new Semaphore(1);

	private void changeNumber() {

		//s.accuire(); to lock the critical section
		if (number == 0) {
			System.out.println(Thread.currentThread().getName() + " changed!");
			number = -1;

		} else {
			System.out.println(Thread.currentThread().getName() + " unchanged!");
		}

		//s.release(); to unlock the section
	}

	public static void main(String[] args) {

		final CheckThenAct unsafe = new CheckThenAct();

		for (int i = 0; i < 1000; i++) {
			new Thread(new Runnable() {

				@Override
				public void run() {
					unsafe.changeNumber();

				}
			}, "T" + i).start();

		}

	}

}
```

So, here the expected result should be that only the first thread should change the value and the others will just read it, but we get multiple changed through the course. 


<h2>The solution</h2>
1. identify the critical section. 
(A critical section is a place where multiple threads have access. Let's say for example  a method that changes a shared variable can be accessed by a lot of threads at the same time , which leads to inconsistent results. So we have to ensure thread safety by identifying the exact spots where threads intervene.) 
2. The result of a critical section should be viewed as an unseparable atomic variable that has to be protected from outside threads. For this we can use monitors and semaphores.
	* Monitors build the protected section of an object with the word <b>synchronized</b>

	```java
		private synchronized void changeNumber() { // to lock a method

		synchronized(/* the object to be protected */){}

	```

	* Semaphores use the Semaphore objects like this 


	```java
		Semaphore s = new Semaphore(/* how many threads are allowed */);
		s.accuire():// to lock the section;
		s.release(); // to unlock it 
	```
Both methods are used to seal off a section, a method or an object so only one or more allowed threads can work with the data at a time. 
			






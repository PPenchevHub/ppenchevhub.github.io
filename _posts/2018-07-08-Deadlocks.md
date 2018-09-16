---
layout: single
title:  "Notes on Deadlocks"
date:   2018-07-08
categories: 
---

Deadlocks are caused by multiple locked critical sections, to which threads are waiting to gain access.

* A special case of deadlock is the livelock, which is caused by multiple Threads constantly changing states but unable to reach completion.

<ul><b>Conditions for a deadlock</b>
<li>Mutual exclusion - there is unleast one critical section, which cannot be used by multiple threads at the same time</li>
<li>Hold and Wait - A thread should have locked unleast one critical section before it can wait for a second one, which is locked by another thread.</li>
<li>Interrupting - A critical section can be unlocked only from the thread that is working inside it , and cannot be forcefuly unlocked by another thread.</li>
<li>Circular wait - A minimum of two threads are holding critical sections and both are waiting for each others section to be unlocked.</li>
</ul>

Some ways to solve the deadlock problem are. : 

* Do not use nested critical sections - one thread should hold the lock olny to one section.
* If nested critical sections are unavoidable make a specific, consistent order of entry for the threads.
* Keep the critical sectios as small as possible -  split synchronized methods into blocks and if possible split them into smaller blocks too.
* Try to break one of the four conditions of the deadlock.

A simple Deadlock for example would be: 

```java 


    public class DeadlockSimple {

	public static Object lock1 = new Object();
	public static Object lock2 = new Object();

	public static void main(String[] args) {

		new ThreadDemo().start();
		new ThreadDemo2().start();

	}
    }
    class ThreadDemo extends Thread {
	public void run() {
		synchronized (DeadlockSimple.lock1) {

			System.out.println(Thread.currentThread().getName() + " is holding lock1!");

			try {
				Thread.sleep(10);
			} catch (Exception e) {
			}

			System.out.println(Thread.currentThread().getName() + " is waiting for lock2!");
			synchronized (DeadlockSimple.lock2) {
				System.out.println(Thread.currentThread().getName() + " is holding lock1 && lock2!");

			}
		}
	}
    }

    class ThreadDemo2 extends Thread {
	public void run() {
		synchronized (DeadlockSimple.lock2) {
			System.out.println(Thread.currentThread().getName() + " is holding lock2!");

			try {
				Thread.sleep(10);
			} catch (Exception e) {
			}

			System.out.println(Thread.currentThread().getName() + " is waiting for lock1!");
			synchronized (DeadlockSimple.lock1) {
				System.out.println(Thread.currentThread().getName() + " is holding lock1 && lock2!");

			}
		}
	}
    }

``` 

The result of this is the first thread waiting for the second to release the lock and the second thread is waiting for the first one.

so smt like this :

Thread-0 is holding lock1!

Thread-1 is holding lock2!

Thread-0 is waiting for lock2!

Thread-1 is waiting for lock1!

* So one way to break the circular hold here is to switch order of the locks on either of the threads. So lets say ThreadDemo will try to get lock2 instead of lock1 first, thus breaking the cycle.





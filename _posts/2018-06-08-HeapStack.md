---
layout: single
title:  "Notes on Heap and Stack"
date:   2018-05-07
categories: 
---

What are those things?
<img src="https://steemitimages.com/0x0/https://i.stack.imgur.com/HOY4C.png"/>
<h4>https://steemit.com/programming/@drifter1/programming-assembly-heap-memory-allocation</h4>


<h2><center>Heap vs Stack</center></h2>
1 A <b>Heap</b> is the memory address place assigned to a thread, where it can store all local and temporary variables.
* Follows the LIFO(Last In First Out) principle
* Grows and shrinks in size with the program
* Doesn't require any kind of garbage collection

* A <b>Stack</b> is the memory address place assigned to a process and all its threads, to store objects, classes and instance variables.
* Pointers are used for refferencing
* A garbage collector <b>MUST</b> be enforced
* Slow access time 



---
layout: single
title:  "Notes on concurrency, multithreading and threads"
date:   2018-05-07
categories: 
---


<p>Concurrency VS Parallelism
<ol>
<li>Tasks are called <b>concurrent</b> when they can run completely independetly from each other. This includes Time-Slicing, Interleaving or parallel to each other </li>
<li>When tasks run independetly from each other at the exact same time, we can say they run <b>parallel</b> to eachother.This excludes time slicing then. </li>
</ol>

<h2>Types of parallelism</h2>

<ul>
<li><h3>Bit-Level Parallelism</h3>
- increase in the bandwidth/word length of the CPU, which leads to a decrease in the number of separate instructions that the CPU must run.
</li>

<li><h3> Instruction-Level Parallelism</h3>
- CPUs can run mutliple independent tasks at the same time 
- the output from a task can be the input for another one ... aka Pipelining
</li>

<li><h3>Data Parallelism</h3>
- Data can be separated, so different cores can work on parts of the data at the same time 
</li>

<li><h3>Task-Level Parallelism</h3>
- Tasks can be run in Processes or Threads on different CPU-cores.
</li>
</ul>

<h2>Process VS Thread </h2>
<ul>
<li>Processes run only in their own memory address space which mean they run independetly and are completely isolated from other processes.
So the key components are <b>memory address space, ressources and a processcontext</b>.</li>
<li>Threads are parallel running activities withing a process, and the assignment of resources to a thread is not deterministic, which means that the order of completion cannot be predicted.</li>
</ul>

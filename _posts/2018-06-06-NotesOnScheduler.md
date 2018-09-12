---
layout: single
title:  "Notes on scheduler and scheduling"
date:   2018-05-07
categories: 
---

<h3> What's a scheduler? </h3>
Scheduling is a method of assigning resourcess to a thread/task to complete some work. And all of this is carried by the scheduler, which is responsible for the prioritization and completion of a given job.


<h4>The main purposes of a scheduler are :</h4>
<ol> 
<li><b>Fairness</b> - ensures that no thread should wait for a long time, without a legitimate reason, when other threads are getting higher priority.</li>
<li><b>Resource starvation </b>- number of finished threads in a time interval should be maximized so a greater efficiency of the CPU can be achieved.</li>
<li><b>Time to answer</b> - The waiting time for the user with Threads which require user interaction should be minimized as much as possible.</li>
</ol>

<h3>Scheduling Strategies</h3>
Those are algorhythms designed to achieve maximum resource efficiency with minimal answertime. 
Different situations will require ofc different methods but the some of the main supergroups that divide the scheduling algorhythms are 

1. Priority Scheduling - a priority factor is assigned to every thread and the scheduler can control the execution based on that factor 
2. Preemptive Scheduling - a running thread is interrupted every time another thread with a higher priority comes and has a ready state.

Another examples are <b> Time slicing, FIFO, LIFO, Round Robyn...</b>

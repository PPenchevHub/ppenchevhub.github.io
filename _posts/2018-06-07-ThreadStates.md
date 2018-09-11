---
layout: single
title:  "Thread States and lifecycle"
date:   2018-06-07
categories: 
---

Every thread has it's own lifecycle going through different states before it dies or is terminated.

<img src="https://www.uml-diagrams.org/examples/state-machine-example-java-6-thread-states.png"/>
<h5>https://www.uml-diagrams.org/examples/java-6-thread-state-machine-diagram-example.html</h5>

<ul>
<li><h3>New</h3></li>
- A thread is created but not started.
<li><h3>Runnable</h3></li>
-A thread is ready to be started but is waiting or blocked by something
<li><h3>Ready</h3></li>
-A thread can be run but no CPU power has been assigned to it.
<li><h3>Running</h3></li>
-well .. the thread is running.
<li><h3>Timed waiting</h3></li>
- the thread is suspended for a specific time. For example in java by wait(...ms); or sleep(...ms).
<li><h3>Waiting</h3></li>
- same but waiting until its woken up with for example notify().
<li><h3>Blocked</h3></li>
- it's waiting for ressources 
<li><h3>Terminated</h3></li>
- The thread has completed everything or is shutdown().
</ul>



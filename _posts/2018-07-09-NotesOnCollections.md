---
layout: single
title:  "Notes on Collections"
date:   2018-07-09
categories: 
---


Collections are a group of objects , which are connected in a complex, dynamic datastructure. No primitive datatypes are allowed and the size can be changed during runtime.
They all implement the Iterable and Collection interfaces. Which are then split into Set, List and Queue interfaces (Map is a different story) 
Couple of examples are: 

* List - elements are ordered from the user, duplicates are allowed and everything can be reached via indexes.
* Arraylist - Dynamic size, fast reading time, but adding and deleting are slow, because all the positions of the elements have to be adjusted.
* LinkedList - bidirectional chaining of elements, slow reading time, because the list must always be read untill the end, but fast adding and deleting 
* Set - unsorted list and no duplicates possible, all the elements are immutable.
* HashSet - saved in a Hashtable, based on the hash of the elements, fast adding, elements can be reached via an iterator, but the order is unpredictable.
* LinkedHashSet - bidirectional chaining of the elements in the hashtable, order of the elements is the same as the order of adding.
* TreeSet - sorted in a binary Tree, only elements from the same type that can be compared and it MUST implement the Comparable interface
* Map - a tuple of keys and values, every key is unique


BUT all collections without vector and Hashtable are not threadsafe, so the solution to this are wrappers(internal monitors) like this

	Collections.synchronizedList(new ...);

or Concurrent Collections with the following methods: 

* CopyOnWrite - where elements are saved in an immutable array, but if we want to modify any part of it we must create a new aray and then replace the initial one with it, and this makes reading fast but adding or deleting very slow.(ex. CopyOnWriteArrayList or CopyOnWriteArraySet) 
* Compare and swap - like atomic variables. If we want to modify an element, we have to make a copy of it then change it and replace the itinial element. But before the replacement it should be checked if the element hasn't already been changed. If yes replace with the changed original value.(ex. ConcurrentLinkedQueue or ConcurrentSkipList)
* Locks - synchronize with monitors, but not the whole collection, but just parts of it like the end or the beginning(ex. BlockingQueue)  

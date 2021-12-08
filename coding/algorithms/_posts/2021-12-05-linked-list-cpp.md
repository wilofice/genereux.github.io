---
layout: post
title: Linked list in C++
image:
  path:    /assets/img/posts/tutorials/data-structure-linked-list.png
comments: true
---

Linked list in C++

To store a list of items, we usually use an array. This implementation is the most intuitive but it is not so efficient in terms of memory, time and usage.

In this article, we are going to learn how to implement a linked list. It is an implementation that allocates memory to data item by data item as they are added in the list. It also come with the advantages that the insertion and deletion operations are very simple. 

#### 1) Creating a linked list

A linked list is a data structure composed of nodes, each node holds some information and a pointer to another node in the list. When a node has only a link to its successor, the list is called a singly linked list . But a node has a link to its successor and also a link to its predecessor, it is called a doubly linked list.

Only one variable is needed to access all the elements of the list and the last element of the list is the null pointer.

In our implementation below, we use two classes: 
- *Node* to represent each node of the list
- *LinkedList* to manage the list and modify it

The class *Node* has data member :
- *info* an integer containing the information
- *next* a pointer to the next node

The class *LinkedList* has two data member:
- *head* is a pointer to first node of the list
- *tail* is a pointer to the last node of the list


~~~c++
#ifndef INT_LINKED_LIST
#define INT_LINKED_LIST

class Node {
public:
	int info;
	Node *next;
	
	Node(int val, Node *p = 0)
	{
		info = val;
		next = p;
	}
};

class LinkedList {
private:
	Node *head, *tail;
public:
	LinkedList() {
		tail = head = 0;
	}
	~LinkedList();
	int isEmpty() {
		return head == 0;
	}
	
	void addToHead(int);
	void addToTail(int);
	int deleteFromHead();
	int deleteFromTail();
	void deleteNode(int);
	bool isInList(int) const;
};

#endif
~~~

This class also defines members that help to manipulate the list and do the basic operations of insertion, deletion over the list.

#### 2) Insertion at the front of the list

~~~c++
#include <iostream>
#include "linkedlist.h"

void LinkedList::addToHead(int info){
	head = new Node(info, head);
	if(tail = 0) tail = head;
}
~~~

#### 3) Insertion at the first element of the list
~~~c++
#include <iostream>
#include "linkedlist.h"

void LinkedList::addToTail(int info){
	if(tail == 0){
		addToHead(info);
	} 
	tail->next = new Node(info);
	tail = tail->next;
}
~~~

#### 4) Deletion of the head of the list
~~~c++
#include <iostream>
#include "linkedlist.h"

int LinkedList::deleteFromHead() {
	Node *tmp = head;
	int info = head->info;
	if(head == tail) {
		head = tail = 0;	
	} else {
		head = head->next;
	}
	delete tmp;
	return info;
}
~~~


#### 5) Deletion of the last element of the list
~~~c++
#include <iostream>
#include "linkedlist.h"

int LinkedList::deleteFromTail() {
	Node *tmp = tail;
	int info = tmp->info;
	if(head == tail){
		head = tail = 0;
		delete tmp;
	} else {
		Node *j;
		for(j = head; j->next != tail; j = j->next);
		tail = j;
		tail->next = 0;
		delete tmp;
	}
	delete tmp;
	return info;
}
~~~


#### 6) Deletion of any element of the list
~~~c++
#include <iostream>
#include "linkedlist.h"

void LinkedList::deleteNode(int val){
	if(head == 0) return;
	
	if(head->info == val){
		Node *tmp = head->next;
		delete head;
		head = tmp;
		return;
	}
	Node *j;
	Node *previous;
	for(j = head; j != 0 && j->info != val; j = j->next){
		previous = j;
	}
	if(j == 0){
		return;
	}
	previous->next = j->next;
	if(j == tail) tail = previous;
	delete j;
}
~~~


#### 7) Deletion of the last element of the list
~~~c++
#include <iostream>
#include "linkedlist.h"

int LinkedList::deleteFromTail() {
	Node *tmp = tail;
	int info = tmp->info;
	if(head == tail){
		head = tail = 0;
		delete tmp;
	} else {
		Node *j;
		for(j = head; j->next != tail; j = j->next);
		tail = j;
		tail->next = 0;
		delete tmp;
	}
	delete tmp;
	return info;
}
~~~


#### 8) Check if an element is in the list
~~~c++
#include <iostream>
#include "linkedlist.h"

bool LinkedList::isInList(int val) const {
	Node *i;
	for(i = head; i != 0 && i->info != val; i = i->next);
	return i != 0;
}
~~~
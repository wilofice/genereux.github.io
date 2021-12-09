---
layout: post
title: Linked list in C++
image:
  path:    /assets/img/posts/tutorials/data-structure-linked-list.png
comments: true
tags: [data structures, linked lists]
---

To store a list of items, we usually use an array. This implementation is the most intuitive but it is not so efficient in terms of memory, time and usage.

In this article, we are going to learn how to implement a linked list. It is an implementation that allocates memory to data item by data item as they are added in the list. It also come with the advantages that the insertion and deletion operations are very simple. 

**Before continuing, I assume that you have basic undestanding of C++ classes, methods and memory allocation notions.**
**If you feel more comfortable reading in the dark, you can set the dark mode by clicking on the button besides the menu button*

1. toc
{:toc}

## Creating a linked list

A linked list is a data structure composed of nodes, each node holds some information and a pointer to another node in the list. When a node has only a link to its successor, the list is called a *singly linked list*. But a node has a link to its successor and also a link to its predecessor, it is called a *doubly linked list*.

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
// file: "linkedlist.h"
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

A basic implementation for a singly linked list
{:.figcaption}
~~~


This class also defines members that help  manipulating the list and do the basic operations of insertion, deletion over the list.

## Insertion at the beginning of a linked list

Inserting a node at the beginning of a list is performed in the following steps:
- A new node is created. The value of *info* is initialized the one provided and its *next* member is set to be equal to head. Indeed, the new node must be at the front of the list so it is logical that its *next* member holds a pointer to the current head of the list
- Since the new node is the new head of the list, the *head* data member must be updated to reflect that
- Finally we check that if *tail* has not been initialized so far. Indeed, if tail is *null*, it means that *head* is the only element of the list. That means it is also the last element of the list. Then *tail* must be equal to *head*

~~~c++
// file: "linkedlist.cpp"
#include <iostream>
#include "linkedlist.h"

void LinkedList::addToHead(int info){
    head = new Node(info, head);
    if(tail = 0) tail = head;
}
~~~

## Insertion at the end of a linked list

Inserted at the end of a linked list is performed by taking the following actions: 
- We check if *tail* is null then info is the first element that is being added to the list. So we simply call *addToHead* to add the new elememnt to the head of the linked list and that's all.
- If it is not the case, we create a new node and initialize it's *info* data member.
- The new node must be the last element of the list so we set the *next* data member of the current *tail* property.
- The new node added has become the last element of list, then we must update *tail* to reflect that.



~~~c++
// file: "linkedlist.cpp"
#include <iostream>
#include "linkedlist.h"

void LinkedList::addToTail(int info){
    if(tail == 0){
        addToHead(info);
        return;
    }
    tail->next = new Node(info);
    tail = tail->next;
}
~~~

## Deletion of the first element of a linked list

Deleting of the dead of a linked list:
- First we check if the list has only two nodes. That would mean that *head* is equal to *tail*
- In that case, head and tail is set to *null* 
- Otherwise, we save *head* in a temporary variable so that we can deallocate its memory space (this is a C++ particularity). Then *head* is reset so that what was the second node becomes the first.
- Then we delete the allocated memory space the previous head of the list and return the value stored in that node.

~~~c++
// file: "linkedlist.cpp"
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


## Deletion of the last element of the list

Deleting the last element of a linked list is performed with the following steps:
- We save in a temporary variable, *tmp*  the value of the current tail of the list. 
- We check if the linked list has only one element by checking if *head* is equal to *tail*. In that case, we delete *tmp* and deallocate its memory
- Otherwise, we iterate over the list from beginning with the *head* until we reach the current node before the last element. 
- *tail* is updated to become it's previous element and its *next* member must is updated to reflect that there is no element after *tail*


~~~c++
// file: "linkedlist.cpp"
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


## Deletion of any element of the list

Deleting any element of the list is performed by following these septs:
- We check of course if *head* is null . In that case, no action needed. 
- Otherwise we look for the element preceding the one we want to delete.
- Before we check if the element to delete is at the head of the list, then  *head* becomes the second element of the list (and we make sure we properly delete the element from the memory)
- If that's not the case, we iterate over each element of the linked list until we stop before the element we want to delete : that is *previous* 
- Then we update our linked list variables *tail* and *head* so that our list remains consistant

~~~c++
// file: "linkedlist.cpp"
#include <iostream>
#include "linkedlist.h"

void LinkedList::deleteNode(int val){
    if(head == 0) return;

    if(head->info == val){
        Node *tmp = head->next;
        delete head;
        head = tmp;
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

## Check if an element is in the list

To check if a value is in the linked list, we iterate over each element to check if the value exists. The value does not exist in the list if we iterate over the list until we hit the last element (*null*)

~~~c++
// file: "linkedlist.cpp"
#include <iostream>
#include "linkedlist.h"

bool LinkedList::isInList(int val) const {
    Node *i;
    for(i = head; i != 0 && i->info != val; i = i->next);
    return i != 0;
}
~~~

In a next article, we are going to see in details what is the time complexity of each operation. We will also discuss about a case study of linked list real applications. 
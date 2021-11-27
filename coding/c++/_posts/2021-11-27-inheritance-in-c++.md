---
layout: post
title: Inheritance in c++
image:
  path:    /assets/img/posts/tutorials/cpp_inheritance.png
comments: true
---


Inheritance

In C++, it is possible to inherit attributes and methodes from one class to another.
The inheritance concept can be grouped in two notions:

- derived class (child) : class that inherits from another class
- base class (parent): the being inherited from

To inherit from a class, use the symbol : .

In the example below, the Airbus class (child) inherits from the attributes and methods from the Airbus class (parent).


~~~c++
#include <iostream>
using namespace std;
// Base class
class Aircraft {
  public:
    string name = "aircraft";
    void fly() {
      cout << "I am an aircraft and I am flying \n" ;
    }
};

// Derived class
class Airbus: public Aircraft {
  public:
    string model = "Airbus";
};

int main() {
  Airbus myAirbus;
  myAirbus.fly();
  cout << myAirbus.name + " " + myAirbus.model;
  return 0;
} 
~~~

Inheritance : the class Airbus inherits from the class Aircraft
{:.figcaption}

![Full-width image](/assets/img/posts/tutorials/inheritance.png){:.lead width="668" height="143" loading="lazy"}

Execution of the code
{:.figcaption}


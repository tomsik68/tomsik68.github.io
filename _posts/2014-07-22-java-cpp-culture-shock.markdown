---
layout: post
title:  "C++ for Java Programmers = Culture shock!"
date:   2014-07-22 15:15
categories: java cpp
---

I've been trying to learn C++ for a while, but I didn't succeed. I'm trying it again and I've got some experiences which other people may find useful.
These tips will probably be useful especially to java developers. I can't say I'll be 100% right, I know there are people who know this better, so I'll just try to list some difficulties I experience as java programmer.
Note: Before reading, I recommend you have basic knowledge of C++ or you'll get a headache :)

## 1. Compilation system, Build environment

Compilation & build system of C++ is very different than java's. You have all kinds of tools to help you with compilation.
I'd like to point out CMake, which is simple and cross-platform. It generates a Makefile, so you also need make to use it.
Adding libraries is much harder than in java. All you need to do in java is to specify a JAR file and you're good to go.
In C++, you need to specify a "search path", where compiler will search for header files and a static or dynamic linking library. 
Which leads me to #2

## 2. Separating declaration & implementation

Declaration is put in header files (.h or .hpp), while implementation is put in .c or .cpp files depending on which language you want to use(you can also combine them!). 

## 3. Multiple inheritance

In java, one class may only have one superclass. In C++, you can inherit multiple classes, which creates confusion for java programmers.

## 4. Superclass and Childclass are not compatible, only pointers

Consider this example:
We have class Animal and class Dog. Dog extends Animal. Let's say we have a method which takes Animal as an argument:
		
	void doSomething(Animal animal);
	
C++ won't allow you to pass myDog of type Dog to this method. To achieve this, you need to use a pointer. Pointers of child classes are compatible with pointers of super classes.

	void doSomething(Animal* animal);

To pass myDog of type Dog into this method, call it like this:

	doSomething(&myDog);
	
&myDog produces pointer to myDog, which is compatible with pointer to animal.

## 5. Nothing is abstract, something is virtual 

Abstract keyword is used very often in java. In C++, there's no abstract keyword. There's just virtual. However, there's a big difference between these two keywords: abstract doesn't require you to provide base implementation, while virtual requires you to do that.

You can't just override whatever you want, you have to specify function as virtual to be able to do it.

## 6. De-structor?

Except for creating object, in C++ you also need to remove it. Java does this automatically, so I usually forget about this :)

## 7. 3 different ways to refer to members  `::` `->` `.`

It's not that difficult, I just didn't get comfortable with this yet. This is how it works:

To refer to a static member, you use `::`

To refer to a regular member, you use `.`

If you have a pointer to object instead of an object, you use `->`.

## 8. There are more ways to call a constructor, objects declared are directly created.

In java, this declaration causes the variable to have null value:

	Object myObject;
	
In C++, it doesn't work that way. Rather than that, it's a way to call the default constructor.

There's also the `new` keyword in C++. As you probably expected, it works differently. It produces pointer instead of object:

	Object* myObject = new Object();
	
Btw in C++ there's no "Object" class, but you don't really need that. To refer to whatever type, just use `void*`. It's a pointer to unknown type.

## 9. Variables, Functions WITHOUT an Object!

In C++, you can define a variable or a function without being in an object. This comes from its older brother, C, which wasn't sadly object-oriented. You can of course work fully object-oriented except for main.cpp which usually contains only int main();

## 10. Strings may be confusing

std::string is really awesome. However, some libraries introduce their own types of strings, which may or may not be difficult to convert to std::string.

## 11. Passing arguments by whatever you want

Java passes arguments which are Objects by reference. C++ normally passes all arguments by value, unless you specify a `*` before variable name like this:

	void myVoid(Object *myObject);

---
I hope this was useful to someone at least :) 

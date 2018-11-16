---
layout: post
title:  "Memories about pointers, or was it pointers about memory?"
categories: programming
excerpt_separator: <!--more-->
---
[garbage]:https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)
[machinecode]:https://en.wikipedia.org/wiki/Machine_code
[blog_post]:/programming/2018/11/11/Constructing-and-destructing.html
[pointersInLanguages]:https://en.wikipedia.org/wiki/Pointer_(computer_programming)#Support_in_various_programming_languages
[wikipedia]:https://en.wikipedia.org/wiki/Pointer_(computer_programming)
[smartpointers]:https://en.wikipedia.org/wiki/Smart_pointer
[cprogramming]:https://www.cprogramming.com/tutorial/lesson6.html
[lecture]:http://www.cs.uwm.edu/classes/cs315/Bacon/Lecture/HTML/ch10s04.html
[geekforgeeks]:https://www.geeksforgeeks.org/memory-layout-of-c-program/
[tech]:https://cpp.tech-academy.co.uk/memory-layout/
[dataSegmentInWiki]:https://en.wikipedia.org/wiki/Data_segment
[isocpp]:https://isocpp.org/wiki/faq/freestore-mgmt

I’m dwelling deeper and deeper to territory that was previously pretty mysterious to me and made me sometimes wonder what was going on with the program. Most of time when doing exercises that needed to be solved using C++ pointers and memory management I was mostly trying to brute force myself through and Google the compiler errors as they came, without truly understanding what was going on.<!--more--> Like I said on my [previous][previous] post:
>When I was younger I learned programming by reading about something superficially (ie. about object oriented programming) and then moving on the programming part without truly having comprehension of the subject matter.

Because of my past experiences I was better prepared this time and when the time was to start learning about pointers and memory in C++ I wanted to make sure that before I move on I have understood what is going on under the hood when programs use pointers and memory allocation in general. Usually this is the point where many of the would be C++ programmers are turn off by the language or programming in whole. Pointers and memory allocation can be pretty off putting, because unlike, say Java and Python, where this kind of thing are done automatically, C++ provides very little automation on its own. This automation, so called [garbage collection][garbage], is still possible with C++ like said in the Wikipedia page:
>Some languages, like Ada, Modula-3, and C++/CLI, allow both garbage collection and manual memory management to co-exist in the same application by using separate heaps for collected and manually managed objects. 

I knew from the past that this is can be a very huge subject so it made me wonder where I should start, so that I could begin to grasp it more. Well there is no better place to start than from the beginning so I went ahead and collected as much as material about C++ and memory management I could possibly find and here are the findings and things that I think are most important to know.

C++ Memory Layout
==================

C++ programming language shares the same memory layout with the C-language, so when information about memory layout of C++ is searched, information about both languages tend to pop up. The memory layout consist of six data segments and they are illustrated in the picture below. The explanation may use words that are not used in this blog before, but don’t worry; next section contains information about operators, such as new and *-pointer, which I will explain in greater detail in the next header. They play a big part in C++, because they directly increase or decrease amount of used memory or point to memory addresses.

![Data segments](/assets/data_segments.svg)

Described here from the top to bottom are what each of the the numbered data segments mean:
1. Stack is used to store local variables (for example integer declared in the main of the program, or string declared in a function member) and passing arguments to functions, along with return address of the next instruction to be executed when the function call is over. It works on **last-in-first-out** or called **LIFO**-basis (think of it as a stack of plates, you can put one on top and can only take one out of the top). Stack grows downward towards lowest address. It should be noted that stack is often limited to 1 MB or lower, depending on the system and/or compiler settings.
2. The area between heap and stack is called unallocated segment. It is a free area that is available to be utilised for growth of heap or stack segments.
3. Heap, which is also known as free store for memory allocation and is the segment where dynamic memory allocation takes place *most of the time*, when everything is going as they should be. As pictured, it grows upwards to highest address. Heap can grow approximately as large as available physical memory on the device where the program is being run on. In C++ heap is managed by new- and delete-keyword. It should be also noted that heap segment is shared by all threads, shared libraries, and dynamically loaded modules.
4. Uninitialized data segment, also known as bss(block started by symbol)-segment. Data in this segment is initialized by the kernel to value 0 or NULL, before the program starts executing. This segment contains all global and static variables, that are initialized to zero or do not have initialization written in the source code. For example variable declared static int i; or a global variable declared int j; would be stored in the bss segment.
5. Initialized data segment contains data, that has already been initialized in the source code, which means it contains both the global and static variables. This segment, unlike text segment below it, is not **read only** because variables in a program need to be able to change during runtime (hence the name *variable*). For example when user inputs data and it is then stored to variable, this variable would be stored in initialized **read-write** area. However this segment also has its own **read only** section and it is needed for instance, when a global statements like const char* string = “happy coding” is called. This line of code makes the string “happy coding” to be stored in initialized read-only area while the *-pointer is stored in initialized read-write area. As can be seen data is stored to this segments own *segments* depending if the variable is something that should be changed later on the runtime.
6. Text segment or code segment and it contains the compiled [Machine code][machinecode], meaning the instructions in ones and zeroes so that the computer's central processing unit understands the code. In short it tells the story of what the program does so that computer can run it. This memory segment is often in read only state to stop it being overwritten by stack or heap segments, which could be a source of errors or crashes.

As heap can be as large as available memory the system, using heaps dynamic memory possibilities makes **much bigger** projects conceivable than what only the stack has to offer. That couple with the fact that there is no way to pass pointers or references to objects on the stack outside their scope, as the stack will get cleaned when the scope ends (i.e. at the end of a function for example), thus the object becomes unavailable to use elsewhere in the program. Objects or variables saved to heap segment carry on through the whole program until they are deleted by the program or when the program closes. In fact if objects, variables or whatever that is stored to heap isn’t deallocated at some point during runtime, it may cause memory leaks which I made [blog post][blog_post] about.


Pointers and references
==================
One of the greatest advantages of C++ over other **popular higher level programming languages** is the inclusion of pointers. While other languages, such as Java has them, they are usually handled differently (ie. through references etc. check full list of differences [here][pointersInLanguages]). So what are pointers exactly? Like the name implies they **point** at something and that something is memory addresses where another value is stored. This means that pointer can be pointed to another object of a class, variable, even an array as long as the thing that is pointing at is saved in the memory, so that there is an address to point to. To put it in real life example, thanks to [Wikipedia page][wikipedia]:
>..a page number in a book's index could be considered a pointer to the corresponding page; dereferencing such a pointer would be done by flipping to the page with the given page number and reading the text found on that page.

So what are pointers good for? When pointing to a simple integer value one could think that why just not use that same simple integer and pass it to method, or whatever that happens to be the use case. And yes that can be more efficient in most cases, but what about objects that are much bigger than say that same integer. Instead of creating a copy of that object when passing it to a member it is much more effective, performance and memory wise, to point to that memory address and pass that pointer to that same member. Example:
{% highlight cpp %}
//Creating a huge object that takes multiple kilobytes of memory:
MobilePhone NewMobilePhone;

// Creating a pointer of same class type called ptr.
MobilePhone* ptr;

//Pointing the pointer called ptr 
//to the memory address of NewMobilePhone
//& is like a @-sign, as it refers the memory address of an object.
ptr = &NewMobilePhone;

//Calling the ExampleFunction and passing the pointer to it.
ExampleFunction(ptr);
{% endhighlight %}

As stated above this example code only passes the pointer pointing at the memory address of an object. In C++ when object is passed to function the program creates a copy of the whole object (something that is defined in the language by default). This means that in example code the programs size suddenly doubles when function call is done. With pointer that doesn’t happen because pointer points to the already existing object without ever needing a copy. If we recall the example that the pointer is like a page number in an index of a book this function call could be like if when you read the book and it refers to something that has already happened but instead of saying that “when this and that happened to protagonist in the past” it tells exactly the same events **AGAIN**, thus doubling the page count with unnecessary information that the reader already knows about.

New- and delete-operators
==================
Memory layout included data segment called heap. Heap is the free store for memory allocation. This segment of data is used when C++ operator new is used on a source code. New operator can be called on almost anything and when it is used all the data is stored to heap. So how it differs from the for example variables stored stack? Normally syntax like “int a”-variable or the “char str[10]”-array are automatically allocated to the stack-memory and then deallocated at the end of their lifecycle, be it end on main part of the program or function. With the operator new, nothing is deleted until the program explicitly tells that it needs be deleted. That is when the delete-operator comes in. It deallocates memory from the heap and make whatever was called before with new-operator no longer available. Again here is an example with both new and delete, notice how pointers are also used here:
/{% highlight cpp %}
// Pointer called ptr initialized with NULL
// Then request memory for the integer variable.
int *ptr1 = NULL;
ptr1 = new int;   

// Combine declaration of pointer and request for memory
int *ptr2 = new int;

//It is also possible to do all that and initialize these by using (insert value here):
int *ptr3 = new int(25); 
float *ptr4 = new float(75.25);

//New-operator can also be used on objects
MobilePhone *MobilePhonePtr = new MobilePhone;

//Delete-operator is used on each of the pointer
delete MobilePhonePtr;
delete ptr1;
delete ptr2;
delete ptr3;
delete ptr4;
{% endhighlight %}

Example above shows how to allocate memory with new-operator and how to release, or deallocate, it with delete-operator. It is very important to always delete pointers that are pointing to variables, objects etc. that are saved on the heap since the program will not do it automatically at the end of the scope. This is one major source of memory leaks and can make programs unstable, slow and even crash at certain points. You will also notice that new-operator and pointer go hand in hand. In this case the pointer points to the newly allocated memory address. For example when source code has ptr1 = new int; amount of memory for int is allocated somewhere in the heap and the pointer is there point where exactly that is so that in can be accessed later via it. 

So there are the basics. Of course there are still tons of stuff that can be done and especially learned with this memory management. There are libraries that allow [“smarter” pointers][smartpointers] so that the new-operator isn’t needed that much, making C++ little bit more like Java with garbage collecting aspect. I will keep posting about new development when I will learn more.

Other sources, that were not linked, when writing this blog post:
* [Cprogramming site about pointers][cprogramming]
* [Jason W. Bacon Computer Science 315 Lecture Notes][lecture]
* [Geeks for geeks][geekforgeeks]
* [tech-academy][tech]
* [Wikipedia: Data Segments][dataSegmentInWiki]
* [ISOCPP][isocpp], which also provide a lot of information about memory management in general.


-sorhanp
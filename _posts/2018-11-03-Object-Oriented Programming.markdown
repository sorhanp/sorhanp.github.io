---
layout: post
title:  "Object-Oriented Programming"
categories: programming
excerpt_separator: <!--more-->
---
[geeks]: https://www.geeksforgeeks.org/basic-concepts-of-object-oriented-programming-using-c/
[ntuedu]: http://www.ntu.edu.sg/home/ehchua/programming/cpp/cp3_OOP.html
[tutpoint]: https://www.tutorialspoint.com/cplusplus/cpp_object_oriented.htm
[wikispp]: https://en.wikipedia.org/wiki/Single_responsibility_principle
[last]: /programming/2018/10/31/Out-with-the-old-in-with-the-new.html
:https://www.cprogramming.com/tutorial/lesson6.html 
:https://en.wikipedia.org/wiki/Data_segment
:http://www.cs.uwm.edu/classes/cs315/Bacon/Lecture/HTML/ch10s04.html
:https://www.geeksforgeeks.org/memory-layout-of-c-program/
:https://cpp.tech-academy.co.uk/memory-layout/


My [last][last] blog post was mostly about my change of tools and in this post I’m going to describe more closely my learning progress so far. Last time I wrote about loops, which are very important part of programming and about my new findings such as setprecision(). This time I’m mostly writing about Object-Oriented Programming, which I have been very interested since I heard about it back in the day and learned what it really meant.<!--more--> Nowadays when I try to learn something that I’m really into, I also try to search as much background information as possible so that I can form a complete understanding about it. I know that sometimes that is not possible, but with programming I think that this is really necessary. When I was younger I learned programming by reading about something superficially (ie. about object oriented programming) and then moving on the programming part without truly having comprehension of the subject matter. Usually this lead to situations where I would face a problem and then force my way through. Using this tactic usually leaves me with knowledge how to solve that particular problem, but doesn't make me truly learn anything. Managing to understand the big picture is the most important and I think that is the case with object orientation. This is why I wanted to write whole blog post about it.

What it is?
==================
Object oriented programming is based completely around data structures that contain data fields and methods. These structures are called objects, and hence the name object oriented. Everyday things that you find around you are, in fact, *objects* in programming sense also. For example the device that you are reading this post is an object, be it a mobile phone, computer, tablet, anything can be used to access web pages. For the sake of an example let say that it is a mobile phone. Each mobile phone has its attributes (data fields), like model name, size, weight, color and so on. Each mobile phone also have things one can do with it, like text messaging, browsing the Internet and so on. These things that can be done with it are methods. In programming these objects are created from a *class*. Classes are like blueprints, or guidelines, for the object, so one can go and build an object (in this case one mobile phone) from it, let's keep up with the example above and build a class mobile phone in C++.
{% highlight cpp %}
class MobilePhone {
    //Data fields also known as attributes of the phone:
    string Model;
    int ModelNumber;
    int IMEI;
    string Color;
    string OperatingSystem;
    //These are only examples, as mobile phones can have many attributes

    //Methods also known as things you can do with a phone.
    public:
    void MakePhoneCall(int NumberToCallTo);
    void OpenInternetBrowser(string NameOfBrowser);
    //Mobile phones tend to have a lot of things you can with do it.
    //Which means that there are a lot of members.
    //Let's keep it sort and keep reading how one should go
    //and create classes that are not too large.
};
{% endhighlight %}

As you can see from above example an object can have multiple data fields and even longer list of methods. This is why methods are usually separated into multiple classes like this:
![Classes](/assets/classes.svg)

As seen in the image program written in object oriented manner is made up of objects that communicate with each other. This is also called [single responsibility principle][wikispp], which *states that **every class** should have responsibility over a **single part** of the functionality*.

Why it is used?
==================

I think [this page][ntuedu] best describes the original problem with non object-oriented programming:
>A car is assembled from parts and components, such as chassis, doors, engine, wheels, brake, and transmission. The components are reusable, e.g., a wheel can be used in many cars (of the same specifications). Hardware, such as computers and cars, are assembled from parts, which are reusable components.
How about software?  Can you "assemble" a software application by picking a routine here, a routine there, and expect the program to run?  The answer is obviously no!  Unlike hardware, it is very difficult to "assemble" an application from software components.  Since the advent of computer 60 years ago, we have written tons and tons of programs.  However, for each new application, we have to re-invent the wheels and write the program from scratch.

Object oriented programming is designed to alleviate problem of having to write software again and again from the beginning when new project is started. In previous picture there were multiple classes like BrowseInternet(); represented as boxes. These boxes can be moved from the original program to the new program no more re-inventing the wheels. Programs developed using object orientation are also easier to design because rather than thinking how would programming languages variables, loops etc. solve this problem programmers can perceive and work out the problem with *high-level concepts and abstractions* with the help of classes. Best way to describe abstraction is to compare classes and objects to variables and named storages created from them.
{% highlight cpp %}
    string ExampleVariable = “Name of phone”;
    //string variable with storage name “ExampleVariable” that holds one value.
    MobilePhone ExampleMobilePhone(“Name of phone”, IMEI, etc…) ;
    /*Object ExampleMobilePhone is created from previously created
    class MobilePhone and it contains multiple values.
    Later this phone can do different methods,
    such as MakePhoneCall(number); to call someone.*/
{% endhighlight %}
As seen in this example abstraction provides only the needed information and hiding their background details. This way software is also easier to maintain, such as fix problems users may find later of the programs lifecycle, because it is easier to understand what makes the program work.
So there you have it, object oriented programming in a nutshell. I highly recommend that you check out these sources I used to read more about it if you are interested. I think I will return later and revisit this subject when I have more understanding so that I may even better and clearer explanation of the benefits that it offers.

Sources used when writing this blog post:
* [Geeks for geeks][geeks]
* [yet another insignificant...programming notes][ntuedu], which has very, very detailed explanation of the subject.
* [Tutorialspoint][tutpoint]
* [Wikipedia about Single responsibility principle][wikispp]

Happy object orienting!

-sorhanp
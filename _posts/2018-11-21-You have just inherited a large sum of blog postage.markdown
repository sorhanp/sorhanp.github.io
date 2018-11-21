---
layout: post
title:  "You have just inherited a large sum of blog postage."
categories: programming
description: My findings about C++(CPP, or cpp) object oriented programming and inheritance.
tags: programming, c++, object-oriented, cpp, inheritance
excerpt_separator: <!--more-->
---

[uml]:https://en.wikipedia.org/wiki/Unified_Modeling_Language
[aticleworld]:https://aticleworld.com/inheritance-in-c/
[geeksforgeeks]:https://www.geeksforgeeks.org/inheritance-in-c/
[tutorialspoint]:https://www.tutorialspoint.com/cplusplus/cpp_inheritance.htm
[cplusplus]:http://www.cplusplus.com/doc/tutorial/inheritance/
[programiz]:https://www.programiz.com/cpp-programming/inheritance
[javatpoint]:https://www.javatpoint.com/cpp-inheritance
[wikipedia]:https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)
[last_post]:/programming/2018/11/16/Memories-about-pointers,-or-was-it-pointers-about-memory.html
[couple]:/programming/2018/11/11/Constructing-and-destructing.html
[past]: /programming/2018/11/03/Object-Oriented-Programming.html
[feature_phones]:https://en.wikipedia.org/wiki/Feature_phone
[imei]:https://whatis.techtarget.com/definition/IMEI-International-Mobile-Equipment-Identity

[Last time][last_post] I wrote about something that was very tricky for me to understand in the past which was pointers and memory. Continuation on the path to becoming more fluent in object orientation programming my next stumbling point was inheritance in C++. Making sure that the history doesn’t start repeating itself, this time I wanted to make sure that I understand what is going on and so. So like previously with pointers and memory, I started by reading as much as possible about inheritance. <!--more-->

Inheritance is huge part of the object orientation and it means that classes can acquire data members and methods from another class. Like always it would best to start again with an example. I think it is yet again time to use our precious MobilePhone-class that I have already used in [couple][couple] of [past][past] examples. For this example, I will be streamlining my MobilePhone-class from the previous example, because not every phone can access email, ie. phones that are designed for older people, the so called “[feature phones”][feature_phones]. However I have ditched the additional classes for reading email etc. just to make this example purely about inheritance in object-oriented programming.

![Classes with inheritance](/assets/classes_inheritance.svg)
Picture 1. Classes with inheritance.

Before going into detail about the picture above, let me first start by saying that while most of modern programming languages have inheritance and object-orientation I will write this purely on the viewpoint of a C++-language. So what inheritance allows programmers to do? One of the benefit is reducing duplicate code, which is done by letting other classes use the same data methods and members that the class where they are inheriting them from. For example “MobilePhone”-class has data member [IMEI(International Mobile Equipment Identity)][imei] and since every mobile phone, smart or feature, needs its own IMEI or they cannot function in mobile network it is placed here on top so that every other class can inherit it. This same data member can be inherited by all the other classes that are “connected” with it. In example picture this means that even the class called “Smartphone” can has it own IMEI, if necessary, because it is connected to “MobilePhone” class through all the classes that are between them. Without inheritance every class that needs to have its own properties, such as IMEI, screenSize or methods, such as access to email written in to them. It might not sound bad with this image example but with bigger projects where there are hundreds of classes this reduces code rewrite **A LOT**. This is pictured below with every mobile phone looking the same and always when new phone needs to be created, it would needed to write again from scratch. Even if they have same operating system, same screen size and so on. Because of that another benefit from inheritance is errors and by that I mean that there are lot less changes to write code that does something wrong, while also making the code more easier to maintain. Of course fewer lines of code also mean shorter development time, which leads to more cost effective products.

![Classes without inheritance](/assets/classes_without_inheritance.svg)
Picture 2. Classes without inheritance.

So what are terms that are used in inheritance? There is actually couple and I haven’t set using either one yet because so many sources use these differently. Some say a base class and a derived class, while others prefer subclass or child instead of derived class. There is also the term superclass or parent for base class. For the sake of this blog and clarity I will use terms base class and subclass. With these terms the base class in first image is the “MobilePhone” while it has a subclass “Manufacturer”. This subclass is a base class to two subclasses “SmartPhone” and “FeaturePhone” which both are base classes to subclass “Model”. It can also be said that subclass extends from base class, because it acquires data members and methods from base. It should be also noted that each of different inheritance types have their own name. I will refer back to picture 1 when explaining the differences:
1. **Single inheritance** happens when Manufacturer (subclass) extends from MobilePhone (base class).
2. **Multiple inheritance** happens when SmartPhone and FeaturePhone (both subclasses) extend from Manufacturer (base class).
3. **Multilevel inheritance** happens when FeaturePhone (subclass) extends from Manufacturer (base class of FeaturePhone), which then continues with Manufacturer (now a subclass since it is extending) extends from MobilePhone (base class).
4. **Hierarchical inheritance** is like what is featured in picture 1, where there is one base class at the top and then it splits in to multiple subclasses, which then can split in their own subclasses and so on.
5. **Hybrid, or virtual, inheritance** is when all of the previous types are combined so there might be one hierarchical inheritance that is then connected to one multiple one. This is rather rare occurrence but I will post a example when I come up with one. Meanwhile you can also contact me with email and send me your own examples.

So how does this all transform in the code. Here is a same classes described in the picture 1 in written in C++ language:
{% highlight cpp %}
class MobilePhone {
    private:
    int IMEI;
    public:
    MobilePhone(int imeiFromUser): IMEI(imeiFromUser){
        /*Using initializer list so that IMEI-code can be stored to
        private data member IMEI*/
    }
    void makePhoneCall(int phoneNumber){
        //code to make a phone call
    }
 };

class Manufacturer: public MobilePhone {
    private:
    std::string manufacturerName;
    public:
    Manufacturer(int imeiFromUser): MobilePhone(imeiFromUser){
        /*Using initializer list so that IMEI-code can be stored to
        private data member IMEI of the MobilePhone-class by
calling its constructor*/
    }
    void manufacturerPackage(int packageVersion){
        //code to install software package
    }
 };

class SmartPhone: public Manufacturer {
    private:
    int screenSize;
    public:
    SmartPhone(int imeiFromUser): Manufacturer(imeiFromUser){
        /*Using initializer list so that IMEI-code can be stored to
        private data member IMEI of the MobilePhone-class by
calling its constructor*/
    }
    void accessEmail(std::string userName){
        //code to login to user email and display unread mail
    }
  };

class FeaturePhone: public Manufacturer {
    private:
    bool PhysicalKeyboard;
    public:
    FeaturePhone(int imeiFromUser): Manufacturer(imeiFromUser){
        /*Using initializer list so that IMEI-code can be stored to
        private data member IMEI of the MobilePhone-class by
calling its constructor*/
    }
    void listenFmRadio(float channel){
        //code to open radio application and setting channel
    }
  };

class Model: public SmartPhone, public FeaturePhone {
    private:
    std::string versionName;
    int ModelNumber;
    public:
    void printModelNumber(){
        //code to show model number and all the other specs
    }
  };
{% endhighlight %}

There are a lot of private- and public-keywords used with classes. These are part of the abstraction and they are used to encapsulate data. I will next time spend blog post explaining what each of these mean and continue my [first blog post about object orientation][past]. Above code snippet shows that when we start expanding the “MobilePhone”-class to contain more data members or methods they can easily be implemented to all of the subclasses as well. Couple of new lines of code versus adding the same kind of lines to every class. The code above also demonstrates how constructors behave with inheritance in C++. Long story sort: in C++ constructors are only called, not copied. This means that when object is created the constructor of base class is also called. If there are multilevel inheritance in the code then all the constructors of classes above the subclass are executed. With initializer list constructors even the private data members of the top base class can be accessed. It should be noted that even with inheritance private data members of a base class cannot be accessed without public data methods, such as constructors in above code example. I will also return to this subject in next blog post when talking more about encapsulation.

However not everything is always just positives, since there are also thing that should be also noted when using inheritance. Because of close relationship of the subclass and base class, any changes written to base class affect all the subclasses below it. That is why it is really important to document what class relations with, for example, [Unified Modeling Language][uml]. Inheritance also allocates more memory as program will have to keep records of the base classes as well as the subclasses. Some of the allocated memory is not even needed in a program, for example if subclass “SmarthPhone” doesn’t need to use method “manufacturerPackage” in a program.

Sources and where to read more:
* [Aticleworld, about inheritance][aticleworld]
* [Geeks for geeks, inheritance in C++][geeksforgeeks]
* [Tutorialspoint, C++ inheritance][tutorialspoint]
* [Cplusplus inheritance tutorial][cplusplus]
* [Programiz: inheritance][programiz]
* [Javatpoint][javatpoint]
* [Wikipedia about inheritance in object oriented programming][wikipedia]

-sorhanp
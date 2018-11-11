---
layout: post
title:  "Constructing and destructing"
categories: programming
excerpt_separator: <!--more-->
---
[object oriented programming]: /programming/2018/10/31/Out-with-the-old-in-with-the-new.html
[mediumcom]: https://medium.com/tech-vision/all-about-destructors-in-c-62b5f534057e
[hackere]:https://www.hackerearth.com/practice/notes/deep-copy-and-shallow-copy/

Wow! Almost didn’t make a single post this week, since it has been a blast and I have been doing much stuff in my private life as well as coding. I have learned so much during the week and because I didn’t want to break the good learning streak I did not have the time to post the usual two posts per week which I have been targeting for. <!--more-->

So last time I wrote about [object oriented programming][object oriented programming]. This post is no different because it is both big and important concept, and all the things that I have been learning this week also have prepare me to be better at creating object oriented code. I currently feel that what I’m learning are not separate blocks of code here and there, but instead parts of a bigger picture, which is nice feeling to have, when doing any kind of learning. It makes it a process and gives the feeling of progression and continuity. Same can be said about this blog. I first started blogging to serve as a diary where I can come back later and see what I have done, keep track of learning sources and so on. It is still that of course, but I like to think that it now also serves as a learning tool. I think the difference is that using a blog as learning tool is a way to think back and put in concrete writing what has been learned this week, whereas a diary is, like said before just there for a quick look back of things that have been done, like a reference sheet. So evolution has happened and I like to think that it is not stopping anytime soon. Now what have I learned this week...

So the week has been all about constructors, copying them, overloading them and of course their counterpart destructors. What do all these have to do with programming and more closely, what it means in terms of object orientation. Last time I wrote that objects are created from a class, which serve as blueprint of how the object should be build. Classes include data members, so the things that describe what the object looks like, color etc., and data methods, the things that objects can do, like make a phone call, or read email. Constructors are data methods that are instantly called when object is created from class. In its simplest form constructor can be, for example, text box that informs that the object has been successfully created, so that the user knows that the program is working correctly. Constructors can be also used to input default values to data members. Expanding on the mobile phone class created on last blog post here is a constructor that prints out text about successful creation of a object and sets default values to two data members.
{% highlight cpp %}
class MobilePhone {
    private:
    string Model;
    int ModelNumber;
    int IMEI;
    string Color;
    string OperatingSystem;

    public:
    //The following is a constructor. It has same name as a class has.
    MobilePhone(){std::cout << "Object created"; ModelNumber = 000000; IMEI = 000000; };
    //Constructor prints out text and sets two data members to 000000 value.
    void MakePhoneCall(int NumberToCallTo);
    void OpenInternetBrowser(string NameOfBrowser);
};
{% endhighlight %}

As seen in the example above constructor has the exactly same name as the class has, and in this case it is MobilePhone. Constructors can be overloaded, this means that there can be multiple constructors, which each has the same name as the class, with only difference being that the each constructor must have different arguments passed to them. Let's keep expanding the class:
{% highlight cpp %}
class MobilePhone {
    private:
    string Model;
    int ModelNumber;
    int IMEI;
    string Color;
    string OperatingSystem;

    public:
    MobilePhone(){std::cout << "Object created"; ModelNumber = 000000; IMEI = 000000; };
    MobilePhone(int UserInputModelNumber) {ModelNumber = UserInputModelNumber};
    //Above overloaded constructor that takes one argument from user and..
    //..stores it in to private data member ModelNumber
    void MakePhoneCall(int NumberToCallTo);
    void OpenInternetBrowser(string NameOfBrowser);
};
{% endhighlight %}

Like said there could be another constructor that only has IMEI as an argument, one more constructor which has both IMEI and model number as an argument and so on with possibilities creating as many as there is need in the program, long as arguments are different from each other. I will present an example how these can be used when creating an object from class next, but before that I would like to talk about destructors, which are the opposite of constructor, like the name suggests. Being an opposite destructors are called when object is terminated. Here is what destructor looks like:
{% highlight cpp %}
class MobilePhone {
    private:
    string Model;
    int ModelNumber;
    int IMEI;
    string Color;
    string OperatingSystem;

    public:
    MobilePhone(){std::cout << "Object created"; ModelNumber = 000000; IMEI = 000000; };
    MobilePhone(int UserInputModelNumber) {ModelNumber = UserInputModelNumber};
    ~MobilePhone() {std::cout << "Object terminated";};
    //Above is a destructor that prints out message
    void MakePhoneCall(int NumberToCallTo);
    void OpenInternetBrowser(string NameOfBrowser);
};
{% endhighlight %}

Destructor again uses the class name but this time it has ~ in front of its name, indicating that it is indeed destructor. To further demonstrate when object termination happens here is an example code snippet using all of the things above, the default constructor, overloaded  constructor and a destructor.
{% highlight cpp %}
int main(){
//Object created using the default constructor
MobilePhone DefaultMobilePhone;

//Object Created using overloaded constructor with ModelNumber argument.
MobilePhone OverloadedMobilePhone(000000);

return 0;
//The point when destructor is called and the object is terminated
//is this last curly bracket:
}
{% endhighlight %}

So destructor is called at the end of the program and it frees up the memory that is being reserved to the object. That is the so called default destructor that happens always, even when it is not defined by the program itself. However it is possible, as demonstrated, to make your own destructor that runs any code that it supported by destructor. Unlike constructors, there can only one destructor in a class and there cannot be any arguments passed to it. One could think that why it is necessary to have these in the first place and what are the use cases for destructors then? There is good explanation in [this page][mediumcom]:
>Since C++ does not include a garbage collector like in other high-level languages (Java/C#), sometimes we have to explicitly deallocate the memory what we have assigned. So, programmers have to do this dirty job manually. Otherwise, this could be lead to a memory leak.

Memory leaks happen when program has objects that are not needed anymore, but the memory is still assigned to these objects. Reserved memory cannot be used by other objects and any newly created object take up new part of the memory. This “unnecessary” memory is very small at first, but after other objects are created and the memory never released the program can later become very slow and unresponsive to the user. Destructors come in handy when object are created in heap memory instead of stack memory. I will return to these memory management and allocations later, because I’m still in the middle of learning about pointers, memory locations, new-operator etc.

I left the last piece of constructor type for last, so what are copy constructors? Best way to describe them are to use this code example:
{% highlight cpp %}
//Object created using the default constructor:
MobilePhone DefaultMobilePhone;
//Copying DefaultMobilePhone object to new object called CopyMobilePhone
MobilePhone CopyMobilePhone = DefaultMobilePhone;
{% endhighlight %}

Copy constructor is called when an object is copied by using =-operator. Normally C++ can form its own copy constructor which automatically copies the value of data members from the original object to the newly copied object. However there is a possibility to create your own if it is needed. Final addition to the MobilePhone-class is going to be new overloaded copy constructor:
{% highlight cpp %}
class MobilePhone {
    private:
    string Model;
    int ModelNumber;
    int IMEI;
    string Color;
    string OperatingSystem;

    public:
    MobilePhone(){std::cout << "Object created"; ModelNumber = 000000; IMEI = 000000; };
    MobilePhone(int UserInputModelNumber) {ModelNumber = UserInputModelNumber};
    ~MobilePhone() {std::cout << "Object terminated";};
    MobilePhone(const MobilePhone &other) {ModelNumber = other.ModelNumber;};
    //Above is example of overloaded copy constructor
    void MakePhoneCall(int NumberToCallTo);
    void OpenInternetBrowser(string NameOfBrowser);
};
{% endhighlight %}

This overloaded copy constructor only copies the ModelNumber data member to new object called CopyMobilePhone. Copy constructors copies are also known as either **deep copies** or **shallow copies** and there is a very good explanation about it to be found [here][hackere].

That is all the constructing and destructing I have been doing this week. Next blog post is going to be about pointers and memory and hopefully I will be able to write it bit sooner, because I found that subject matter very interesting. Keep on constructing!

-sorhanp
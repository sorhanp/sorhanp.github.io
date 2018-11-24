---
layout: post
title:  "High-level concept, a post about abstraction and encapsulation"
categories: programming
description: My findings about C++ (CPP, or cpp) object oriented programming, encapsulation and abstraction.
tags: programming, c++, object-oriented, cpp, inheritance
excerpt_separator: <!--more-->
---

[libraries]:https://en.cppreference.com/w/cpp/links/libs
[last_post]:/programming/2018/11/21/You-have-just-inherited-a-large-sum-of-blog-postage.html
[before]:/programming/2018/11/03/Object-Oriented-Programming.html
[libharu]:http://libharu.org/
[cplusplus]:http://www.cplusplus.com/doc/tutorial/inheritance/
[csharp]:https://www.c-sharpcorner.com/UploadFile/cda5ba/object-oriented-programming-with-real-world-scenario/
[ntuedu]:https://www3.ntu.edu.sg/home/ehchua/programming/cpp/cp3_OOP.html#zz-3.
[w3school]:https://www.w3schools.in/cplusplus-tutorial/encapsulation/
[learncpp]:https://www.learncpp.com/cpp-tutorial/115-inheritance-and-access-specifiers/

[Last blog post][last_post] included something new that I haven’t really touched upon, when talking about classes or object orientation in general and that is abstraction (while mentioning it [before][before], I haven’t wrote a blog post touching the subject) and encapsulation. Encapsulation plays a huge part in limiting access to certain parts of the code, which is the basis of object oriented programming. And to recap, abstraction means providing the user with minimal amount of background details and hiding all the rest so that the user cannot access them later. User in this case means another programmer that may start programming with classes another one have created OR when programmer starts using [libraries], such as Boost or SDL. User of compiled and ready to use program is **end-user** in this case. <!--more-->

So why would you want to hide away information from someone else, wouldn’t it be better that everybody knows exactly what is going on with your code? And how it is beneficial to limit access to certain data members or methods? Former one is part of abstraction and the latter encapsulation. Let’s dive in to these subjects in more detail and take a look at how they are done in C++.

C++ and abstraction
==================
From my [object oriented programming-post][before]:
>Best way to describe abstraction is to compare classes and objects to variables and named storages created from them.
{% highlight cpp %}
    string ExampleVariable = “Name of phone”;
    //string variable with storage name “ExampleVariable” that holds one value.
    MobilePhone ExampleMobilePhone(“Name of phone”, IMEI, etc…) ;
    /*Object ExampleMobilePhone is created from previously created
    class MobilePhone and it contains multiple values.
    Later this phone can do different methods,
    such as MakePhoneCall(number); to call someone.*/
{% endhighlight %}
>As seen in this example abstraction provides only the needed information and hiding their background details.

Continuing expanding from this example about why information is hidden this way can be compared to mobile phone itself. The **end-user** of a mobile phone doesn’t need to know specifics on how a phone call is made, and more importantly what kind of code is behind that, this information is insignificant to them. End-user needs to know only that when they press the contact name on their contact list it dials the contact that they choose. Likewise in this case when somebody else starts using in example MobilePhone-class in their own program, the programmer of that program doesn’t need to know exactly what kind of code is “behind the scenes”.

How is distribution of classes done exactly? C++ source code is are usually kept in two files, a header file (file extension .h) and the so called “regular” source code file (file extension .cpp). Class declaration goes inside header files while the implementation goes to inside the .cpp-file. Again, I’ll use the MobilePhone-class to illustrate what this mean in practice. Let's start by creating a header file called MobilePhone.h:
{% highlight cpp %}
//Check if this class has already been defined and if not, define it.
#ifndef _MOBILEPHONE_H
#define _MOBILEPHONE_H


class MobilePhone {
    private: //Private data members and methods
    int IMEI;
    protected: //Protected data members and methods
    int pinCode;
    public: //Public data members and methods
    
    //Constructors:
    MobilePhone();
    MobilePhone(int imeiFromUser, int pinCodeFromUser);
    
    //Methods to change data members later
    void changeImei(int newImei);
    void changePinCode(int newPin);
    
    //Methods to return out values of data members
    int returnImei();
    int returnPinCode();
    
    //Method to use mobile phone-class to make a call
    void makePhoneCall(int phoneNumber);
 };

#endif /* _MOBILEPHONE_H */
{% endhighlight %}

With header file **declared**, now it is time to **implement** what each of the data methods do:
{% highlight cpp %}
//Tells compiler to include the declaration file
#include "MobilePhone.h"

//MobilePhone:: is needed so that the compiler knows 
//these are methods of MobilePhone-class
MobilePhone::MobilePhone(){
//Constructor that sets default value if user doesn’t provide anything
//when creating a object from this class
    IMEI = 000001;
    pinCode = 1234;
}

MobilePhone::MobilePhone(int imeiFromUser, int pinCodeFromUser){
//Constructor that sets values of data members at creation of class.
    IMEI = imeiFromUser;
    pinCode = pinCodeFromUser;
}

void MobilePhone::changeImei(int newImei){
//Saves value from newImei variable to IMEI data member
    IMEI = newImei;

}
void MobilePhone::changePinCode(int newPin){
//Saves value from newPin variable to newPin data member
    pinCode = newPin;
}

int MobilePhone::returnImei(){
//When this data member is called it returns the IMEI of an object.
    return IMEI;
}

int MobilePhone::returnPinCode(){
//When this data member is called it returns the pinCode of an object.
    return pinCode;
}

//Following is a data method that does something when it is initiated.
//It is here as an example that objects can to various things
//that are not necessary tied to data members.
void MobilePhone::makePhoneCall(int phoneNumber){
    //code make a phone call
}
{% endhighlight %}

Now when this distributed forward to users the actual implementation file is hidden from the users (by creating a so called object-file) and only the declaration (header file) is provided to users. That way the users know what the class looks like, what data members and methods are included but doesn’t know how they are implemented, since object files cannot be accessed. Now the users can add the class in their own program easily as demonstrated where in main.cpp-file that I created:
{% highlight cpp %}
#include <iostream>
//Tells compiler to include the declaration file
#include "MobilePhone.h"

int main(){
    
    //Creates a object from a MobilePhone without setting data members
    MobilePhone ExamplePhone;
    //IMEI is 000001 and pinCode 0000
    
    //Creates a object from a MobilePhone setting data members
    MobilePhone myExamplePhone(3252121312, 4321);
    //IMEI is 3252121312 and pinCode 1234
    
    //Now if data members need to be changed later it can be done with 
    //changeImei or changePinCode methods:
    ExamplePhone.changeImei(3252121313);
//ExamplePhone.IMEI = 0; cannot be used and I will talk more about in
//next section    

    //Printing out what the current pinCode is:
    std::cout << ExamplePhone.returnPinCode() << std::endl;
    
    //Make a call to number 0302121xxx
    ExamplePhone.makePhoneCall(030212xxx);
    
    return 0;
}
{% endhighlight %}

As can be seen including previously made class to your own program is very simple. Included classes can be about anything and as can be seen at the [libraries][libraries]-list there are something for everything so that everything doesn’t need to be done from the ground up when programming a new program. For example [libharu][libharu] is a library for generating PDF files so that you do not need to create it yourself. Any programmer can add it to their program without needing to figure out how PDF file generation is done themself. With libraries all they need to do is read the documentation about how library is included and what kind of methods or functions are included and how the user can access them. They don’t need to know how the code behind the methods or functions. This same can be applied to one developer who creates thousands classes during one project and later uses some them in other projects. Abstraction can be compared to house building in a way that the carpenter doesn’t need to know how bricks are made or what kind trees should be cut down to make dimensional lumber out of it. Carpenter simply puts the building materials together to build a house from it.

C++ and encapsulation
==================
Previous code examples included keywords private, protected and public. These keywords are used to hide even more from the user. Since user can view the declaration file perhaps better way to say it that they are hidden in plain sight since their access is limited. Encapsulation is a way of setting access levels to data members or methods. I also mentioned this on [last blog post][last_post] on inheritance, where these access levels are also used. So what do these mean? Well for first of all they are called access specifiers and when they are inside of a class they limit how users are able to access data members and methods inside the class. Here is a list of what each of the keyword does:
* **Public** doesn’t limit the access at all, so data is available everywhere in the program.
* **Protected** limits access from outside of the class except classes that are inherited from it.
* **Private** is used by default, and all data of a class remain in this mode if nothing else is stated. Limits the access so that **only** the class itself can access these members.

As seen in example code there is one private data member called IMEI that is of type integer. This data member cannot be accessed, for example from main.cpp file (see ExamplePhone.IMEI = 0; comment). If it is done compiler gives out error stating that this data member is private. Because there are public data **methods** that can be used to change IMEI (ExamplePhone.changeImei(3252121313);) one might think that what is the point of using these access limitations when user can still change them with public methods. These examples are in small case and it is true that in this it can look bit silly, but this prevents unplanned usage of data members such as mixing up the usage of data members to directly change their value and data methods way of setting up the value. Going back to carpenter example above encapsulation is like making sure that carpenter doesn’t have direct access to explosives to blow up the rock that is blocking the foundation, but that same carpenter can call a specialist who has a training to do it as safe as possible. It is to prevent accidents or in case of programming, crashes.

Then what about in inheritance. Usually when inheritance is done public access level is almost always used, but there still might be cases when private or public are used.
Here is code example from inheritance example with all the access specifiers:
{% highlight cpp %}
class MobilePhone {
    private: //Private data member
    int IMEI;
    protected: //Protected data member
    int pinCode;
    public: //Protected data member
    int productNumber;
 };

class Manufacturer: public MobilePhone {
    //This class inherits from MobilePhone with public
    //access identifier
 };

class SmartPhone: protected MobilePhone {
    //This class inherits from MobilePhone with protected
    //access identifier
  };

class FeaturePhone: private MobilePhone {
    //This class inherits from MobilePhone with private
    //access identifier
  };
{% endhighlight %}

The way access specifiers work in classes is best explained by using above examples data members IMEI (private), pinCode(protected) and productNumber (public). When inherit happens publicly all these data members are inherited as they are to the class that is doing the inheritance. That means that in the example case, members that are in the Manufacturer-class now have the same access level as the class they are inherited from so IMEI is stil private, pinCode is still protected and productNumber is still public.

When inheritance is done with protected specifier all the data members that have been public are now transformed to protected, but the rest stay the same. That means that in our little example SmartPhone IMEI is still private, pinCode is still protected and productNumber is transformed to protected and thus SmartPhone member productNumber is no longer accessible from everywhere. Lastly when inheritance is done with private specifier all the data members are transformed to private. That means that FeaturePhone class has all three of the data members private. Please note that during inheritance the base class MobilePhone access specifiers to data members and methods does not change and these changes only target the inherited class. Nevertheless it is very rare to use anything else than public-specifier when inheritance is done so what is the most important to keep in mind is how things behave when that type on inheritance is done.

Final thoughts and further reading
==================
As can be seen that these two concepts work together to make *high-level concepts* possible. Abstraction makes everything that is not necessary to know hidden and encapsulation acts as a “gatekeeper” so that unnecessary details are kept away from harmful usage of data members and methods. 

Sources and where to read more:
* [Cplusplus inheritance tutorial][cplusplus]
* [C# corner][csharp] The code is about C# but still viable in C++ because it is mostly about the concept.
* [Ntuedu][ntuedu]
* [W3School][w3school]
* [LearnCpp][learncpp]


-sorhanp
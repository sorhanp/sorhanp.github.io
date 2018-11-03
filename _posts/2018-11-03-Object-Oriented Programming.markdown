---
layout: post
title:  "Object-Oriented Programming"
categories: programming
excerpt_separator: <!--more-->
---
[arch]: https://www.archlinux.org/
[virtualbox]: https://www.virtualbox.org/
[github]: https://github.com/sorhanp
[Amaintenance]: https://wiki.archlinux.org/index.php/System_maintenance
[debian]: https://www.debian.org/
[ubuntu]: https://www.ubuntu.com/
[xfce]: https://www.xfce.org/
[kate]: https://kate-editor.org/
[brackets]: http://brackets.io/
[jani]: http://www.penttinen.fi/
[splitted]: http://cse230.artifice.cc/lecture/splitting-code.html
[eclipse]: https://www.eclipse.org/ide/
[oop]: http://www.ntu.edu.sg/home/ehchua/programming/cpp/cp3_OOP.html
[beginnerscpp]: https://www.udemy.com/free-learn-c-tutorial-beginners/learn/v4/content
[isofaq]: https://isocpp.org/wiki/faq/classes-and-objects
[cplusplus]: http://www.cplusplus.com/doc/tutorial/classes/
[cppreference]: https://en.cppreference.com/w/
[previous]: /programming/2018/10/26/Keeping-on-keeping-on.html
[source]: https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/

My last blog post was mostly about my change of tools and in this post I’m going to describe more closely my learning progress so far. Last time I wrote about loops, which are very important part of programming and about my new findings such as setprecision(). This time I’m mostly writing about [Object-Oriented Programming][oop], which I have been very interested since I heard about it back in the day and learned what it really means.<!--more--> Usually when I try to learn something that I’m really into, I also try to search as much background information as possible so that I can form a complete understanding about it. I know that sometimes that is not possible, but with programming I think that this is really necessary. In the past when I was younger I learned programming by reading something superficially and then moving on the programming part without truly having comprehension of the subject matter. Usually this lead to situations where I would face a problem and then force my way through. Using this tactic usually leaves me with knowledge how to solve that particular problem, but doesn't make me truly learn anything. Managing to understand the big picture is the most important.

Object oriented programming is based completely around data structures that contain data fields and methods. These structures are called objects, and hence the name object oriented. Expressing this using an example is probably the easiest way to start.  Everyday things that you find around you are in fact *objects*. For example the device that you are reading this is an object, be it a mobile phone, computer, tablet, anything can be used to access web pages. For the sake of an example let say that it is a mobile phone, each mobile phone has its attributes (data fields), like size, weight, color and so on. Each mobile phone also have things one can do with it, like text messaging, browsing the Internet and so on. These things that can be done with it are methods. In programming these objects are created from a *class*. Classes are like blueprints for the object, so one can go and build one object (in this case one mobile phone) from it, let's keep up with the example above and build a class mobile phone in C++. 
{% highlight cpp %}
class MobilePhone {
    //Data fields also known as attributes of the phone:
    string Model;
    int ModelNumber
    int IMEI;
    string Color;
    string OperatingSystem
    //These are only examples, as mobile phones can have many attributes

    //Methods also known as things you can do with a phone.
    public:
    void MakePhoneCall(int NumberToCallTo)
    void OpenInternetBrowser(string NameOfBrowser)
    //Mobile phones tend to have a lot of things you can do it so that means a lot of members so let's keep it sort and keep reading how one should go and create classes that are not too large.
};
{% endhighlight %}

As you can see from above example an object can have multiple data fields and even longer list of methods. This is why usually things are separated into multiple classes like this:
![Classes](/assets/classes.svg)


-sorhanp
---
layout: post
title:  "Monthly recap - November"
categories: programming
description: My findings about C++ (CPP, or cpp)
tags: programming, c++, object-oriented, cpp
excerpt_separator: <!--more-->
---

[cppbeginners]:https://www.udemy.com/share/1000sQBEUccF1bRX4=/
[johnpurcell]:https://caveofprogramming.com/
[helloworld]:https://en.wikipedia.org/wiki/%22Hello,_World!%22_program
[oop]: /programming/2018/11/03/Object-Oriented-Programming.html
[loops]:/programming/2018/10/26/Keeping-on-keeping-on.html
[docs_oracle]:https://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html
[constructors and destructors]:/programming/2018/11/11/Constructing-and-destructing.html
[psychologytoday]:https://www.psychologytoday.com/us/blog/happiness-in-world/200911/eight-ways-remember-anything
[stroustrup]:http://www.stroustrup.com/programming.html
[cpp11]:https://en.wikipedia.org/wiki/C%2B%2B11
[cp14]:https://en.wikipedia.org/wiki/C%2B%2B14
[cp17]:https://en.wikipedia.org/wiki/C%2B%2B17
[pointers]:/programming/2018/11/16/Memories-about-pointers,-or-was-it-pointers-about-memory.html
[abstraction]:https://sorhanp.github.io/programming/2018/11/24/High-level-concept-a-post-about-abstraction-and-encapsulation.html
[inheritance]:https://sorhanp.github.io/programming/2018/11/21/You-have-just-inherited-a-large-sum-of-blog-postage.html
[sdl]:https://www.libsdl.org/
[cppadvanced]:https://www.udemy.com/share/1000MSBEUccF1bRX4=/

There have been a lot of things going on, new things learned and blog post written. Because of that I decided I should also make a little recap of things that I have been working on, what I have learned and what they made me think. What better time than now, when my first full calendar month of blogging is about to be behind me. Granted I will also include the half month of October in the recap. I also will talk about what I have been doing this week and what’s in the future for me. But before we go there lets start all the way from beginning.<!--more-->

Week 43
==================
Week 43 consist of October 22th to 28th and it was the first week of studying. I started my journey with [C++ Tutorial for Complete Beginners][cppbeginners] at Udemy, which is taught by [John Purcell][johnpurcell], John is amazing teacher whose pragmatic way of teaching is really captivating. He tells just enough of the basics, which then makes you experience and play around with the code as much as possible to expand your horizon so to speak. Also because he doesn’t provide all the answers use of search engines is needed. He even emphasizes and encourages it, so that any attendee will start doing so. This suits me fine because I really enjoy learning new stuff by just stumbling upon it. This is why I tend to include a lot of sources to my blog posts, because Internet is chock full of information to be found. I also think that this method of getting known the basics and then gaining more knowledge yourself is motivating.

So what were the main points of week 43? Well the very basics of C++, which include introduction to different kind of variables, [loops][loops], if and else-statements, arrays, advanced conditions(AND and OR) and of course the classic [Hello World][helloworld]. Most of these I still remember from the past, but I still tried to make as many notes to myself as possible, even if the thing seems to be a little tidbit of information that doesn’t seem to have any value at the moment. Better safe than sorry, so that there is no need to backtrack to something that I have should learned. When making notes for myself I, usually write them in to the code as comments and then make a little summary of what I have learned to text document, which in turn sometimes turn in to bigger blog posts, which then go into more detail on topic such as [object-oriented programming][oop]. I tend to write everyday as sort of a my diary so I can later look back at what has been going on and leave myself notes about something that I should read. One of those was [What Every Computer Scientist Should Know About Floating-Point Arithmetic][docs_oracle] which I still haven’t touched upon yet, but it is still there so I can take a look at it. This week also lead me to something of a replacement for arrays, something called **vectors**. To this day I haven’t read more about it, or even used them, but I know that vectors are useful when programmer doesn’t know how many elements might be inside the array. More on this later, since I believe I will learn about them in the future.

Week 44
==================
Week 44 consist of October 29th to November 4th and what I learned that week is the base of my object oriented programming studies, meaning classes, data members, data methods [constructors and destructors][constructors and destructors]. Even if I have studied about these things before, this week was the moment, where I thought to myself that I have truly understood the concept of object orientation. Because I have made myself a goal to use this blogging platform to deliver things as simple as possible to readers, so I have to dig much deeper than the surface level, so that I can deliver understandable content. This goal is there so that I have to do as much background work as possible and fulfill as many [Strategies for Remembering][psychologytoday] as possible. So far I think it is working rather nicely. For example I can now comprehend programs that other people write much better than in the past where I usually just simply run it through a compiler and check what it does. I wrote before about my habits of [brute forcing][oop]:
>Usually this lead to situations where I would face a problem and then force my way through. Using this tactic usually leaves me with knowledge how to solve that particular problem, but doesn't make me truly learn anything.

Not using brute force strategies has enabled me to think like a programmer. To reinforce this abilitty I have acquired a copy of [Principles and Practice Using C++][stroustrup] by Bjarne Stroustrup. The book book promises that it:
> ...helps you understand the principles and acquire the practical skills of programming using the C++ programming language. My aim is for you to gain sufficient knowledge and experience to perform simple useful programming tasks using the best up-to-date techniques.

It also teaches things that are only available on [C++’11][cpp11] and [C++’14][cp14], both of which will be valuable in the future because of new features such as variable templates and initializer lists (something that I have used already). These version of C++ were not available when I first studied C++ all those years ago and it is very nice to see that my favourite programming language has been updated consistently, there is even [C++’17][cp17].

Week 45
==================
Week 45 consist of November 5th to 11th. This is the part where the where the biggest hurdle for most new programmers, such as myself back in the day, is usually had. I started learning about [pointers and C++ memory management][pointers]. Pointers is something that do not exist in other programming language in such extent that they are in C++. This time I wanted to make sure I understood the concept and wrote one of the longest blog post I so far and made as many comments in the code as it was necessary. I even made the programs print out information of current program status as much as possible. Here is an example:
{% highlight cpp %}
    int iNumber = 8;
    
    //Creation of pointer. 
//In this case pointer variable piValue doesn't store the value 8
//but the memory address of iNumber. 
//int* means that it is pointer to the int.
    int* piValue = &iNumber;
    
    std::cout << "Int value: " << iNumber << "\n";
    
    //The following prints out "Pointer to int address: 0x" 
//again referring back to this-statement.  
    std::cout << "Pointer to int adress: " << piValue << "\n";
    
    //The following prints out Int value via pointer: 8. 
//Meaning that it memory address is translated back to value
    std::cout << "Int value via pointer: " << *piValue << "\n";
    
    //Print +-signs to separate function call from the first pointer calls done in this tutorial.
    std::cout << "++++++++++++++++++++++++++++++++++++++" << "\n";
    
    /*The following is the normal way of doing things and it prints out:
    1. dValueInMain 123.4
    2. Value of dValueInFunction in fnManipulate: 123.4
    3. Value of dValueInFunction in fnManipulate after inserting different value to it: 10
    4. dValueInMain 123.4

    Meaning that when dValueInMain variable is passed to fnManipulateNormal function 
it only passes on the data inside of that variable, 
thus creating a copy of itself to function variable called dValueInFunction. 
When dValueInFunction in changed it doesn't change the dValueInMain in anyway.
    */
    double dValueInMain = 123.4;
    std::cout << "1. dValueInMain " << dValueInMain << "\n";
    fnManipulateNormal(dValueInMain);
    std::cout << "4. dValueInMain " << dValueInMain << "\n";
    //Print +-signs to seperate function calls
    std::cout << "++++++++++++++++++++++++++++++++++++++" << "\n";
    
    /*The following is the pointer way of doing things and it prints out:
    1. dValueInMain 123.4
    2. Value of dValueInFunction in fnManipulate: 123.4
    3. Value of dValueInFunction in fnManipulate after inserting different value to it: 10
    4. dValueInMain 10

    Meaning that instead of example above 
that only creates a copy of value that is saved inside dValueInMain this time
dValueInMain is passed to function fnManipulatePointer as a memory address
(0x<numbers>) and when it the value in memory address changed at the function 
so is value of variable dValueInMain changed.
    */
    dValueInMain = 123.4;
    std::cout << "1. dValueInMain " << dValueInMain << "\n";
    fnManipulatePointer(&dValueInMain);
    std::cout << "4. dValueInMain " << dValueInMain << "\n";
{% endhighlight %}

As can be seen above, I also created two example functions so that it can demonstrate different without pointers vs. using pointers:
{% highlight cpp %}
//Example how to use pointers. 
//First here is a function that is done without any pointers:
void fnManipulateNormal(double dValueInFunction){
    std::cout << "2. Value of dValueInFunction in fnManipulate: " << dValueInFunction << "\n";
    dValueInFunction = 10.0;
    std::cout << "3. Value of dValueInFunction in fnManipulate after inserting different value to it: " << dValueInFunction << "\n";
}

//Example how to use pointers. And here is a function that is done with pointer:
void fnManipulatePointer(double *pdValueInFunction){
    std::cout << "2. Value of dValueInFunction in fnManipulate: " << *pdValueInFunction << "\n";
    //Instead of changing this dValueInFunction = 10.0; variable to ten 
//(meaning if its done this way it just tries to access memory adress with the value
//10.0, which doesn't exist). 
//The correct way of doing this is using **dValueInFunction = 10.0, which means that it
//goes to that point in memory and change it to ten;
    *pdValueInFunction = 10.0;
    std::cout << "3. Value of dValueInFunction in fnManipulate after inserting different value to it: " << *pdValueInFunction << "\n";
} 
{% endhighlight %}

This is something that I recommend to any person who is about to learn programming: **print out as much as possible** when you create constructors and destructors, make them inform you, the programmer, that the task is done so you understand how memory management in C++ works, likewise when using pointers make doubly sure that you understand what is being done, like in the code blocks above. Seeing is believing in this case.

Weeks 46 and 47
==================
I grouped these two weeks together because I didn’t have that much of time to concentrate purely on coding because lot of personal matters that needed to be taken care of. These weeks consist of November 12th to 25th. Still I used the little time I had to instead read about abstraction and encapsulation and even [made a post about it][abstraction], sort of sequel to object-oriented post I made at the beginning of the month of November. My current project is heavily object-oriented, which I will tell more in the next section. So it was rather good idea to expand knowledge of important object-orientation parts such as encapsulation.

The time I had to do programming were about [inheritance][inheritance], namespaces and the keyword static in C++. I haven’t really touched upon namespaces in this blog but that is also something that is going in my current project and I will address it later in the bigger blog post that tells about the project. Same with static, so I will keep you, the readers, on the edge off your seat for a little while longer about these topics :)

What now, how about the future?
==================
I’m at the end of one path of journey here. The C++ Tutorial for Complete Beginners is at the end after 7 sections ranging from basic syntax to object oriented programming and beyond to pointers and memory. What remains is a project, called The Particle Fire Simulation. This section teaches how to develop a real life program that actually shows graphics instead of lines of text in a console. Project is being done in a using [Simple DirectMedia Layer][sdl]. I have already started to animate particles drawn on the screen and next up is adding explosions in to the mix.

I know that the program developed on this isn’t fully optimized and have room for improvement, such as selecting resolution, adding frame counters, asking for user input to change how the program behaves etc. After I have completed the “basic” part of the program I will continue to improve it and add it to my GitHub-page. I have used SDL-libraries before and maybe one day I will return to my old game project and try to improve it also. Time will tell, but for now I really enjoy making this project. I have done extensive documentation so this point, which I will also add to my GitHub-page when everything is set.

So there it is. First one and a half month has been a breeze. I think I have come a long way from the start, but still sometimes have the feeling that I could be making progress faster. However writing down and especially now returning what kind of things I have been doing so far really shows, that there is progress and something is being made everyday. So I think that feeling might be due the fact that in my past working environment changes came fast and because I had more experience on the matter I could adapt to that change at steady speed. Here I still struggle a bit **BUT** with good code comments and making sure that I really understand something I can lay good foundation where to build on. I will keep updating my progress on the project and when the final version is ready I will document it to the fullest. After this course it is time to move on the next course called [Learn Advanced C++ Programming][cppadvanced] while reading the book I mentioned.

-sorhanp
---
layout: post
title:  "Keeping on keeping on"
categories: programming
excerpt_separator: <!--more-->
---

[beginnerscpp]: https://www.udemy.com/free-learn-c-tutorial-beginners/learn/v4/content
[multiplytable]: https://en.wikipedia.org/wiki/Multiplication_table
[array]: http://www.cplusplus.com/doc/tutorial/arrays/
[loops]: https://en.wikiversity.org/wiki/C%2B%2B/Loops
[pencil]: https://pencil.evolus.vn/
[iomanip]: http://www.cplusplus.com/reference/iomanip/
[setprecision]: http://www.cplusplus.com/reference/iomanip/setprecision/
[wchar_t]: http://www.cplusplus.com/reference/cwchar/wchar_t/
[utf8everywhere]: http://utf8everywhere.org/

After last blog post I have kept “attending” [C++ Tutorial for Complete Beginners][beginnerscpp] course. During my studies I have found out that I still have the ability to think like a programmer. Meaning, that I have been able to do much more than is required on current lesson and expand my learning with things from the past. <!--more--> For example, when there was lesson about conditions where the lecturer suggested, that after his you should try to do program that does certain [multiplication table][multiplytable] using an [C++ standard array][array] and set values. Instead of hard coding the values to the code itself, I wrote a little program that asks from user how long multiplication table is needed and what number should be multiplied. Example code is below:

{% highlight cpp %}
#include <iostream>
using namespace std;

int main(){

    int iUserTableInput = 0;
    int iUserInput = 0;
    
    cout << "Input how long of a multiplication table do you need > " << flush;
    cin >> iUserTableInput;
    
    cout << "Input which number you want to multiples of > " << flush;
    cin >> iUserInput;
    
    int iMultiplication[iUserTableInput + 1] = {}; 
    // +1 to make sure that there are enough memory allocated to array. 
    
    for (int iLoop = 1; iLoop <= iUserTableInput; iLoop++){
        iMultiplication[iLoop] = iUserInput * iLoop; 
        cout << iLoop << " times " << iUserInput << " is " << iMultiplication[iLoop] << endl;
    }

    
    return 0;
}
{% endhighlight %}

As seen on the little program above, my current lessons have been covering loops and how to implement them to a program. To make sure that I understand how each of them works I decided to look up the differences between [for-, do while- and while-loops][loops] and even went, and couple draw flowcharts of loops to visualize what happens in different loops. I used application called [Pencil][pencil] to draw and the charts are presented below.

For- and while-loop are pretty much the same when put in a simplest flowchart form:
![For- and Do while-loops](/assets/for_while_loop.png)

Do while loop does it differently, since it runs the code always atleast once. Here it is in a flowchart:
![For- and Do while-loops](/assets/do_while_loop.png)

I also read about what are the major differences between each of these loops and when should programmer select which to use, and came to conclusion that it all depends on the circumstances. My favourite anecdote was that each of these are tools for different situation in the same way as the tools in carpenters toolbox. There are several ways to hammer down a nail, but the most elegant and easiest way to use the **hammer** rather than **wrench**. Some programmers may dislike do while loop because it creates confusion. After I have more experience in a matter, I think I will continue using each of the tools provided to find the best solution to each of problems presented to me.

This time I decided to list all the new things that I have learned since my last blog post and comment them a little bit. There haven’t been a lot of completely new things but I still think that using the beginners course as a refresher is a good idea. I have never felt bored, but rather intrigued to find out that I still can remember all the basics. When I decided to change my career path some of the people who I told about my next move told me that returning to something that I have already done before is like riding a bicycle after all these years. You never really forget it all. After almost couple of weeks of setting up development environment to myself and starting to write programs I kind of agree with that sentiment. Anyways, here are the things that were something new to me, or made me do additional digging around the Internet:

* Header called [iomanip][iomanip] provides parametric manipulators such as:
    * [setprecision][setprecision] which include setting decimal precision of floating point values. 
    * I have never really written programs that need floating point values to be this precise and thus haven’t really need these before. After learning about these I'm pretty sure I will use them later on.
    * I will share another code about floating point values after this list.
* [wchar_t][wchar_t] which is used in UTF-16 text encoding. 
    * Altough it should be never used. See [utf8everywhere][utf8everywhere] which state: "Do not use wchar_t or std::wstring in any place other than adjacent point to APIs accepting UTF-16." I think knowing that this is might be handy when coming across legacy systems in Windows environment that had to use old UTF-16/Unicode encoding. Learning bit of history never hurts :)
* Declaring variables at the beginning of the program vs. declaring them when you really need variables in a program.
    * This is something that I have been thinking myself alot when I started all those years ago and when I heard about it again during one of the lessons I thought immediately this is something I should write about.
    * It seems that declaring all the variables at the beginning of the program was something that was done in the old days, when compiler standards where different. However it also depends on the used language. I will keep digging around and come back to this point later when I have found more information to back up one theory over another.

One last piece of new information was comparing floating point values and I learned that that it is like comparing height of two people, as in one person can very rarely be *exactly* same height with another person, even when they might look as tall. Example code below shows one way to compare floating point values.
{% highlight cpp %}
float fValue1 = 1.1;
    if (fValue1 < 1.11){
        cout << "equals" << endl;
    }
    else{
        cout << "not equal" << endl;
{% endhighlight %}

Next up on the course is going to be more advanced programming such as object oriented coding, inheritance and pointers. Can't hardly wait. Until next time!

-sorhanp
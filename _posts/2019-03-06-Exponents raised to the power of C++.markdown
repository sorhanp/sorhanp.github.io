---
layout: post
title:  "Exponents raised to the power of C++"
categories: programming
description: My findings about C++ (CPP, or cpp), Khan Academy, math, mathematics, exponents, raised to power, c++ mathematics, c++ maths, c++ exponent rules and properties
tags: programming, c++, object-oriented, cpp, math, mathematics, exponent, exponents, raised to power,
excerpt_separator: <!--more-->
---

[joint_application]:https://studyinfo.fi/wp2/en/higher-education/applying/
[entrance_exams]:https://studyinfo.fi/wp2/en/higher-education/how-to-apply-for-bachelors/entrance-examinations/
[exponents_rules]:https://www.rapidtables.com/math/number/exponent.html#rules
[arithmetic]:http://www.informit.com/articles/article.aspx?p=1705442&seqNum=6
[bit_shift]:https://github.com/sorhanp/particlefire-revision/wiki/Color
[bitwise]:https://en.wikipedia.org/wiki/Bitwise_operations_in_C
[cmath]:http://www.cplusplus.com/reference/cmath/
[pow]:http://www.cplusplus.com/reference/cmath/pow/
[purple_math]:https://www.purplemath.com/modules/negative4.htm
[google_calc]:https://www.google.com/search?q=-1^2
[microsoft_calc]:https://www.microsoft.com/en-us/p/windows-calculator/9wzdncrfhvn5?activetab=pivot:overviewtab
[galgulator]:http://galculator.mnim.org/
[precedence]:http://macnauchtan.com/pub/precedence.html#_index
[khan_negativeexp]:https://www.khanacademy.org/math/pre-algebra/pre-algebra-exponents-radicals/pre-algebra-negative-exponents/a/negative-exponents-review

My studies at Khan Academy have been chugging along nicely and the application deadlines for [joint application for universities and universities of applied sciences][joint_application] is closing in. I feeling ready to take the next step on my journey and hopefully can perform well on the [entrance examinations][entrance_exams]. When studying algebra I stumbled upon exponents, and more closely, on [their rules and properties][exponents_rules] I started to wonder how C++ handles them and if there are some exceptions that programmers should notice when working with them.<!--more-->

C++ and how to exponents
==================
The fact that there is [no arithmetic operator for exponentiation in C++][arithmetic], means that you cannot write a program like this, and expect correct results:
{% highlight cpp %}
int a = 0;
a = 123^3; 
/*^ is used for Bitwise XOR-operator and this results to 120*/
{% endhighlight %}
I have wrote about bit shifting on my [Particle Fire Revision Color wiki page][bit_shift], and ^-operator is part of [Bitwise operations in C][bitwise]. They are, and especially were, very helpful in the past when hardware was more limited. Because of these legacy reasons (and there is probably myriad of other reasons, but not let’s get in those), it was decided that C++ doesn’t need arithmetic operator for exponents, thus only way of achieving is using external libraries or by coding your own solution such as this very primitive one:
{% highlight cpp %}
int exponent = 3;
int base = 123;
int power = base;

    for(int i = 1; i < exponent; i++){
        power *= base;
    }

std::cout << base << " to the power of " << exponent << " is " << power << std::endl;
{% endhighlight %}
This example would print “123 to the power of 3 is 1860867”. Other way of doing things is using libraries such as [cmath][cmath], which “declares a set of functions to compute common mathematical operations and transformations”, such as cos, sin and tan which I also used as algorithm in [Particle Fire Revision][bit_shift]. Among the functions is [pow][pow], which usage is simple:
{% highlight cpp %}
#include <math.h>
std::cout << pow (123, 3) << std::endl;
{% endhighlight %}
Print out from this is 1.86087e+06 as can be seen it is a floating point number with scientific notation. If there is only need to use integer numbers without any floating, it is better to use own solution, to achieve longer numbers such as 64-bit integers with 19 characters with the maximum value of 9,223,372,036,854,775,807. This is pretty useful, since exponent tend to grow very rapidly.

C++ and exponents properties
==================
Like many things in mathematics there is a list of rules on how things behave when certain conditions are met. This also true for exponents, for example zero-exponent property, which states that anything raised to the 0 power is equals to 1. With that rule the primitive program fails miserably and prints out “123 to the power of 0 is 123”, thus there needs to be some kind of mechanism in place that checks if exponent is 0 and sets the power-variable to 1:
{% highlight cpp %}
    int exponent = 0;
    int base = 123;
    int power = base;
    
    if(exponent == 0){
        power = 1;
    }
    else{
        for(int i = 1; i < exponent; i++){
        power *= base;
        }
    }
    std::cout << base << " to the power of " << exponent << " is " << power << std::endl;
{% endhighlight %}
So how about pow-function? How does it fare with this rule? The print out for...
{% highlight cpp %}
std::cout << pow (123, 0) << std::endl;
{% endhighlight %}
...is “1”, meaning it works as intended!

Next interesting property is one rule, which states that either base of 1 or -1 raised to **any power** is always **1**. Also on -1, completely new rule also applies, which also applies to all negative base numbers, which states that whether the exponent is *odd* or **even** changes the value of product either to *negative* or **positive**, however there is a “catch”, a matter that needs to be examined. But before that, let’s chew on both of these properties since they are connected. First of all pow-function takes all of these in the account and works like it is supposed to:
{% highlight cpp %}
std::cout << pow (1, 2) << std::endl;
//Prints out 1, complying the one rule

std::cout << pow (-1, 3) << std::endl;
//Prints out -1, complying the one rule and the odd part of odd/even rule

std::cout << pow (-1, 2) << std::endl;
/*Prints out 1, complying the one rule and the even part of odd/even rule*/
{% endhighlight %}
The primitive program written for this blog also supports negative bases and here are example print outs:
{% highlight cpp %}
1 to the power of 2 is 1
-1 to the power of 3 is -1
-1 to the power of 2 is 1
{% endhighlight %}
However, now it is time for the “catch” part of it. In mathematics [there is a difference][purple_math] between -1^2 and (-1)^2. What is happening in the both the primitive loop and on the pow-function is the (-1)^2 version, which is same as 1 * (-1) * (-1) = 1. However -1^2 is same as -1 * (-1) * (-1) = -1. This result can be verified on certain web calculators, such as [Google’s][google_calc], but be wary! Other calculators do not address this fact at all and treat -1^2 = (-1)^2. Examples include [Microsoft’s calculator on Windows 10][microsoft_calc] and [Open Source GTK 2 / GTK 3 galgulator][galgulator]. There is even a [list by Douglas P. McNutt][precedence] on how certain software, compilers and scripting languages approach this problem. The list is from 2006, but it shows that this little problem has been prevalent for long time and still continues to be the case. Maybe one day I will perform similar study and inform the developers of this discrepancy.

Since there is no way to program values with ()-parentheses to the pow-function, nor to the primitive program featured on this article this mathematical rule has to be solved using other methods, such as asking for user to verify their input, by asking do you mean with or without parentheses or, if there is calculator-program make it strict in mathematical sense, so that different kind of inputs behave according to the rule. Then when there is confirmation alter the way the program works, for example:
{% highlight cpp %}
    int exponent = 0;
    int base = 0;
    int power = base;
    bool parentheses = true;
    
    if(exponent == 0){
        power = 1;
    }
    else if(parentheses == true){
        for(int i = 1; i < exponent; i++){
            power *= base;
        }
    }
    else{
        for(int i = 1; i < exponent; i++){
        power = -1 * power * base;
        }
    }
{% endhighlight %}
In this case when parentheses-variable are true, the print out is:
“-1 to the power of 2 is 1”, which is correct answer for expression (-1)^2 
However when dealing with situation where the variable is false, print out is altered:
“-1 to the power of 2 is -1” which is correct answer for expression -1^2.

Now some people might be thinking why -1^2 ≠ (-1)^2 and some maybe even answered to exponent problems incorrectly, when basing their answer to software or calculator that doesn’t respect this strict mathematical syntax. The answer to this is in the ground rules laid out by exponent itself. Since [negative exponents][khan_negativeexp] indicate how many times number 1 is divided by a base. For example 4^-3 = 1 / (4 * 4 * 4) = 0.015625. This same rule can be also applies to positive exponents, as in how many times number 1 is multiplied by base. For example 4^3 = 1 * (4 * 4 * 4) = 64. So when these same rule is applied to negative base, it explains why parentheses matter. So starting with (-1)^2, what it really means under these rules? 1 * (-1) * (-1), and since negatives cancel each other out when multiplying the expression is simplified to 1 * 1.  With this same rules -1^2  = -1 * (1) * (1), meaning that the exponent doesn’t affect the negative sign but only the integer 1, and since there is only single negative sign the final answer is also negative. The same logic applies to all positive and negative base numbers, not just 1 and -1. So to recap here is nice table as reminder, and with algebraic equations:

| Rule  | Equation | Example Calculation |
|:-:|:-:|:-:|
| One rule | 1^n = 1 | 1^128 = 1 |
| Negative one rule, with parentheses | (-1)^n = positive 1 if n = even number, else negative | (-1)^2 = 1,<br/> (-1)^3 = -1 |
| Negative one rule, without parentheses | -1^n = -1  | -1^4 = -1 |
| Negative base, with parentheses | (-x)^n = positive y if n = even number, else negative | (-5)^2 = 25,<br/> (-5)^3 = -125 |
| Negative base, without parentheses | -x^n = -y | -5^4 = -625 |

These another property related to 0, which states that base 0 raised to any positive power always equals 0. However on negative exponent the answer should be infinity (since what is happening is dividing by zero, which is not defined in mathematics at the moment of writing this blog), and finally if raised to 0 power the result should equal to 1 or undefined depending on the case. Let see how each of these rule behave on the pow-function and primite program that has been growing nicely along the blog post. There are three tests:

1. Positive exponent
2. Negative exponent
3. Zero exponent

Let’s start with pow-function:
{% highlight cpp %}
std::cout << pow (0, 2) << std::endl;
//Prints 0 as expected

std::cout << pow (0, -2) << std::endl;
//Prints the word inf, for infinity, as expected

std::cout << pow (0, 0) << std::endl;
/*Prints 1 as expected*/
{% endhighlight %}
So pow-function gets very good results, 3/3 from the 0 base test. Time for primite program to show what it can do:
{% highlight cpp %}
0 to the power of 2 is 0
0 to the power of -2 is 0
0 to the power of 0 is 1
{% endhighlight %}
Pretty good results, again with slight modification, in which I mean adding a one more else if-statement for the negative exponents with 0 base to print out word infinity, or inf, or maybe even infinity-symbol and it would have been fixed. However, there also could be room for improvement on the code itself, for example improve the algorithm based on the way that exponents are “really” handled, ie. 1 * (4 * 4 * 4) or 1 / (5 * 5 * 5). Before that, there are still some rules that I want to cover on this blog. I will make another post about them later this week, but now I’m off to improve my algorithm and produce the results on next post!

-sorhanp
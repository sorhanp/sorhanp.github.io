---
layout: post
title:  "Part 2/2: Performing prime factorization and finding least common multiple in C++"
categories: programming
description: My findings about C++ (CPP, or cpp), Khan Academy, math, mathematics, prime factorization and least common multiple
tags: programming, c++, object-oriented, cpp, math, mathematics
excerpt_separator: <!--more-->
---

[last]:/programming/2019/01/28/Prime-factorization.html
[lcm]:https://www.mathsisfun.com/least-common-multiple.html
[set_difference]: http://www.cplusplus.com/reference/algorithm/set_difference/
[gcd]:https://en.wikipedia.org/wiki/Greatest_common_divisor

This is a continuation of [Part 1/2: Performing prime factorization and finding least common multiple in C++][last]. On this post I will go through least common multiple and how to implement it to the class I created on last post.<!--more-->

Least common multiple overview 
==================
A multiple is basically like multiplication table, because a **multiple of a number** is the product of *number in question* and *another integer*. So for sake of example three’s multiples are 3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36… until infinity. When applied to mathematical statement of multiple is a product of number and another integer in case of three’s it is 3 * 1 = 3, 3 *2 = 6, 3 * 3 = 9… 3 * 12 = 36… until infinity.

[Least common multiple][lcm] is the smallest positive integer that can be divided by two or more values. As the name suggests it is the lowest possible multiple to each of those values share. To understand this concept better, here is a list of **first ten** multiples of values from 1 to 10, or by simply drawing a multiplication table of 10:

| * | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **1** | 1 | 2 | 3 | 4 | 5 | ***6*** | 7 | ***8*** | 9 | 10 |
| **2** | 2 | 4 | ***6*** | ***8*** | 10 | ***12*** | 14 | 16 | ***18*** | 20 |
| **3** | 3 | ***6*** | 9 | ***12*** | 15 | ***18*** | 21 | ***24*** | 27 | 30 |
| **4** | 4 | ***8*** | ***12*** | 16 | 20 | ***24*** | 28 | 32 | 36 | 40 |
| **5** | 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 | 45 | 50 |
| **6** | ***6*** | ***12*** | ***18*** | ***24*** | 30 | 36 | 42 | 48 | 54 | 60 |
| **7** | 7 | 14 | 21 | 28 | 35 | 42 | 49 | 56 | 63 | 70 |
| **8** | ***8*** | 16 | ***24*** | 32 | 40 | 48 | 56 | 64 | 72 | 80 |
| **9** | 9 | ***18*** | 27 | 36 | 45 | 54 | 63 | 72 | 81 | 90 |
| **10** | 10 | 20  | 30 | 40 | 50  | 60  | 70 | 80  | 90 | 100 |

I have both **bold** and *italic* -effects on every 6, 8, 12, 18, and 24 occurrence of these numbers. Each of these numbers appear total of **four** times in this simple listing of multiples. Each of these numbers are least common multiples for **four** values. For values 1, 2, 3 and 6 the least common multiple is 6. For values 1, 2, 4, and 8 the least common multiple is 8. For values 2, 3, 4 and 6 the least common multiple is 12 and so on. If we apply again the mathematical statement of smallest positive integer that can be divided by two or more values we can clearly see, that 12 is divisible 6, 4, 3 and 2. 12 / 6 = 2, 12 / 4 = 3 and so on. This works, since multiplication is **opposite operation** of division, as 3 groups of 4 makes 12, while 12 divided into groups of 4 is 3 groups.
 
To take these out of the scope of simple multiplication table of 10, and think bigger numbers such as 43, 77 and 102, what is the least common multiple of these values? Of course it is possible to start writing out all the multiples of each of the values like this: 43, 86, …, 77, 154, … and 102, 204, ..., but that is rather time consuming and might be better task for computer to handle. There is simpler way of doing this and that is prime factorization, which was explained in better detail on [part 1][last].

We can start by splitting up 43, 77 and 102 to the product of prime numbers:
43 cannot be factored down to prime numbers, since it is a prime number itself.
The prime factorization of 77 is: 7 * 11.
The prime factorization of 102 is: 2 * 3 * 17.
We can find the least common multiple by product of multiplying the highest power of each prime number together. To put it simply, multiply each **unique occurrence** of the prime numbers above. Least common multiple is the product of 2 * 3 * 7 * 11 * 17 * 43 = **337722**. To put is in words; the least common multiple of 43, 77 and 102 is 337722. This can be proved by performing division operation to 337722 by each of the values. 337722 / 43 = 7854, 337722 / 77 = 4386 and 337722 / 102 = 3311. Now how does this translate in to the Prime-class created at previous post?

Expand prime factorization to include least common multiple
==================
So here is how I implemented least common multiple to Prime-class. First class declaration needs one new vector and two new data methods:
{% highlight cpp %}
//filename: prime.h
#include <iostream>
#include <vector>

//Include algorithm-library for sorting out vectors
#include <algorithm>

class Prime{
    private:
    //Private data members
    int originalValue;
    bool isPrime;
    std::vector<int> factorization;
    
    //Create a new static vector that is designed to hold all the factored values
    static std::vector<int> leastCommonMultiple;
    
    //Private methods
    void Factorization();
    
    public:
    //Constructors
    //Default constructor
    Prime(){isPrime = true; originalValue = 2; Factorization();};
    //Constructor with one parameter
    Prime(int input){isPrime = true; originalValue = input; Factorization();};

    //Public data methods
    void PrintFactorization();
    
    //Create a new static data method for printing out least common multiple(LCM)
    static void PrintLCM();
    
    //Returns vector factorization to the user
    std::vector<int> GetFactorization() {return factorization;}
    
    //Returns static vector leastCommonMultiple(LCM) to the user
    static std::vector<int> GetLCM() {return leastCommonMultiple;}
    
};
{% endhighlight %}

Vector leastCommonMultiple is used to store all **unique prime factors** and for this Factorization data method need one new line of code in Prime-class’s implementation file:
{% highlight cpp %}
//filename: prime.cpp
//Populate the static leastCommonMultiple vector with values from current factorization vector, if there are duplicates, they are not inserted
std::set_difference(factorization.begin(),
               factorization.end(),
               leastCommonMultiple.begin(),
               leastCommonMultiple.end(),
               std::back_inserter(leastCommonMultiple));
{% endhighlight %}

Algorithm-library provides very useful [set_difference][set_difference] function, which detects difference of two vectors. In sort; elements that are present in the first vector (factorization), but not in the second (leastCommonMultiple) are added to desired location, which in this case is leastCommonMultiple.

Since GetLCM is very simple vector returning data method, I will not be covering it further, instead here is the implementation of the second new method, called PrintLCM:
{% highlight cpp %}
//filename: prime.cpp
void Prime::PrintLCM(){
    
    //Sort vector so that values are presented from lowest to highest
    std::sort(leastCommonMultiple.begin(),
              leastCommonMultiple.end());
    
    //Declare variable to hold least common multiple and initialize it to zero
    int iLCM = 0;

    std::cout << "Using prime factorization of values to calculate the least common multiple: " << std::endl;

    //Print the values and at the same time do calculations of least common multiple.
    for (auto i = leastCommonMultiple.begin(); i != leastCommonMultiple.end(); ++i){
        //On first iteration store value of first value inside the vector to iLCM, preventing multiplication by zero incidents.
        if(i == leastCommonMultiple.begin()){
            std::cout << *i << " * ";
            iLCM = *i;
        }
        else if(std::next(i) == leastCommonMultiple.end()){
            std::cout << *i;
            iLCM *= *i;
        }
        else{
            std::cout << *i << " * ";
            iLCM *= *i;
        }
    }

    std::cout << " = " << iLCM << std::endl;
    
};
{% endhighlight %}

Again I have made comments to code and tried to make it as self explanatory as possible. Just to make sure that why those if, else if and else statements are needed. First **if** is for setting the value to variable iLCM, **else if**  is for final value of the vector so that the printout looks clean and finally the **else** is for all the rest of use cases. Again here is main program and print out of that main:
{% highlight cpp %}
//filename: main.cpp
#include "prime.h"

int main(){
        
    Prime prime1(43);
    prime1.PrintFactorization();
    
    Prime prime2(77);
    prime2.PrintFactorization();

    Prime prime3(102);
    prime3.PrintFactorization();
    
    Prime::PrintLCM();
    
    std::vector<int> LCM = Prime::GetLCM();
    
    for (std::vector<int>::const_iterator i = LCM.begin(); i != LCM.end(); ++i){
        std::cout << *i << ' ';
    }
    
    return 0;
}
{% endhighlight %}

Print out:
{% highlight cpp %}
43 cannot be factored down to prime numbers, since it is a prime number itself.
The prime factorization of 77 is: 7 * 11.
The prime factorization of 102 is: 2 * 3 * 17.
Using prime factorization of values to calculate the least common multiple :
2 * 3 * 7 * 11 * 17 * 43 = 337722
//This is the example of getting vector from class and printing it without PrintLCM-method:
2 3 7 11 17 43
{% endhighlight %}

This is the end of second part, but not necessary the end of Prime-class since prime factorization can be used in other situations also. I might come back later and expand upon and maybe use it to find [greatest common divisor][gcd].

-sorhanp
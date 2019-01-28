---
layout: post
title:  "Part 1/2: Performing prime factorization and finding least common multiple in C++"
categories: programming
description: My findings about C++ (CPP, or cpp), Khan Academy, math, mathematics, prime factorization and least common multiple
tags: programming, c++, object-oriented, cpp, math, mathematics
excerpt_separator: <!--more-->
---

[ftoa]:https://en.wikipedia.org/wiki/Fundamental_theorem_of_arithmetic
[prime]:https://en.wikipedia.org/wiki/Prime_number
[commutative_property]:https://en.wikipedia.org/wiki/Commutative_property
[vector]:http://www.cplusplus.com/reference/vector/vector/
[mathisfun]:https://www.mathsisfun.com/prime_numbers.html
[prime_com]:https://en.wikipedia.org/wiki/Prime_number#Computational_methods
[trial_division]:https://en.wikipedia.org/wiki/Trial_division
[pubkey]:https://en.wikipedia.org/wiki/Public-key_cryptography

Prime factorization and least common multiples are two mathematical concepts, which  each has it own applications, meaning that they can be used to solve certain real life problems as well as serve as algorithm in a computer program. Both of them are their own ideas, but they are linked and that is why I have created a class that can handle both of them! Let’s start by prime factorization and then move to least common multiple in part two.<!--more-->

Prime factorization overview 
==================
Before moving on to what prime factorization is, it is essential to understand what [prime numbers][prime] are. They are integers higher than positive one, that are **only divisible** by itself and one. One of the way of finding prime numbers is by inserting elements in stacks that are of **equal size**. If this *cannot* be done, then the amount of elements is a prime number. This can be represented with this picture of eighteen elements and nineteen elements:
![Prime numbers](/assets/prime_numbers.svg)

Of course eighteen elements can be arranged in two stacks where there are nine elements on each of stacks or six stacks with three element each, etc etc. Point being that eighteen is divisible by many numbers other than itself and one, where as number nineteen is not and one element would still be left over with each stack in each situation. Because the nature of prime numbers, there isn’t really an easy solution to find which of the numbers are prime, but more about that later on the programming part. The first ten prime numbers from the beginning are 2, 3, 5, 7, 11, 13, 17, 19, 23, 29. Considering there are infinite prime numbers it is not reasonable to keep listing them further. [This site][mathisfun] has prime numbers up to 1,000 and there is even a calculator to find out which numbers are prime numbers above that. Thanks to that calculator I now know that **4,294,967,291** is a prime number

This brings us to the main topic of prime factorization. It also has fancier name, [fundamental theorem of arithmetic][ftoa] which has two statements, firstly:
>every integer greater than one either is a prime number itself or can be represented as the product of prime numbers

Which means that integer such as 2,147,483,646 equals to 2 * 3 * 3 * 7 * 11 * 31 * 151 * 331, all of which are prime numbers. Another example could be 18, which is product of 2 * 3 * 3. The second statement of the theorem is:
>representation is unique, up to (except for) the order of the factors.

This means when prime factorization is applied, there is only **one unique way** of portraying it. One could argue that this statement could be disputed by placing numbers in different orders, since *order of operation* doesn’t matter when multiplying. It is true that multiplication operation has [commutative property][commutative_property], thus 3 * 3 * 7 * 11 * 31 * 151 * 331 * 2 still equals 2,147,483,646. What the statement declares is that when prime factorization is applied to 2,147,483,646 there will be always be one 2, two 3s, one 7, one 11, one 31, one 151 and one 331 and **no other prime numbers**. Bottom line: *Rearranging the numbers is not unique representation*.

Program for prime factorization
==================
With the theory of prime numbers and prime factorization out of the way, now it is time for programming. I decided that best way to start implementing prime factorization is in a form of a class, that way this same class can be broaden to also include least common multiples, or anything else that has to do with prime numbers. First, here is declaration a of class Prime:
{% highlight cpp %}
//filename: prime.h
#include <iostream>
#include <vector>

class Prime{
    private:
    //Private data members
    int originalValue;
    bool isPrime;
    std::vector<int> factorization;
    
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
    //Returns vector factorization to the user
    std::vector<int> GetFactorization() {return factorization;}
};
{% endhighlight %}

And, here is implementation a of class Prime:
{% highlight cpp %}
//filename: prime.cpp
#include "prime.h"

void Prime::Factorization(){
    
    //Declare variable value and initialize it with private data member originalValue so that when factorization is done, original value is not lost
    int value = originalValue;

    //Declare and initialize for smallest possible prime factorization
    int primeFactor = 2;

    //Factor the number into smaller factors via loop that goes on as long as value is smaller than primeFactor
    while (primeFactor < value){
        
        //If value doesn't have a remainder store primeFactor to vector
        if(value % primeFactor == 0){
            //Divide value by primeFactor and store the quotient to value
            value /= primeFactor;
            factorization.push_back(primeFactor);
            //If value can be divided by anything other than itself or one it is no longer prime
            isPrime = false;
        }
        //If there is a remainder, increment primeFactor by one.
        else{
            primeFactor++;
        }

    }
    
    //If value is not a zero it means that the remainder is a prime number so it must be also stored to vector
    if(value != 0){
        factorization.push_back(value);
    }

};

void Prime::PrintFactorization(){
    
    //Different printout depending if value is prime
    if (isPrime == false){
        std::cout << "The prime factorization of " << originalValue << " is: ";

        for (auto i = factorization.begin(); i != factorization.end(); ++i){

            if(std::next(i) == factorization.end()){
                std::cout << *i << "." << std::endl;
            }
            else{
                std::cout << *i << " * ";
            }
        }
    }
    else{
        std::cout << originalValue << " cannot be factored down to prime numbers, since it is a prime number itself." << std::endl;
    }
    
};
{% endhighlight %}

The code itself is commented and pretty much and self-explanatory enough so I will not be covering it line by line. This program uses [vectors][vector], since they are arrays that can change in size after their initialization. This is very effective, because there is no way of knowing beforehand how many prime factors they are going to be. I will cover vectors in later blog post and much better detail than just “arrays that can be expanded”. Prime numbers are also tricky since there is no actual way of calculating it [via simple equation][prime_com] and the way of finding prime numbers, that is used in this program is called [Trial division][trial_division]. As the name suggested only way of truly knowing is by testing if it really is prime or not by doing division by smaller numbers. For this reason [cryptography][pubkey] is based around prime numbers.

Finally here is main.cpp that initializes two objects with custom parameters from prime class and prints their factorization:
{% highlight cpp %}
//filename: main.cpp
#include "prime.h"

int main(){
    
    Prime prime1(154266);
    prime1.PrintFactorization();
    
    Prime prime2(154277);
    prime2.PrintFactorization();
    
    std::vector<int> factorization = prime1.GetFactorization();
    
    for (std::vector<int>::const_iterator i = factorization.begin(); i != factorization.end(); ++i){
        std::cout << *i << ' ';
    }
    
    return 0;
}
{% endhighlight %}

Printout of the program when it is run:
{% highlight cpp %}
The prime factorization of 154266 is: 2 * 3 * 7 * 3673.
154277 cannot be factored down to prime numbers, since it is a prime number itself.
//This is the example of getting vector from object and printing it without PrintFactorization-method.
2 3 7 3673
{% endhighlight %}

On next post I will be expanding this class to include finding least common multiple and of course go through the overview of what it means to find least common multiples.

-sorhanp
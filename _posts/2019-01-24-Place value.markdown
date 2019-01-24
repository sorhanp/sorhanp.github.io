---
layout: post
title:  "C++ and place value"
categories: programming
description: My findings about C++ (CPP, or cpp), Khan Academy, math, mathematics and place value
tags: programming, c++, object-oriented, cpp, math, mathematics
excerpt_separator: <!--more-->
---

[last]:/programming/2019/01/23/Math-and-cpp.html
[place_value]:http://www.montereyinstitute.org/courses/DevelopmentalMath/COURSE_TEXT_RESOURCE/U01_L1_T1_text_final.html
[khan]:https://www.khanacademy.org/
[32bitInteger]:https://en.wikipedia.org/wiki/2,147,483,647#In_computing
[positional_notation]:https://en.wikipedia.org/wiki/Positional_notation
[english_grammar]:https://www.grammarbook.com/numbers/numbers.asp
[finnish_grammar]:https://en.wikipedia.org/wiki/Finnish_numerals#Years
[expanded_notation]:https://www.mathsisfun.com/definitions/expanded-notation.html

In reference to my [last post][last], about learning more mathematics in becoming better programmer. I started my first mathematical module at [Khan Academy][khan], which was about arithmetic properties. It’s first topic was [place value][place_value] in decimal system.<!--more--> Place values are important to grasp, since it is the basis of understanding what values digits from 0-9 represent when they are placed in a line with each other. Sans place value, a string of numbers 2541 would just be two-five-four-one but thanks to place value we can definitely say that this string of numbers is actually two thousand, five hundred and forty one. Decimal system is also sometimes called [base-ten positional numeral system][positional_notation], which is fitting since each of the digits has it own **position** in value notation that represents it worth. This is best represented with a table:

| Place value |  Digit |
|:-:|:-:|
| **Billions** |  |
| **Hundred millions** |  |
| **Ten millions** |  |
| **Millions** |  |
| **Hundred thousands** |  |
| **Ten thousands** |  |
| **Thousands** |  |
| **Hundredths** |  |
| **Tens** |  |
| **Ones** |  |

As can be seen, the higher the **position** the greater the number is. Now, of course there are even higher place values than billions, but I decided to draw the line there because the maximum value that [signed 32-bit integer can hold is 2,147,483,647][32bitInteger]. Now for example if we take that maximum value and place it to the place value table above it would look like this:

| Place value |  Digit |
|:-:|:-:|
| **Billions** | 2 |
| **Hundred millions** | 1 |
| **Ten millions** | 4 |
| **Millions** | 7 |
| **Hundred thousands** | 4 |
| **Ten thousands** | 8 |
| **Thousands** | 3 |
| **Hundredths** | 6 |
| **Tens** | 4 |
| **Ones** | 7 |

It can be read that two is at billions place, one is at hundred millions place, four is at ten millions place etc. all to way to seven which it at ones place. This is to basis how us, humans, decode numbers. We sort of cut the number in convenient slices like in the case of value 2,147,483,647 there are **,**-character after every third place value. Again this is something that us humans do, and in this case certain population of humans, since [English grammar][english_grammar] has difference to [Finnish grammar][finnish_grammar] for example. Because of this programmers must be careful on how to present numbers since in Finnish grammar 2,212 is not the same as in English grammar (way to separate decimals vs. way to separate place value). As can be seen place values has neat connection to grammar in a way how we perceive numbers as a human.

But that is enough about grammar, let’s get to programming. I prepared two versions of a program that splits user entered number in to place value. These programs do not have object-orientation, but they are split up in functions just to make the code bit more clearer, let’s start with simplest function, which is PrintOut():
{% highlight cpp %}
#include <iostream>

unsigned int PrintOut(){
    int value = 0;
    bool validValue = false;
    
    while(validValue == false){
        std::cout << "Please input a value between 1 and 2,147,483,647: ";
        std::cin >> value;
        
        if(value > 0 && value < 2147483647){
            validValue = true;
        }
        else{
            std::cout << "Invalid input" << std::endl;
        }
    }
    
    return value;
}
{% endhighlight %}

This function asks user to input a number between 1 and 2 147 483 647 and checks if it really is among these limitations. If it is not the program says that the input is invalid and asks the number again from the user. Finally the value is then returned to from the function. Next up simple function that is used to determine the length, meaning the amount of numbers, of value user has entered:
{% highlight cpp %}
int FindLength(unsigned int value){
    int length = 1;
    while ( value /= 10 ){
        length++;
    }
    return length;
}
{% endhighlight %}

This function divides the value entered by 10 until it is no longer divisible and each time the loop is run, value of length is raised by one. Starting value of the length is always one, so that if the value is not divisible at all (values from 1-9) they still have length of one. Since the scope of value is only at this function the original value is still stored in the main program that will be later in this post. Main program also sends user input value and length of the value to FindPlaceValue-function, which is used to print out the place value starting from ones all to way up to billions:
{% highlight cpp %}
void FindPlaceValue(unsigned int value, int length){
    
    std::cout << "++++++++++++++++++++++++++++++++++++++++++++++++" << std::endl;
    std::cout << "Here is a place value of each number of " << value << " starting from ones:\n";
    
    for (int i = 0; i < length; i++) {
        unsigned int rem = value % 10;
        value = value / 10;
        
        if (i == 0){
            std::cout << "Ones place value is: " << rem << std::endl;
        }
        else if(i == 1){
            std::cout << "Tens place value is: " << rem << std::endl;
        }
        else if(i == 2){
            std::cout << "Hundredths place value is: " << rem << std::endl;
        }
        else if(i == 3){
            std::cout << "Thousands place value is: " << rem << std::endl;
        }
        else if(i == 4){
            std::cout << "Ten thousands place value is: " << rem << std::endl;
        }
        else if(i == 5){
            std::cout << "Hundred thousands place value is: " << rem << std::endl;
        }
        else if(i == 6){
            std::cout << "Millions place value is: " << rem << std::endl;
        }
        else if(i == 7){
            std::cout << "Ten millions place value is: " << rem << std::endl;
        }
        else if(i == 8){
            std::cout << "Hundred millions place value is: " << rem << std::endl;
        }
        else{
            std::cout << "Billions place value is: " << rem << std::endl;
        }
    }
}
{% endhighlight %}

There is also alternative version of this that is more dynamic, meaning that it doesn’t have multiple if-statements since it just states, that 1. digit is, 2. digit is etc., with this version of the function variable can be bigger than 32-bit and the place value could be over billion:
{% highlight cpp %}
void FindPlaceValue(unsigned int value, int length){
    
    std::cout << "++++++++++++++++++++++++++++++++++++++++++++++++" << std::endl;
    std::cout << "Here is a place value of each number of " << value << " starting from rightmost digit:\n";
    
    for (int i = 0; i < length; i++) {
        unsigned int rem = value % 10;
        value = value / 10;

        std::cout << i + 1 << ". digit is: " << rem << std::endl;
    }
}
{% endhighlight %}

Each of the functions has the same functionality where the modulo operation of 10 is applied to value user has entered, remainder of this operation is stored to rem variable which is then printed to user. Each loop also divides value by 10 so that the digits move one place to the right. This is done until the length of value is met. Finally here is the main-program that calls these functions and sends the values to functions:
{% highlight cpp %}
int main(){
    
    unsigned int userInput = PrintOut();
    int length = FindLength(userInput);
    FindPlaceValue(userInput, length);
    
    return 0;
}
{% endhighlight %}

For example here are one printout of program with FindPlaceValue-function with multiple IF-statements:
{% highlight cpp %}
Here is a place value of each number of 2147483646 starting from ones:
Ones place value is: 6
Tens place value is: 4
Hundredths place value is: 6
Thousands place value is: 3
Ten thousands place value is: 8
Hundred thousands place value is: 4
Millions place value is: 7
Ten millions place value is: 4
Hundred millions place value is: 1
Billions place value is: 2
{% endhighlight %}

Another example of program with FindPlaceValue-function which is more dynamic:
{% highlight cpp %}
Here is a place value of each number of 2147483644 starting from rightmost digit:
1. digit is: 4
2. digit is: 4
3. digit is: 6
4. digit is: 3
5. digit is: 8
6. digit is: 4
7. digit is: 7
8. digit is: 4
9. digit is: 1
10. digit is: 2
{% endhighlight %}

That is how place value can be utilized in simple C++ program, this may come handy in programs where data has to presented in certain way, such as in [expanded notation][expanded_notation], speaking of which is the the topic of next post.

-sorhanp
---
layout: post
title:  "Expanded form and expanded notation using C++"
categories: programming
description: My findings about C++ (CPP, or cpp), Khan Academy, math, mathematics, expanded notation and expanded form.
tags: programming, c++, object-oriented, cpp, math, mathematics
excerpt_separator: <!--more-->
---

[last]:/programming/2019/01/24/Place-value.html
[expanded_notation]:https://www.mathsisfun.com/definitions/expanded-notation.html
[multdivten]:http://everydaymaths.co.uk/place-value-multiplying-and-dividing-by-ten-and-the-importance-of-zero/

[Last time][last] I ended the post with little teaser about [expanded notation][expanded_notation], which is basically just way of presenting numbers as their place value so instead of writing 2,541, the place value of each digit is expressed as an addition: 2000 + 500 + 40 + 1, or alternatively (2 * 1,000) + (5 * 100) + (4 * 10) + (1 * 1). The former is called expanded form while the latter is expanded notation. Using either of these methods the true place value of each digit is portrayed.<!--more--> In short this is just another way of expressing numbers, although not as common as simply writing the whole number.

This can be programmed rather easily by expanding the place value program that was presented on [my last blog][last] so the PrintOut- and FindLenght-functions are identical to last time, asking for value between 1 and 2 147 483 647 and then counting the length of that value. After that, a new ExpandedForm-function is called with entered value and length parameters and this is how the number is transformed into expanded form:
{% highlight cpp %}
void ExpandedForm(unsigned int value, int length){
    
    //Initialize an array of integers that holds as many elements as there are amount of digits. Initialize elements to zero.
    int arrayExpandedForm[length] = {0};
    
    std::cout << "++++++++++++++++++++++++++++++++++++++++++++++++" << std::endl;
    std::cout << "Here is " << value << " written in expanded form:\n";
    
    for (int i = 0; i < length; i++){
        //Apply modulo operation of 10 to value to "extract" rightmost digit to variable rem
        unsigned int rem = value % 10;
        
        //Raise the remainder by 10 to power of current loop to add zeros to value
        for(int j = 1; j <= i; j++){
            rem *= 10;
        }
        
        //Store value to array
        arrayExpandedForm[i] = rem;
        //Divide value by 10 to “remove” rightmost digit
        value = value / 10;
    }
    
    //Print array
    for (int i = length - 1; i >= 0; i--){
        if (i == 0){
            std::cout << arrayExpandedForm[i] << std::endl;
        }
        else{
            std::cout << arrayExpandedForm[i] << " + ";
        }
        
    }
    
}
{% endhighlight %}

Alternatively here is the function for Expanded notation:
{% highlight cpp %}
void ExpandedNotation(unsigned int value, int length){
    
    //Initialize an array of integers that holds as many elements as there are amount of digits. Initialize elements to zero.
    int arrayExpandedNotation[length] = {0};
    
    std::cout << "++++++++++++++++++++++++++++++++++++++++++++++++" << std::endl;
    std::cout << "Here is " << value << " written in expanded notation:\n";
    
    for (int i = 0; i < length; i++){
        //Apply modulo operation of 10 to value to "extract" rightmost digit
        unsigned int rem = value % 10;
        
        //Store value to array
        arrayExpandedNotation[i] = rem;
        
        value = value / 10;
    }
    
    
    //Print array
    for (int i = length - 1; i >= 0; i--){
        
        unsigned int rem = 1;
        
        //Raise the remainder by 10 to power of current loop to add zeros to rem variable to represent expanded notation
        for(int j = 1; j <= i; j++){
            rem *= 10;
        }
        
        if (i == 0){
            std::cout << "(" << arrayExpandedNotation[i] << " * " << rem << ")" << std::endl;
        }
        else{
            std::cout << "(" << arrayExpandedNotation[i] << " * " << rem << ")" << " + ";
        }
        
    }
    
}
{% endhighlight %}

Both of functions has pretty much the same idea behind them, which is to “extract” the last digit from the value and then storing it to array for later use. Difference only being when the zeros are added. On the expanded form zeroes are added on the first loop after the extraction of the rightmost digit, and on expanded notation it is done when printing the values to user. I’m really glad that I got acquainted with each of these ways of representing numbers since they also had to make me use other mathematical ideas such as [Multiplying and dividing by ten][multdivten], which are used for “moving” the place value from one place to another or even adding zeros to value.

In the very end, here are print out from both of the functions:
{% highlight cpp %}
//Expanded form:
Please input a value between 1 and 2 147 483 647: 2147483644
++++++++++++++++++++++++++++++++++++++++++++++++
Here is 2147483644 written in expanded form:
2000000000 + 100000000 + 40000000 + 7000000 + 400000 + 80000 + 3000 + 600 + 40 + 4

//Expanded notation:
Please input a value between 1 and 2 147 483 647: 2147483644
++++++++++++++++++++++++++++++++++++++++++++++++
Here is 2147483644 written in expanded notation:
(2 * 1000000000) + (1 * 100000000) + (4 * 10000000) + (7 * 1000000) + (4 * 100000) + (8 * 10000) + (3 * 1000) + (6 * 100) + (4 * 10) + (4 * 1)
{% endhighlight %}


-sorhanp
---
layout: post
title:  "Exponents raised to the power of C++^2"
categories: programming
description: My findings about C++ (CPP, or cpp), Khan Academy, math, mathematics, exponents, raised to power, c++ mathematics, c++ maths, c++ exponent rules and properties
tags: programming, c++, object-oriented, cpp, math, mathematics, exponent, exponents, raised to power,
excerpt_separator: <!--more-->
---

[last]:/programming/2019/03/06/Exponents-raised-to-the-power-of-C++.html
[exponents_rules]:https://www.rapidtables.com/math/number/exponent.html#rules
[wiki_product]:https://en.wikipedia.org/wiki/Product_(mathematics)
[wiki_commutativeproperty]:https://en.wikipedia.org/wiki/Commutative_property
[wiki_quotient]:https://en.wikipedia.org/wiki/Quotient
[polydiv]:https://www.purplemath.com/modules/polydiv.htm
[wiki_solving]:https://en.wikipedia.org/wiki/Equation_solving
[wiki_square]:https://en.wikipedia.org/wiki/Square_root

Continuing from the [last post][last], here is a overview of [rest of the the properties][exponents_rules] that exponents have to offer. Before going on any further I want to start by making the terminology clear for the rest of this blog post. **Base** is the value that is multiplied by itself as many times as the *exponent* declares, in the case of **5**^*3*, the number **5** is the base and *3* is the exponent. The result of this expression is called either product, or power. I also would like to point out that the code examples here are, well examples, they represent the raw idea on how to perform simplified calculations, nothing more.<!--more-->

Exponent property: Rules of product 
==================
Continuing from the first paragraph, in mathematics [product][wiki_product] is also result of multiplying, meaning that product of 5 and 4 is 20 (5 * 4 = 20). Which is really sensible, since what is happening is multiplication, thus the rules that apply here are based on rules of multiplication. In the case of exponents, there are two rules related to multiplication of two base values with exponents. First, when the base values are identical, addition can be applied to their exponents. Considering this rule, the expression 2^3 * 2^4 can be simplified to 2^3+4, which can be simplified even further to just 2^7. Why this works is [the commutative property][wiki_commutativeproperty] of multiplication, which states that 4 * 5 is the same as 5 * 4. When deconstructing 2^3 * 2^4 to how many times the base is multiplied together, the end result looks like this; 2^3 -> (2 * 2 * 2) and 2^4 -> (2 * 2 * 2 * 2), thus the expression 2^3 * 2^4 = (2 * 2 * 2) * (2 * 2 * 2 * 2) = 2 * 2 * 2 * 2 * 2 * 2 * 2 = 2^7. This rule can be used to, for example simplify user inputs on a program that expects two multiplication from user, and detects that there are two identical bases:
{% highlight cpp %}
    int base_input1 = 2;
    int base_input2 = 2;
    int exponent_input1 = 3;
    int exponent_input2 = 4;
    int power = 0;
    
    if(base_input1 == base_input2){
        int exponent = exponent_input1 + exponent_input2;
        power = base_input1;

        for(int i = 1; i < exponent; i++){
            power *= base_input1;
        }
    }
    else{
        /* If bases are different,
        first calculate the power of both inputs and
        then multiply both power to receive answer
        */
    }
{% endhighlight %}
Like seen on the example above, without this rule of product there would have to be much longer calculations, first run for-loop for  base_input1 and then base_input2 and only after that multiply the result of those powers.

Second product rule follows the logic of the second rule, but this time it states that if exponent of bases that are being multiplied are identical, then the multiplication of bases can be done first and lastly apply the exponent to the product. So according to this rule 2^3 * 3^3 = (2 * 3)^3. Why this works is yet again tied to commutative property. Deconstructing the expression 2^3 * 3^3 to (2 * 2 * 2) * (3 * 3 * 3) =  2 * 2 * 2 * 3 * 3 * 3. So in the end there is always three 2’s and three 3’s. Because of commutative property the numbers can be thrown around freely and the end result will not change, 2 * 2 * 2 * 3 * 3 * 3 = 3 * 3 * 3 * 2 * 2 * 2 = (2 * 3) * (2 * 3) * (2 * 3), which can be just simplified to (2 * 3)^3, which can be read as 2 times 3 three times.

Expanding the code block above there could be else if-statement for cases where the exponents are same:
{% highlight cpp %}
    else if(exponent_input1 == exponent_input2){
        int exponent = exponent_input1;
        power = base_input1 * base_input2;
        
        for(int i = 1; i < exponent; i++){
            power *= base_input1 * base_input2;
        }
    }
{% endhighlight %}

Again, like last post, here is a table with rules explained:

| Rule  | Equation | Example simplification |
|:-:|:-:|:-:|
| Product rule with same base | a^y * a^x = a^y+x = a^z | 5 * 5^3 = 5^1+3 = 5^4 |
| Product rule with same exponent | a^x * b^x = (a * b)^x = c^x | 5^2 * 6^2 = (5 * 6)^2 = 30 ^ 2 |

What is important to realize, is that the rules also can go backwards, so a^z can be also split in to a^x * a^y. This can be useful in pure mathematical cases where there might be reason to simplify big expressions but before that is even possible there might be need to express some cases differently.

Exponent property: Rules of quotient 
==================
In mathematics [quotient][wiki_quotient] is the result of division, so in the case of 20 and 4 the quotient is 5, (20 / 4 = 5). Since division is the inverse operation of multiplication the rules of quotient are opposite to the rules of product, so when the base values are identical, subtraction can be applied to their exponents. Thus 2^4 / 2^3 can be simplified to 2^4-3. Justification for this is how [divisions can be simplified][polydiv]. Again let’s deconstruct expression 2^4 / 2^3. 2^4 becomes 2 * 2 * 2 * 2 and 2^3 = 2 * 2 * 2 so the whole expression is 2 * 2 * 2 * 2 / 2 * 2 * 2, it is possible to reduce the division by cancelling out the duplicates on both side of the expression, which mean that in this case that three 2’s can be reduced from both sides: ~~2 * 2 * 2~~ * 2 / ~~2 * 2 * 2~~, resulting 2 = 2^4-3 = 2^1. 

Like product rules in the previous heading, quotients also have rule for identical exponents, which states that 10^2 / 2^2 = (10 / 2)^2 =  5^2. This works because divisions have important property known as *equality*, which states that whatever is done to the right side of equation, must also be done to left side of equation to keep the *equality*. This property is used to [solving equations][wiki_solving] among other things. So in this case both sides of the equation are raised to 2th power, which results in equation 100 / 4 = 25 = 5^2. As seen, because of equality rule, it does not matter if the exponent is applied before or after the division. For human it is of course always easier to think with smaller numbers, thus first dividing 10 by 2 and after that rising the result to the 2th power is simpler to understand.

Again both of these rules can be used on a program to simplify calculations:
{% highlight cpp %}
    int base_input1 = 10;
    int base_input2 = 2;
    int exponent_input1 = 2;
    int exponent_input2 = 2;
    int power = 0;
    
    if(base_input1 == base_input2){
        int exponent = exponent_input1 - exponent_input2;
        power = base_input1;

        for(int i = 1; i < exponent; i++){
            power *= base_input1;
        }
    }
    else if(exponent_input1 == exponent_input2){
        int exponent = exponent_input1;
        power = base_input1 / base_input2;
        
        for(int i = 1; i < exponent; i++){
            power *= base_input1 / base_input2;
        }
    }
    else{
        /* If bases are different,
        first calculate the power of both inputs and
        then divide both power to receive answer
        */
    }
{% endhighlight %}
Here is a table with rules explained, again these can be used “backwards” too, so 5^2 can also be expressed as 5^4 / 5^2 if needed:

| Rule  | Equation | Example simplification |
|:-:|:-:|:-:|
| Quotient rule with same base | a^y / a^x = a^y-x = a^z | 5^4 / 5^2 = 5^4-2 = 5^2 |
| Quotient rule with same exponent | a^x / b^x = (a / b)^x = c^x | 20^2 / 5^2 = (20 / 5)^2 = 4^2 |

Exponent property: Rules of power 
==================
Powers, or powers of powers, have many rules, some of which include [square roots][wiki_square]. I will omit these for time being and focus on two rules that follow along the same line as previous two properties. Starting with first rule of power, which states that to raise *a power* to **a power** is same as applying product of the exponents to the base. So for example expression (2^3)^4, which can be read as 2 times itself *3 times*, **4 times**,  can be simplified to 2^*3****4** = 2^12 according to this rule. Why this rule makes sense becomes clear when, expressed like this; 2^3 * 2^3 * 2^3 * 2^3, and finally when expressions is fully deconstructed to just multiplication; (2 * 2 * 2) * (2 * 2 * 2) * (2 * 2 * 2) * (2 * 2 * 2). 

Second rule of powers is very closely related to the first. However second rule states that rising base’s to exponent to a power is same as rising the base to product of exponent to the power. Sounds bit complicated, but is far from, since it looks like is this: 2^(3^4). At first glance seem to be the same as the first rule, but ()-parentheses are in different place, thus what happens in this case is exponent itself is raised to the fourth power; 2^(3 * 3 * 3 * 3) = 2^81. So it is very important to understand difference between these rules and observe the place where parentheses are placed, since the different in values between these two equation is **massive**. Finally let’s apply these two rules to a program:
{% highlight cpp %}
    int base_input = 2;
    int exponent_input1 = 3;
    int exponent_input2 = 4;
    bool PowerToPower = false;
    long long power = 0;
    
    if(PowerToPower == true){
        //Multiply exponent by the power
        int exponent = exponent_input1 * exponent_input2;
        power = base_input;

        for(int i = 1; i < exponent; i++){
            power *= base_input;
        }
    }
    else{
        power = base_input;
        int exponent = exponent_input1;

        //Raise the exponent to exponent_input2:th power
        for(int i = 1; i < exponent_input2; i++){
            exponent *= exponent_input1;
        }
        
        //Apply the raised exponent to base
        for(int i = 1; i < exponent; i++){
            power *= base_input;
            std::cout << power << std::endl;
        }
    }
{% endhighlight %}
Again the logic is pretty much the same as before, BUT on the cases where the second rule is applied what happens first is rising exponent to power stored inside exponent_input2. The result being 2^81 where even the long long-variable cannot hold the final value since it is 2,4178,5163,9229,2583,4941,2352.00 and the maximum exponential value of 2 that can be stored to unsigned long long is 922,3372,0368,5477,5808.00, which is same as 2^63. Finally time for one more table:

| Rule  | Equation | Example simplification |
|:-:|:-:|:-:|
| Power to power-rule | (a^x)^y = a^x * y | (4^3)^2 = 4^3 * 2 = 4^6 |
| Exponent to power-rule| a^x^y =  a^(x^y) | 4^3^2 = 4^(3^2) = 4^9 |

A word about negative exponent and how to utilize exponential rules
==================
I touched on the subject of negative exponents on my last post, such as what it means to apply negative exponents to base (dividing number 1 by base as many time as exponent indicates). However in mathematics it is much simpler to have only positive exponents when solving complex expressions. Negative exponents can be turned to positive by simple rule; negative exponents are multiplicative inverse of positive exponents and vice versa. Simply put 2^-3 = 1 / 2^3. Why this work is because, like said, negative exponents are the same as dividing number 1 by base as many time as exponent indicates, thus 2^-3 is same as 1 / (2 * 2 * 2). Again this same can be expressed with multiplicative inverse, which states that dividing by x is same thing as multiplying by 1 / x. Common sense way of thinking, and great way to remember this is just to say: “dividing by 2 is same as multiplying by half”, thus 1 / (2 * 2 * 2) = 1 * (1 / 2) * (1 / 2) * (1 / 2) = 1/8 = 2^-3.

These rules make thinking of programming algorithm much simpler, rather than spending long time of solving something by brute force techniques. Think of problem like 2^3 / 6^-2 * 5^-2 * 4^-2 * 3^-2 * 2^-2, sure it is possible to just input all these values to C++ -program with variables and start calculating them one by one, or rather yet, start input this to a calculator yourself and see how long does it take? But what if instead first simplify the problem by first applying the product rule with same exponent:  2^3 / (6 * 5 * 4 * 3 * 2)^-2  = 2^3 / 720^-2. Now the expression looks much cleaner, but wait, there's more. How about using the negative rule to make negative exponent positive, by flipping the problem like this: 2^3 * 720^**2** / 1. Which then can be finally simplified just to 8 * 518400 / 1 and since dividing by 1 has no effect on the result the final answer is 4147200. Cases like 2^3 * 720^2 are much simpler to input to a calculator and like said, make simpler algorithm rather than just brute forcing the answer, which can waste precious computing resources on user’s computer. I will demonstrate this more thoroughly on my next blog post.

-sorhanp
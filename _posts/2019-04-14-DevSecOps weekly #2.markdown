---
layout: post
title:  "DevSecOps weekly, second issue"
categories: programming
description: My findings about DevSecOps, DevOps, Service Design, learning diary, modern software development, cloud services and agile
tags: programming, DevSecOps, DevOps, modern software development, agile, cloud services, service design
excerpt_separator: <!--more-->
---

[last]:/programming/2019/04/07/DevSecOps-weekly-1.html
[service_design]:https://www.interaction-design.org/literature/article/the-principles-of-service-design-thinking-building-better-services
[stefan]:http://www.stefan-moritz.com/
[tools]:https://www.designorate.com/4-service-design-tools/
[porter]:https://www.mindtools.com/pages/article/newSTR_82.htm
[brainstorming]:https://www.mindtools.com/brainstm.html
[conjoint_analysis]:https://www.qualtrics.com/experience-management/research/types-of-conjoint/
[scenario_thinking]:https://www.scenariothinking.org/index.php?title=What_is_Scenario_Thinking%3F
[service_blueprint]:https://www.lucidchart.com/blog/what-is-a-service-blueprint
[bootstrap]:https://bootstrapstudio.io/
[forbes]:https://www.forbes.com/sites/forbesagencycouncil/2017/10/24/18-steps-to-take-before-you-launch-a-product-or-service/#4040a8d19cf9
[measuring]:https://www.thebalancecareers.com/you-can-t-manage-what-you-dont-measure-2275996
[study]:https://aaltodoc.aalto.fi/handle/123456789/3931
[web_course]:https://www.jamk.fi/fi/Koulutus/Avoin-AMK/Koko-opintotarjonta/ICT/web-ja-ohjelmistotekniikka/
[fullstackopen]:https://fullstackopen-2019.github.io/
[nodejsinaction]:https://www.amazon.com/Node-js-Action-Mike-Cantelon/dp/1617290572
[book_think_programmer]:https://www.goodreads.com/book/show/13590009-think-like-a-programmer
[sliding_puzzle]:https://en.wikipedia.org/wiki/Sliding_puzzle

Two weeks of studies and the results are in. I have crafted my path and now it is time to start following through the plan. This week I have learned more on how to think like a programmer, returned to study more mathematics, so that I can pass he entrance exams. This week on the lectures I got insight on Cloud Services and Service Design. <!--more-->

Designing a service
==================
I start with the most recent thing on my mind, which is **Service Design**. It is something that I have heard of, but never actually committed my time to fully learn what it really means (I even think I have started a MOOC on it but due time limits did not really start it). Now I feel, that I should have spent at least some time learning about it in the past. I say this because it makes perfect sense to implement it in the software development environment. First of all what does [Service Design][service_design] mean? Well it is a way of implementing end-user's needs to the development process of a good or a service (I will use product from now on). Supposedly It is also a never-ending process in a sense that when end-user receives the product, it is crucial to also start thinking what kind of updates the product needs. Is the process itself relevant anymore? What could be done better according the feedback? How is this related to modern DevOps-ideology? However let’s not get ahead of things. Keeping things in chronological order it is time to start from the beginning.



It is also important to notice that Service Design is a very agile process, since it is not standardized in any means and it’s a very fresh concept. However there are general direction on how the process usually goes, and they are as follows: define => investigate => design => develop => ship. Like said, since this is not a standard and being agile the order might change and there might be even little steps inside these steps depending on the situation. I found that using these five steps it can describe the whole process in most efficient way, without sidelining too much to little details. This is also how I understood the concept the best. Since this is a little analysis on what Service Design is and how it fits modern software development, I recommend [Service Design, 
Practical Access to an Evolving Field e-book][stefan] for further reading to fully understand the nitty-gritty details.

Define
------
Defining in this context means finding out what the problem, or rather is there a even a problem, that needs solving? This is the phase where customer might have an “perfect”, ready defined answer, answer or no clue, depending on the level of knowledge customer have about these things. To both of these there are perfect tools on how to start defining. If the customer has a “perfect” answer it should be questioned, since there usually is a hidden **root cause** for that pre-made answer, that the customer is using. However if the customer doesn’t really know, well then there is the process of Service Design at your disposal. So why define anything, even going so far to bother the customer by asking questions until “root cause” is found? Reason is pretty simple, in order to give customer what is needed, it is important to know what that something is, since it is the basis of Service Design.

Define-phase also includes little pre-investigation before moving to the investigate part itself. This is done before going on to full on investigation mode, to find out what kind client we are dealing with. These include but not limited to the vision / mission, strategy, competitor analysis, legality of the product itself. To put it simply this investigation is used to determine if what client needs is even viable to develop. For example, if there is some legal aspect that prevents releasing what client needs, then whole lot of resources were wasted if it is noticed at any other step.

Investigate
------
Also known as “get your hands dirty and do some detective work before rushing headfirst down a cliff”-part. While there is some basic investigatory work on define section as stated, this part is where the magic of Service Design happens. Meaning that this is the part where it is time to listen to expectation, needs and requirements of the end user of the product in question. Okay, sounds enough enough but sometimes it is hard to find out exact information. No worries, there are tools for that, such as interviews and observations. Again with these the sky's the limit, since there are many kind of methods for “accessing the mindset” of the user. However it is important to know **how** and **what** kind of data is necessary to collect, which both can be big hurdles. On *how* part, maybe the interview questions are not objective enough and steer the end user to answer untruthful. Also how to get end-user(s) to participate, since filling out questionnaires is not the most favourite past-time ever. On *what* part, there might be observations that do not reflect the real user cases, this might happen if the observation period is too short, or wrong people are being observed.

When investigating focus is also on strategic planning. The goal being to find out how the product fits to strategy of organization and how organization handles the competition on it’s market with this new product. See [Michael Porter’s competitive strategies], which states that there are three different ways how to compete on the market:
- Price
- Differentiate
- Niche 

In short: Is the product cheaper than the rest? Does the product does something different than the rest? Is the product so specific that there is no competition? This is also the point where it is important to find out if users really use the product, for example if there might be people who do not want to adapt to change and resist using the service.

Design (as in planning)
------
Now that the project has a direction, it is time to start planning. In Service Design planning begins with a [brainstorming][brainstorming], in which solutions to the problem are being thrown around without too much criticism. Quantity is quality in this situation, and after enough ideas are gathered (or time has passed) it is time to start thinking which of them a viable. Usually there might be even similar solutions that can be combined to form one. Again this process is very agile and there might be even multiple brainstorming sessions with many diverse groups of users, since changes are that if enough of time is spend thinking solutions without too much criticism the best answer will be found. The chosen idea(s) is/are then formed to a conception, which is a further visualized version of the idea(s). Tools for presenting conception are [conjoint analysis][conjoint_analysis], [scenario thinking][scenario_thinking], and [service blueprint][service_blueprint]. The benefit of said tools is the ability to understand basic concepts of the product even before there is even working prototype. Kinda like a prototype of a prototype.

Speaking of prototypes, Service Design has a very essential phase called prototyping. That means building a fast model that shows how the product is supposed to work. It helps development and brings more insight on features of the product. More importantly prototyping can unveil what kind of features are not necessary, or even wanted. Thinking this from viewpoint of programming, a prototype can be build without needing to write to be single line of code, or by writing a bare minimum amount of code with frameworks such as [Bootstrap][bootstrap]. Bottom line is: **prototyping minimizes risk of going in wrong direction when developmenting a product**.

Develop
------
Now that the product has been specified and prototyped it is time to start building the actual product. Another essential part of Service Design is **continuous development**. Aha! There is the link to DevOps, but more about that later on my “closing statement”. Piloting is a way to do continuous development, in which end user receives a unfinished product (Pre-Alpha, Alpha… etc. in software development), and feedback is gathered on experience. Secondary goals of piloting are to rise interested and knowledge about the product, also known as building the hype. Again, like in investigation part, it is important to know  *how** and **what** kind of data is necessary to collect. Ideal situation is to get to see hands-on reaction from the end user, but again, the sky's the limit and there might be questionnaires, workshops, anything to get info about the user’s encounter with the product, before launching. Again this process can be very agile and iterative, meaning that feedback can be gathered on multiple point of development (even during different parts of beta-version) and feedback on each iteration is used to improve the product before release. This is used to combat the release day problems, such as non working or unstable products, which could affect the perception of the product, or even the developer.

Ship (as in launch)
------
Hype has been building since the beta-periods and this is the moment, release of the product. Fact is that even the worlds best product won’t sell itself, so some sort of promotion is always necessary. Examples of this include some sort of “soft-launch”, where concise version of product is released, maybe for selected few get to enjoy the product, thus rising the hype even more. Another example is good old advertisement, where the product is being shown to the focus group. As this phase depends heavily on the product itself it is very hard to have one magic pill that solves all promotion problems. To this I say, know your product and present it with correct tools by researching. [Forbes][forbes] has a list and Internet is full of examples on how to do successful launch and how to avoid pitfalls. To be agile, is to be conscious. Be aware of surroundings and learn from others mistakes! Like with all business processes, it is important to be able to [measure performance][measuring]. This goes with Service Design too and since these measurements can be used to gather information for long periods of time it is possible to find out information on how to further improve the product. Making the Service Design never-ending process that aims to deliver better and better product with each iteration.

Closing statement
------
I had interesting morning learning about Service Design, especially with freeform discussion between lecturer and the audience. Especially when talking about how this can be fitted in with modern agile software development with likes of DevOps etc, since the model of Service Design flows from one phase to another, just like in waterfall model, which [I discussed last time][last]. This is something that has been discussed, but not fully realized yet. What I found interesting was this [thesis by Markus Koljonen][study] that describes a conflict in Agile and Service Design relationship:
>...different design fields contradicting to some extent; and agile methodology partly conflicting with service design thinking.

One such conflict is is the fact that agile model expects that there is good understanding of the users and the business without ever questioning them. However since the similarities are also present the author also believes that these two ideologies can enrich each other along the way and that is just matter of layering them together. This might be something worth looking into more in detail in the future, maybe even a form of my own thesis. For now I believe that, since agile development places so much trust in the understanding of users and business it would be perfect fit to combine the two. First utilizing this waterfall model until everything is gathered and when the software design starts, switch gears in to more agile way of doing. I think that is possible to start with very few collaborators, in example only with consultant along with very few software developers that does the preliminary mapping on design and investigate part with the customer and when all the pieces are in place, software production company joins in full force for design and finally when developing starts. This is where both ideologies match perfectly, because both of them are iterative, looking to improve the product in small “sprints”, which they are called in Agile development. Also as the continuous improvement is one of the cornerstones of DevOps [(CI / CD)][last] it would be wise not to at least start trying to find ways to fit Service Design in software projects.

The path
==================
I also had a change to meet my mentor this week and what a lively discussion we had! I first had a discussion about what I’m currently doing, which is of course spent time with the DevSecOps mandatory studies such as introduction to cloud services, which started this week. But rest of the time I have been getting ready for entrance exams that are just around the corner. I have decided to use my weekends to study each years entrance exams to find out which areas of my knowledge need more “maintenance”. Mentor was happy to hear that I’m preparing and for now cut me some slack so that I can focus on getting to my next seat of learning. I’m really happy about the opportunity and will use this to my advantage for the next couple of weeks. Anyway, back to the discussion that we had. Since this DevSecOps-training also has a on-the-job learning, he also asked what kind of work I’m currently looking on. I have come to conclusion that I’m really interested in back-end development, since I never really have had an eye to user interface design. So far I have send one application for trainee position, which included basic programming and database skills. To further drive this home I have also started planning my programming a little further by applying the knowledge of the “How to think like a programmer”-book to my daily programming. I will post example of that under next header. 

Our discussion moved on the what I’m planning to take us optional studies. I have already picked up [web and software technology intensive course][fullstackopen] (Warning: Finnish content!) so that I can learn more deeply on web development. Since it is going to start in next month. Mentor also talked about [Full Stack Open 2019][fullstackopen] (again Finnish) that is free, study on your own pace lectures on React, Redux, Node.js, MongoDB ja GraphQL. I also told that I have been reading [Node.js in Action 1st Edition][nodejsinaction], so that I have something do before I start the intensive course. We will plan further next time we will meet.

Think like a programmer example
==================
I have done some reading of the [Think Like a Programmer: An Introduction to Creative Problem Solving][book_think_programmer] book to also get ready for my entrance exam, since it has good information how to break down problems in the smaller “sub-problems”. The book talked about sliding puzzle and how to solve them and that made me think. How about I start thinking of an algorithm for solving slide puzzle on my own. This is my progress so far, and it is very much work in progress.

## Objective
Create a sliding puzzle algorithm for solving 5, 8, 15 or higher number puzzles. 

## Planning
1. Create a two-dimensional array to simulate 3x3, 4x4, 5x5 etc puzzle by entering values to [][] array
2. Randomize numbers between 5,8,15 etc. depending on the size of the puzzle
3. Use the "human way" of solving so that first line is solved first, then the the leftside and, thus reducing the puzzle from 5x5 -> 4x4
4. First by C++ (to learn algorithm) then graphical program to web where one can solve it him/herself or by clicking "autosolve"

## Printout
Example of 15-puzzle(4x4):

| 5 | 4 | 8 | 14 |
|---|---|---|---|
| **13** | **6** | **12** | **1** |
| **2** | **11** | **3** | **15** |
| ***0*** | **7** | **9** | **10** |

## Algorithm planning

Basic rules:
1. Zero(empty square) can only switch places with other numbers. Switching can only done to right, left, up and down.
2. All the values can be seen all the time, but no value is allowed to be moved unless rule 1 is true, meaning that at the starting position (seen above) only 2 and 7 can be moved.

Initial setup:
1. curretNumber is set to 1
2. Find location of currentNumber, if it is in it's correct location (for example 1 at [0][0]) add one to currentNumber and then move to loop. Otherwise move to loop without adding.

Loop:
1. Zero switches places with other values until currentNumber is found either from sides (left or righ) or above or below.

After number has been place in its correct position
1. Move on the next number and revert back to loop

Final loops:
1. Zero must be at the bottom rightmost square at the end of the algorithm and the end at the end algorithm printout should be as follows:

| 1 | 2 | 3 | 4 |
|---|---|---|---|
| **5** | **6** | **7** | **8** |
| **9** | **10** | **11** | **12** |
| **13** | **14** | **15** | ***0***  |

"array[ROWS4][COLUMNS4]" is same as :

| 5 | 4 | 8 | 14 |
|---|---|---|---|
| **13** | **6** | **12** | **1** |
| **2** | **11** | **3** | **15** |
|  | **7** | **9** | **10** |

### Bottom line and what’s next?
I Googled a little bit on tips how to solve sliding puzzles and find out a lot of good tips and tricks. I will continue improving upon this design when I have more time, since now I have to focus on my career and studies first. Anyway I believe that above displays very well how to start splitting up the problem before writing a program. Like the book says:

>In solving programming problems, we are sometimes faced with situations where we can’t see a clear path to code the solution, but we must never allow this to be an excuse to forgo planning and systematic approaches. It’s better to develop a strategy than to attack the problem through trial and error.

I absolutely agree, because sometimes I feel like just writing lines of code and randomly changing line here and there doesn’t really further the learning experience, and on the contrary, making it a game of pure luck if the program even works.


-sorhanp
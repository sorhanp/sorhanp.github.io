---
layout: post
title:  "DevSecOps weekly, sixth issue"
categories: programming
description: My findings about Robot Framework, unit testing, integration testing, system testing, acceptance testing, Robotic Process Automation and rpa.
tags: robot framework, unit testing, integration testing, system testing, acceptance testing, rpa, Robotic Process Automation
excerpt_separator: <!--more-->
---

[last]:/programming/2019/05/05/DevSecOps-weekly-5.html
[robot_framework]:https://robotframework.org/
[unit_testing]:http://softwaretestingfundamentals.com/unit-testing/
[culture]:https://sorhanp.github.io/programming/2019/04/28/DevSecOps-weekly-4.html
[int_testing]:http://softwaretestingfundamentals.com/integration-testing/
[req_analysis]:https://reqtest.com/requirements-blog/requirements-analysis/
[libraries]:https://robotframework.org/#libraries
[builtin]:http://robotframework.org/robotframework/latest/libraries/BuiltIn.html
[selenium]:http://robotframework.org/SeleniumLibrary/SeleniumLibrary.html#Shortcuts
[tdd]:http://agiledata.org/essays/tdd.html
[rpa]:https://www.uipath.com/rpa/robotic-process-automation

There has been a huge focus on testing aspect of software development during this week at my training. I learned about different testing types and wrote a simple testing suite using [Robot Framework][robot_framework]. <!--more--> 

Types of testing 
------ 
Classically testing can be categorized very broadly to three groups; unit testing, integration testing and system testing. They grow from smallest to the largest in a sense that unit test is done to certain code, like a function or a class, while system testing is done to the completed application. However more modern software development styles may also call a need for fourth group; acceptance testing. In this blog post I will go through each of these testing type and finally present one live example of a system testing. 

Unit testing 
================== 
[Unit testing][unit_testing] is smallest of the bunch. It tests a single part of code (a unit), be It a function, class or subroutine. Aim of a unit test is to make sure that piece of code is working as expected, lowering the possibility of non-functioning code present in the release of program. These tests are designed to make sure that the program is safe to use, and it doesn’t crash when minor errors are met. Program should not crash when user input words to number field, but rather inform that is not possible to use these characters. Unit tests can be also used to determine if code is doing something unexpected, like deleting existing records while adding new ones.  

So, what kind of programming errors can be expected to find using unit testing Usually they are of smaller scale, since unit tests tend to focus on the smallest of the smallest code blocks, for example in object-oriented programming a single method of a class is tested, thus it usually has only limited amount of inputs and outputs. This is it is also beneficial to the code, since it **must be** modular for unit tests to be efficient. 

Since programmers tend to produce a lot of code, there also must be a lot of unit testing. This is where a good DevSecOps’s Continuous Integration (CI) and Continuous Deployment (CD) –tools come in to the play. The CI/CD process can be used to automate unit testing, so once the programmer has finished writing code, it is then uploaded to the CI/CD-pipeline that does the testing of the code automatically before releasing it. If there are anomalies, the process will fail, and feedback report is sent to the programmer. I have discussed the cultural importance of constant feedback in my [previous post][culture]. I’d argue that automated testing puts even further empathize the impact of DevSecOps to the culture of workplace, since automation provides indefatigable feedback, that doesn’t stop even after the tenth time of submitting code for reviewing. When testing the same thing over and over, human testers tend to be less diligent and like programmers, may produce errors themselves. I’m not implicating that humans should stop doing tests completely, but rather do ones that do not require do the same thing repeatedly. 

Integration testing 
================== 
Unit tests' scope is limited into very small details, in which all are tested individually. Unit testing does not do cross testing of all newly implemented modules. This means that there is no certainty that all the code blocks even work together. No worries thought, integration testing is a phase where all the previously unit tested parts are tested together. Goal of this test is to confirm that all the modules work correctly together, since there can be a situation where two or more components do not interact correctly with each other. 

Since programs are modular, means that each unit is part of one component and the whole program is made up of multiple components. Again, I believe this is best understood with a picture: 
![Integration testing](/assets/integration_testing.svg) 

As pictured, each unit is integration tested, so that they work as a part of component. However, this is also where things get interesting. Each of the component must also be tested against each other. What this means is that there are multiple layers of integration testing. I really enjoyed the analogy that [Software Testing Fundementals][int_testing] provides: 

> During the process of manufacturing a ballpoint pen, the cap, the body, the tail and clip, the ink cartridge and the ballpoint are produced separately, and unit tested separately. When two or more units are ready, they are assembled, and Integration Testing is performed. For example, whether the cap fits into the body or not. 

In my mind this integration test analogy can be continued by stating that the ballpoint pen is a component and one eighth of a set of pens sold in certain cardboard box. When the all the eight components (pens) are fully (all units are in place) and correctly assembled, they must also fit the box they are sold on, thus they must have same dimensions and hopefully look identical. Like with unit testing CI/CD-pipeline can be used to automate testing. 

System testing 
================== 
Like stated on my summary of different types of testing, system testing is done to the running program. If not enough of attention to unit tests and integration tests is paid, this is usually the situation where most of the bugs are found. However, that is not to say that this is the only goal for system testing. Main objective is to determine if the program meets the requirements stated in [requirement analysis][req_analysis]. What system testing is testing is including but not limited to; security, reliability and how the program performance is on high stress situations. Thus, unlike previous tests, on this level of testing focus is more on how the program performs on live environment, hence there is smaller focus on source code itself. Not saying that source code is not altered after the system testing, especially if bugs are found. 

Acceptance testing 
================== 
Lastly acceptance testing is done before releasing the program available for end-users. Goal of acceptance testing is to make sure that the program is ready to ship, making sure that the end-users can do what the program promises. In short, acceptance testing ensures that program is working like described.  

There are many ways to do this, since there are many ways to “accept” that this product is ready to ship. One of ways is to simply release the program in alpha / beta state and gather feedback from end-users who have downloaded the program, this is known as User Acceptance Testing or UAT. In situations where program is ordered by another company UAT can be completed by selecting end-users from that company, all of which start using the program and then submit feedback on how it affects their daily work. 

Robot Framework for testing 
------ 
Robot framework is the open source framework for acceptance testing, written using Python programing language. It is a completely independent of operating system and application, thus it can be run almost everywhere. What makes it very powerful is it’s easy to use syntax, that is completely keyword driven. Here is an example.robot-file which has a test case using Robot Framework’s syntax with SeleniumLibrary: 


```
*** Settings *** 

Resource          resource.robot 

*** Invalid login test case starts below ***  

Invalid Login  

    Open Browser To Login Page  

    Input Username    test@test.com 

    Submit Email  

    Input Password    test  

    Submit Password  

    Invalid Username Or Password Text Should Be Printed  

    [Teardown]    Close Browser  

```
As can be seen it is easy to understand, so easy in fact, that my lecturer even stated that even the CEO of the software company knows what is being tested with above syntax. 

Anyway, I stated that Robot Framework has something called SeleniumLibrary, what does it do? Well the idea of Robot Framework is that the base framework provides [libraries][libraries] with basic keywords, such as [Builtin][builtin], but these keywords can be expanded with multiple external libraries, such as SeleniumLibrary which allows web testing. In fact keyword “Close Browser“ is [SeleniumLibrary's keyword][selenium].  

If you have checked out the documentations I have provided so far, you might have noticed that there is no syntax or keyword for Open Browser To Login Page,Submit Email etc. You might have also noticed that Close Browser seems to be only syntax available. Well Robot Framework also has support for something called “high-level keywords”, which allows users to create their own keywords by combining available library keywords. For example, “Open Browser To Login Page” is actually high-level keyword that includes these keywords and variables: 

```
Open Browser To Login Page 

    Open Browser    ${LOGIN URL}    ${BROWSER} 

    Maximize Browser Window 

    Set Selenium Speed    ${DELAY} 

    Login Page Should Be Open 

```

These high-level keywords are declared inside resource.robot-file, and you might have noticed that on example.robot-file, the first line after ***Settings*** is Resource resource.robot. This is where the high-level keywords are acquired. These high-level keywords are same as functions in regular programming. They provide a way to encapsulate regular keywords inside, thus preventing unnecessary repetition of keywords. 

High-level keywords can even call other high-level keywords like is done on “Open Browser To Login Page”.  Here “Login Page Should Be Open” is called and it looks like this: 

``` 
Login Page Should Be Open 

    Title Should Be    Home Page 

``` 
Finally, there are variables, such as ${LOGIN URL} and ${BROWSER} these work like variables in regular programming, meaning that one can store values inside them. Here is an example of values used in resource.robot-file: 
``` 
*** Variables *** 

${SERVER}         testpage.test 

${BROWSER}        Firefox 

${DELAY}          0 

${LOGIN URL}      http://${SERVER}/ 

${WELCOME URL}    http://${SERVER}/welcome.html 

${ERROR URL}      http://${SERVER}/error.html 

``` 
Again, these are highly useful and once again prevent users from repeating the same thing again and again. Also, this makes the syntax much more modular, thus the same test case can be used in another server or browser. Simply changing the corresponding variable without need for combing through the whole file. 

Robot Framework Example 
================== 
Last header covers the basics of Robot Framework, so now it is time for me to show you how it is done. Here is a simple YouTube-video I recorded of the Robot in action: 
<iframe width="981" height="552" src="https://www.youtube.com/embed/ovKSsETfSYE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

What is happening here is four different tests: 

1. Test if newest blog post is up by checking if it is possible for the robot to locate link that points to location “/programming/2019/05/05/DevSecOps-weekly-5.html”. 
2. iPhone X test for blog by resizing the window to 375 x 812 size and taking a screenshot of it. 
3. Test for blog images, in which the robot checks if it possible to locate two images that point to locations /assets/KANBAN.png and /assets/KANBAN_colorcodes.png 
4. View test completed; not really a test, but a redirection to image that shows that all the tests are completed. 

As seen in the second test, robot can be also told to take screenshots on any location, here is what this blog looks like on iPhone X screen:
![Blog on iPhone X screen](/assets/iPhoneX_screen.png) 

Here are my files, first the resource-file know as resource.robot: 
``` 
*** Settings *** 

Documentation     A resource file with reusable keywords and variables. 

Library           SeleniumLibrary 


*** Variables *** 

${SERVER}         sorhanp.github.io 

${BROWSER}        Firefox 

${DELAY}          2 

${HOME URL}       http://${SERVER}/ 

${HOME TITLE}     (Re)discovering the code | Programming blog of Hannupekka Sormunen 

${LATEST POST}    /programming/2019/05/05/DevSecOps-weekly-5.html 

${LATEST TITLE}   DevSecOps weekly, fifth issue | (Re)discovering the code 

${DEFAULT WIDTH}         1100 

${DEFAULT HEIGHT}        975 

${IPHONE WIDTH}          375 

${IPHONE HEIGHT}         812 


*** Keywords *** 

Open Browser To Home Page 

    Open Browser                ${HOME URL}    ${BROWSER} 

    Set Default Browser Size 

    Set Selenium Speed          ${DELAY} 

    Home Page Should Be Open 


Set Default Browser Size 

    Set Window Size             ${DEFAULT WIDTH}    ${DEFAULT HEIGHT} 


Home Page Should Be Open 

    Title Should Be             ${HOME TITLE} 


Click The Newest Post 

    Click Link                  ${LATEST POST} 

    Title Should Be             ${LATEST TITLE} 


Resize To iPhone X 

    Set Window Size             ${IPHONE WIDTH}    ${IPHONE HEIGHT} 


Blog Should Contain Two Images 

    Set Selenium Speed  1 

    Page Should Contain Image   /assets/KANBAN.png 

    Page Should Contain Image   /assets/KANBAN_colorcodes.png 

    Set Selenium Speed  ${DELAY} 


Scroll Through Page 

    Set Selenium Speed  0 

    : FOR    ${INDEX}    IN RANGE    1    750 

    \   Scroll Page To Location     ${INDEX} 

    Log    For loop is over 

    Set Selenium Speed  ${DELAY} 


Scroll Page To Location 

    [Arguments]     ${y_location} 

    Execute JavaScript    window.scrollTo(0,${y_location}) 

```
and finally the test case-file known as blogtest.robot: 

``` 
*** Settings *** 

Documentation     A test suite for https://sorhanp.github.io/. 

Resource          resource.robot 


*** Test Cases *** 

Test If Newest Blog Post Is Up 

    Open Browser To Home Page 

    Click The Newest Post 


iPhone X Test For Blog 

    Resize To iPhone X 

    Capture Page Screenshot 

    Scroll Through Page 


Test For Blog Images 

    Set Default Browser Size 

    Reload Page 

    Scroll Through Page 

    Blog Should Contain Two Images 


View Test Completed 

    Go To   https://sorhanp.github.io/assets/test_completed.svg 

    [Teardown]    Close Browser 

``` 

Final thoughts 
==================
Robot Framework is a highly sophisticated tool for testing. However, in order it for to be most efficient, it is important to design around it from to get go. What I mean by this is that when the robot is accessing web site, it is important to assign IDs for all the elements that are required for testing. For example, if robot needs to check if some picture is visible after an input, that picture should have specific ID so that the robot knows exactly, that it is looking for that picture in particular. There is a term for this kind of approach and it is known as [Test-driven development][tdd]. 

I was also very excited to learn that Robot Framework can be used for [Robotic Process Automation, or RPA][rpa]. It is a way of interacting with a program via a software robot. Robot does exactly what human is doing; thus, it hovers a cursor to a button, clicks it, copies data from form to another etc. Only thing is that it can do it much faster than human, making it perfect tool for automating tasks, such as data entry from one place to another. 

I have been interested in RPA for about a couple of years because I have been part of a workshop designing how RPA would handle automation of certain processes that are error prone and require no actual human input or thought at all. Usually RPA is used in older systems that are no longer viable to develop further to allow native automation to be implemented. I strongly believe that learning more of this will make me a better programmer, since it makes me think ahead of time on how testing can be done effectively.

-sorhanp
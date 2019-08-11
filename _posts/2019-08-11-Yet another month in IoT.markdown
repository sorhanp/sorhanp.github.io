--- 
layout: post 
title:  "Yet another month in IoT" 
categories: programming 
description: My findings about IoT, Internet of Things, IIoT, Industrial Internet of Things, embedded, embedded systems, C, C++ and embedded programming.
tags: IoT, Internet of Things, IIoT, Industrial Internet of Things, embedded, embedded systems, C, C++, embedded programming.
excerpt_separator: <!--more--> 
--- 

[last]:/programming/2019/06/29/A-month-in-IoT.html
[aplicom]:https://www.aplicom.com/
[wiki_embedded]:https://en.wikipedia.org/wiki/Embedded_system#Embedded_software_architectures
[wiki_rtos]:https://en.wikipedia.org/wiki/Real-time_operating_system

Yet another month, well almost a month and a half, has passed since I started my on-the-job training. I must admit that I have been reading and writing a lot text during my trainee hours. So much so, that I have not had the time nor energy to dedicate time for blog posts as frequently as before. Thus, there was this little “sabbatical” from blogging during the month of July. Well now I’m back and I have a major announcement to make!<!--more--> 

Before going on the announcement, a little recap on my second month as a trainee.  

My [last][last] described that I have been working for a telematics company called [Aplicom][aplicom] and I have been getting familiar with the basics of IoT, as well as the security aspects of it. In fact, I spent my days documenting on how to produce a secure IoT solutions. While that was my main task when I signed the on-the-job training contract, I also had the chance to participate in software development. 

That meant that I have had the privilege to work with experienced programmers and learn about C and C++ languages. What an amazing opportunity, which I fully utilized by documenting the programming concepts previously unknown to me! I have not worked with embedded systems before and the difference to personal computers became obvious from the get-go. 

[Examples of embedded software architectures][wiki_embedded] states a list of different types of embedded system software and their properties, such as interrupt-controlled system, and preemptive multitasking or multi-threading. All of these demonstrate how embedded software vary from standard PC applications that I have been working with. 

For example, instead of a general-purpose operating systems (GPOS), such as Linux or Windows, embedded systems may utilize [real-time operating system][wiki_rtos] (RTOS). Like the name suggests, applications in RTOS are served in real time, which means that the data is processed immediately when it has been received.  

Due the time critical element, processing must be done in certain time frame, or execution will fail. This is different from GPOS, where these sorts of timely mechanism do not exist, and processes are carried out when it is possible by a method known as scheduling. 

So, from architectural standpoint embedded systems are different than what I have been used to. On hardware level, embedded devices are usually very constrained, which means that there is a very limited amount of memory and other computing resources available. The memory management of C and C++ programming really plays a big part when designing applications for embedded systems. 

Now back to the announcement! I’m happy to inform, that starting from August, I will be working full-time at Aplicom as a Software Engineer, developing software for embedded devices! Here is my LinkedIn-post from earlier, translated to English: 

>On October 17th, 2018, I began my journey towards re-learning software development with the “(Re) discovering the code” mentality. I first started by jumping in front of my own PC to see how those C ++ pointers work. Half a year later, on April 1st, 2019, I started DevSecOps training, jointly organized by the TE Office and JAMK. As a result of the training, I was able to see how software development is implemented with modern tools. 

>The training also included an internship, during which I was introduced to the world of IoT, which was previously unfamiliar to me, but have always found very interesting. During this time, I became also closely acquainted with embedded systems. 

>I'm writing this reflection, because I’m delighted to announce that as of today, I start at Aplicom Oy as Software Engineer, which means that I have attained one milestone. Many thanks to Atri Vainikainen (my supervisor) for this great opportunity! P.S. Learning will never end, and my blog will continue to contain my thoughts in the future! 

Even though this noticeable turn of events means that I have completed one milestone on my path, I still strongly feel that my journey is not over. Now that I know where my focus is, there are still major things I must learn!  

This is the reason why I decided to go out and continue my learning path on C++, so expect much more programming content focusing on embedded development from now on! 

-sorhanp
--- 
layout: post 
title:  "Global DevOps Bootcamp 2019" 
categories: programming 
description: My findings about Global DevOps Bootcamp 2019, GDBC, devops, and devsecops 
tags: Global DevOps Bootcamp 2019, GDBC, devops, devsecops, Global, DevOps, Bootcamp 
excerpt_separator: <!--more--> 
--- 

[gdbc]:https://globaldevopsbootcamp.com/ 
[zure]: https://zure.com 
[sre]:https://en.wikipedia.org/wiki/Site_Reliability_Engineering#DevOps_vs_SRE 
[polarconf]:https://polarconf.fi/ 
[iglooconf]:https://www.iglooconf.fi/ 
[azure]:https://azure.microsoft.com/en-in/services/devops/ 
[serviceplan]:https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans 
[secret]:https://www.alldaydevops.com/blog/how-to-fully-automate-ci/cd-even-secrets 
[load]:https://docs.microsoft.com/en-us/azure/azure-monitor/platform/metrics-supported#microsoftcomputevirtualmachinescalesets 
[challenges]:https://www.gdbc-challenges.com/ 
[autoscaling_solved]:https://www.gdbc-challenges.com/Challenges/PostMortemSummary/DENOFSERV 
[whitesourcebolt]:https://marketplace.visualstudio.com/items?itemName=whitesource.ws-bolt 
[npm]:https://www.npmjs.com/ 

I had huge honor to attend to [Global DevOps Bootcamp 2019][gdbc] which was hosted by [Zure][zure] at their home offices in the heart of Helsinki. This is equal parts my trip journal and my learning diary of the bootcamp. Hop on and let me tell you about my experiences of the meetup!<!--more-->  

In short, Global DevOps Bootcamp is a event organized by multiple organizations all over the world with the aim to educate and share the message about the benefits of DevOps and of course [Microsoft's own DevOps-environment, called Azure][azure]. I noticed the event from LinkedIn (thanks Visa!) and applied as soon as it was possible. I got invited and got sent bunch of preliminary material about the event. 

I read the preliminary material that the organizer had sent me on Friday afternoon, and my excitement grew! I finally had a chance to attend a meetup of my new career choice and learn DevOps more closely from the professionals who build solutions using the tools in their daily work life. All the while I had a possibility to network with other people at the event. 

Before the event I also learned a new term: Site Reliability Engineering (SRE), and how it [shares same foundational principles with DevOps][sre]. Main difference, however, is that SRE's tend to be developers themselves. This is something I must learn more about, since I always believe that one can learn more another a great deal, bringing the best of both worlds. 

I was armed with laptop, curiosity and mindset of learning and improving, as I hopped on the bus with excitement on that Saturday morning. The bus left bit after five o'clock in the morning from Jyväskylä. While at bus, I rechecked the timetable for today: 
- 09.30 | Drop-in & Coffee 
- 10.00 | Intro and keynote: "You build it, you run it” 
- 10.30 | Bootcamp starts 
- 12.45 | Lunch 
- 13.30 | Bootcamp continues 
- 16.00 | Demos 
- 16.30 | Wrap up 

I will go through each of piece of agenda under their own headers and share how I experienced the event, and hope that you can gain some knowledge at the meantime! 

# 09.30 | Drop-in & Coffee 
The bus dropped me at Helsinki city center around 9 o'clock, so I had plenty of time to get to my destination. Before that, I got myself some breakfast so that I was full of energy, like the organizer was hoped in the preliminary material, at the start of the bootcamp. I was greeted warmly at the start and was directed to get coffee and snacks. Of course, I had my share, thus I was stuffed and ready to learn right at beginning. Talk about warm welcome :smile: 

The drop-in started with the introductions. First from our trainers Okko Oulasvirta and Pasi Huuhka told about what Zure does and who they are.  

During the introduction I was also told about out [PolarConf][polarconf] and [IglooConf][iglooconf] and recommended to check them out. Both are very low-cost level Azure learning festivals. I will keep my eye on these, since maybe I have chance to attend someday. 

After the trainers had introduced themselves, it was time for each of student to introduced themselves. It was very humbling to be around people who have so much experience on DevOps and SRE and I was sure that I will learn alot during the discussions we will have. 

# 10.00 | Intro and keynote: "You build it, you run it” 
Before the bootcamp started there was bit of briefing on the theme of this year: 

>You build it, you run ~~away~~ it.  

Then we watched the brief keynote video on what does it mean to have "positive negativity", because most of the time if something can go wrong, it will go wrong and the role of the DevOps/SRE is to be there and get things up and running smoothly. Part of that positive negativity is also preplanning for things that **will** go wrong. 

When the keynote was over it was time for our trainers to continue with the local agenda on goals of DevOps/SRE:  
- reliability (production environment runs smoothly) 
- appropriate (how to measure success) 
- sustainability (automate things, plan ahead for problem situations -> less tickets and calls) 

I strongly agreed that these are excellent points to have on any software production. Especially because it really drives the fact home that if everything is running smoothly (read: sustainably) on the background, the better it will look on production environment, which is what the customers and the public sees. 

# 10.30 | Bootcamp starts
The bootcamp started and we were given a introduction to PartsUnlimited Inc. a virtual corporation that has it share of problems that it wants to fix with strong DevOps culture.

The goal of today's bootcamps was to start solving almost lifelike DevOps/SRE-challenges of this company. From the preliminary material I learned that this year's challenges were: 
- Exception rate goes up 
- Supply chain attack 
- Message from CEO - Help needed on Social Media 
- SSL Certificate suddenly expired 
- Denial of service on your application 
- Credentials are leaked and are rotated 
- Sentiment on social media (Twitter) goes negative due the issue with site 
- Connections to database are flaky and causes random errors 


For example, they had a credential leaked when the firm decided to go open source. They pushed almost all their code to GitHub, therefore releasing admin credentials publicly in cleartext format. It was our task to start fixing this on their Azure, first by providing a quick fix and then making a postmortem to make sure that this will **never** happen again. 

Other example was that they had a free campaign on their website offering products free for all the people. They got so many hits on their webpage, but they didn't have proper scaling on their server to handle that kind of traffic and the server went unavailable. 

I will not go on details on all of these (in fact you can see them [here][challenges]), but I will tell that everything was build up amazingly. Each of us got our own environment with the available challenges and by clicking on of following challenge-buttons: 
![Challenge buttons](/assets/devops_problems.png)  

The problem was realized on the environment and it was time to to start solving them. We had a long-winded discussion about on how to proceed on the problems and even before I noticed, the next header was upon us.

# 12.45 | Lunch 
So before starting doing any DevOps-work we had lunch as a group. One awesome thing about this event was the fact that the lunch was provided to the location and it was free for all attendees! There were no worries about having to work on an empty stomach! 

All right back to the bootcamp! 

# 13.30 | Bootcamp continues 
After lunch it was time to continue. So, let's go through the tools used in the bootcamp. So the whole event environment was built on Azure platform, where there was database, [App Service Plan][serviceplan], which is used to define a set of compute resources for a web app to run, and finally the web application itself. 

On the background there was Azure DevOps-environment for continuous integration and deployment. That environment hosted the Git-repository, which was used to automatically deploy and build web application. 

One of the most memorable situations was the moment where the credentials where leaked with the repository to the outer world and we started working on the fix. I remember it well because I had talked about [secret management][secret] with my mentor on my studies. 

Thus, when fixing I had a pretty good idea on what angle to approach the situation. Of course, how it is done on this environment was a mystery, but I got the hang of it thanks to good guidance from my partner and the guides provided by the event organizer. 

Next thing I remember was the denial of service attack because it involved something that I have been always interested in; scaling the cloud servers to meet up with the high traffic demands with autoscaling. Autoscaling automatically allocates more resources to match performance requirements, as the volume grows. 

This proved to be tougher than first thought, since we could not locate the [metric][load] on how to scale on server's response time. Finally, after couple of mistakes there was a guide on how to boost up according to log-based metric, while the metric being server response time. More on that [here][autoscaling_solved].

# 16.00 | Demos 
The bootcamp time was up and the organizers started talking a bit about behind the scenes experiences, while the students, including me, shared their opinions on the problems too. Sort of like a postmortem on what we learned, how we solved problems etc.  

Through the discussion learned about [WhiteSource Bolt][whitesourcebolt] that checks out packet dependencies and see, if they are trustful etc., kind of like [npm in JavaScript][npm]. 

# 16.30 | Wrap up 
We had little refreshments and had a raffle and I won awesome Zure-prizes! :smile: 

![Zure prizes](/assets/zure_prizes.png)  

That's it! At 17.45 I was on my way to home back to Jyväskylä and started writing about my day, which I really enjoyed! 

I like to thank for the event from the bottom of my heart. Everything went so smoothly, and I thought that I was learning constantly being surrounded by so much talent! I will definitely go next year, if I get the chance! 

-sorhanp 
---
layout: post
title:  "Out with the old, in with the new"
categories: programming
excerpt_separator: <!--more-->
---
[arch]: https://www.archlinux.org/
[virtualbox]: https://www.virtualbox.org/
[github]: https://github.com/sorhanp
[Amaintenance]: https://wiki.archlinux.org/index.php/System_maintenance
[debian]: https://www.debian.org/
[ubuntu]: https://www.ubuntu.com/
[xfce]: https://www.xfce.org/
[kate]: https://kate-editor.org/
[brackets]: http://brackets.io/
[jani]: http://www.penttinen.fi/
[splitted]: http://cse230.artifice.cc/lecture/splitting-code.html
[eclipse]: https://www.eclipse.org/ide/
[oop]: http://www.ntu.edu.sg/home/ehchua/programming/cpp/cp3_OOP.html
[beginnerscpp]: https://www.udemy.com/free-learn-c-tutorial-beginners/learn/v4/content
[isofaq]: https://isocpp.org/wiki/faq/classes-and-objects
[cplusplus]: http://www.cplusplus.com/doc/tutorial/classes/
[cppreference]: https://en.cppreference.com/w/
[previous]: /programming/2018/10/26/Keeping-on-keeping-on.html
[source]: https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/

When I started relearning the basics of C++ I used [Arch][arch] Linux  through [Virtualbox][virtualbox]. I also used that platform to create this site, post blog updates and maintain my [GitHub][github]-page. Everything went really smooth, but I still thought that with the rolling updates that Arch Linux provides, my system needs constant [maintenance][Amaintenance] just to make sure, that everything continues to run smoothly.<!--more-->  I think that this is bit of an **extra hustle** in this stage, when I want to spent most of time   learning to program, rather than keep learning new ways how to maintain my operating system. That is why I decided I need change in my life. That change came in the form of [Debian][debian] Linux. I have used [Ubuntu][ubuntu] Linux when I was a polytechnic student with a tight budget with a cheap old computer, so rather than paying for operating system, I decided that free Linux is something worth looking into at the time. Ubuntu was and still is Debian derivative so getting Debian up and running with the software I need was really easy. Everything felt really familiar and it is was like I never left the wonderful world of Ubuntu.
![Debian](/assets/debian.png)

This time instead of Plasma desktop environment by KDE I felt that I should choose something little more lightweight. So when Debian asked which environment I want to use I chose [Xfce][xfce]. Changing desktop environment also means, that some of the programs won’t be available, because of library differences etc. While it is still possible to install all the same programs that were available on Plasma, like [Kate][kate], which I used as my editor for C++, and of course doing these blog posts with Ruby, it is still better to use alternatives so that the system keeps lightweight and doesn't need thousands of different libraries installed. So it was time to hunt down new editor that suits my needs.

My quest for the new editor ended quickly when a friend of mine, [Jani][jani] (site in Finnish), recommended me [Brackets][brackets] as and editor. One package installation later and so far I have been very happy with it. It provides easy way to make changes in multiple files, something that is a must when working with [splitted files][splitted], also known as modules when programming for example classes. When the code is in different modules it is important to be able to hop from module to module and edit lines of code where it is necessary. I know that IDEs, such as [Eclipse][eclipse] would be even more powerful, but I think it is important to keep writing the code as much as possible and learn from the simple mistakes one can make when programming as much as possible without automatic corrections, automatic header file creation etc. automatically doing things to me and telling where the mistake is. I also think that it is good to learn to “decipher” what the actual compiler is saying as much as possible.

I also have been tinkering alot with my blog and trying to learn as much as possible about what is “under to hood”. For example after last blog post I added little post excerpts to [main](/index/) page showing first lines of each blog post. I also have started to use code highlighting as seen in [previous post][previous] when I added my multiplication table example. Not visible changes include the fact that I no longer upload the pure HTML-version of the site to the GitHub-pages but rather just upload the whole source code that is [then changed to the website automatically by GitHub][source]. When I first started blogging I did not understand exactly how developing web content is done, so thanks to this blog I have been able to start understanding markup languages bit better. I like to think that anything that one learns is important and I certainly feel that way about this too. Hopefully one day I can build my own site with own theme, but for now I stick with C++ and try to master as much as possible rather than understanding only little of everything.

I will update my C++ progress later this week when I have more understanding of [Object-Oriented Programming][oop] which I’m currently actively learning through the [course][beginnerscpp] and through various other source materials listed here:

* [Standard CPP Foundation][isofaq] has a very comprehensive and helpful FAQ-section.
* [cplusplus.com][cplusplus] has very basic tutorials how everything works and even a forum that has a lot answers from programmers around the world.
* [C++ reference][cppreference] includes very fast access to almost any recourse one could need.

-sorhanp
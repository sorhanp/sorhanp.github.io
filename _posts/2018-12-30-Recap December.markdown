---
layout: post
title:  "What was going on all of December?"
categories: programming
description: My findings about C++ (CPP, or cpp), SDL, game loops, GitHub documenting, code documentation and writing code wiki's
tags: programming, c++, object-oriented, cpp, gameloop, game_loop
excerpt_separator: <!--more-->
---

[last]:/programming/2018/11/30/Monthy-Recap-November.html
[particlefire_home_page]:https://sorhanp.github.io/particlefire-revision/
[cppbeginners]:https://www.udemy.com/share/1000sQBEUccF1bRX4=/
[visual_studio]:https://visualstudio.microsoft.com/
[wiki_particlefire]:https://github.com/sorhanp/particlefire-revision/wiki
[johnpurcell]:https://caveofprogramming.com/
[sdl]:https://www.libsdl.org/
[cppadvanced]:https://www.udemy.com/share/1000MSBEUccF1bRX4=/
[github_repo]:https://github.com/sorhanp/particlefire-revision
[git]:https://git-scm.com/
[subversion]:https://subversion.apache.org/
[particle_position]:https://github.com/sorhanp/particlefire-revision/wiki/Position-and-movement
[box_blur]:https://github.com/sorhanp/particlefire-revision/wiki/Box-blur
[performance_overview]:https://github.com/sorhanp/particlefire-revision/wiki/Performance-overview
[performance_boxblur]:https://github.com/sorhanp/particlefire-revision/wiki/Performance-overview#improving-the-box-blur-algorithm
[cpp_optimizer]:https://en.wikibooks.org/wiki/Optimizing_C%2B%2B
[vs_profiler]:https://docs.microsoft.com/en-us/visualstudio/profiling/profiling-feature-tour?view=vs-2017

Time has passed since [last][last] update to this blog. I completed the [C++ Tutorial for Complete Beginners course][cppbeginners] at the beginning of December. Rest of the month I have been working on programming and improving the final project of the course known as The Particle Fire Simulation and made my own version [The Particle Fire Simulation Revision][particlefire_home_page] of the project, documented the whole process to a [massive wiki with some 40 pages of content][wiki_particlefire] and even installed [Microsoft’s Visual Studio][visual_studio]. About all this and much more on this blog post!<!--more-->

Starting this post with a nice image:
![Classes with inheritance](/assets/certificate.png)

Like the first paragraph stated, I was able to conclude my first online course on programming since March of 2010 and I feel very happy for it. I set clear goals to myself at the beginning of course and was able to achieve those, one of which was of course keeping this blog and second being to have as much as self-written documentation as possible. I have already signed in to the next course known as [Learn Advanced C++ Programming][cppadvanced] which is also tutored by [John Purcell][johnpurcell]. But before going on forward with that I will take a little break from C++ and move on the PHP and Wordpress. I have a little project mind with my friend that we have been wanting to do and since I have more time on my hands I figured that what better time than now. More on that project and my PHP studies on the next blog post, that won’t take another month to complete. No worries though, because I still have couple more programming concepts that I need address on this blog before writing about completely new programming language.

Going back to final project of the course known as The Particle Fire Simulation taught me a lot of things. First of all I since this project now has a [GitHub repository][github_repo] it made me relearn how to use [version control system known as Git][git], since all the updates, changes and deletions to that repository are done with git-program, which was something that I had done in the past, but not as much as I have used now. I have much more experience using [Apache’s Subversion][subversion], which is also a version control system. I also learned how to maintain repositories on GitHub so the service itself is more familiar to me and when I start my next bigger project I have full knowledge how to start a repository and keep updating it etc. Second thing learned was when commenting the code you are going to publish at one point, make sure that it is presentable from the beginning, since it is a great deal to start add comments to even little programs like this one. Also documenting should also be done on the side rather than after the project is finished so that you can remember all the specifics when writing comments and that one doing only one task doesn’t slow you down, since you can switch between coding and commenting at any given time.

Speaking of repositories and documentation Github also has a marvelous way to document the program’s source code for example to demonstrate how to use classes, how different parts of program behave with each other and explain concepts of program such as mathematics behind certain algorithms. [The Particle Fire Simulation revision wiki][wiki_particlefire] is also available and it contains a lot of information. My personal favourites where explaining the concepts behind the program, because I also had to understand the program myself and that is the best way of learning, especially algorithms since my math skills are long evaporated. I recommend pages about [particle position][particle_position], [box blurring explanation][box_blur] and [documentation of program’s performance][performance_overview]. These are really like my previous blog posts in the way that they explain programming concepts.

Finally, I also exported my project from Linux to Windows environment and started using [Microsoft’s Visual Studio][visual_studio]. This was done since program has to display graphics in high speed and while it is possible to view and use graphical programs such as  games through Linux and VirtualBox the performance is not optimal and I wanted to made sure that the program performs as fast as possible to start optimizing it by making data methods such as box blurring execute much faster. This also was to reason that Visual Studio was used. It has very nice [profiling feature][vs_profiler] that points out where program could have potential for improvement. I’m especially proud of my findings on [how to make box blur algorithm perform about 70% faster][performance_boxblur] and the fact that I was able to implement stuff from [Wikibook about Optimizing C++][cpp_optimizer] to my own code.

Pretty much nothing else to add. Month was amazing because I was able to do and learn many things that will prepare me for the future. I’m more confident about my skill and when next project begins I will know where and how to start it.

-sorhanp
--- 
layout: post 
title:  "A month in IoT" 
categories: programming 
description: My findings about IoT, Internet of Things, IIoT, Industrial Internet of Things, protocols, networking and security
tags: IoT, Internet of Things, IIoT, Industrial Internet of Things, protocols, networking, security
excerpt_separator: <!--more--> 
--- 

[last]:/programming/2019/05/26/DevSecOps-weekly-8-2.html
[aplicom]:https://www.aplicom.com/
[iotfund]:http://www.ciscopress.com/store/iot-fundamentals-networking-technologies-protocols-9781587144561
[6lowpan]:https://en.wikipedia.org/wiki/6LoWPAN
[ipv6]:https://en.wikipedia.org/wiki/IPv6
[iic]:https://www.iiconsortium.org/
[iisf]:https://www.iiconsortium.org/IISF.htm

It has been over a month since my [last post][last] regarding my DevSecOps -training, thus it is time to bring you up the speed on what has been going on. As the title suggested it has to do with the Internet of things (IoT)!<!--more-->

On the 27th of May I started on-the-job training at [Aplicom Oy][aplicom]. Aplicom is a vehicle **telematics** device manufacturer and developer. I have had little experience with provisioning SIM cards for telematics devices end sending them to end users of the devices, but that is about it. For example, I have not ever seen a telematics device in real life, up until now of course.

Therefore, I had to start from the beginning in order to brush up my skills in **IoT** to understand the “big picture” behind both bolded keywords. I have noticed that is easier to perform better in my job when I know a little bit more than just what is necessary to perform one’s daily work tasks. 

Example of the previous statement was the fact that when I worked as an order handler. I tried to communicate as much as possible with the developers and other stakeholders of the order system(s). From these discussions, I was able get little details on how the order process works behind the scenes of the system and how to mitigate small error situations by myself.

# The basics 
When I first learned that I will be working in the field of IoT I borrowed book called [IoT Fundamentals: Networking Technologies, Protocols, and Use Cases for the Internet of Things][iotfund] by Robert Barton, Patrick Grossetete, David Hanes, Jerome Henry and Gonzalo Salgueiro from my local campus library.

First part of the book discussed about the higher-level overview of IoT and introduced the key concepts. I learned that IoT has a very highly detailed background than just daily products, such as fridges and lamps, getting connected to Internet. See the picture below for the IoT functional stack.

![High-level IoT functional stack](/assets/iot_stack.svg)

The layers explained:
- Things are the physical devices, that collect the information, such as a speed and position in telematics.
- Communications is the communication between the thing and external system
- Applications are the software, that process the data collected by the things

Things layer also has a sensors and actuators in the title. What I learned is that things in IoT can be either really smart, or really... well, not smart and rather simple. So, for example, the things can be simple sensor devices that collect information via sensors and send that information to a gateway device.

That gateway device then processes and the data and sends it via the communications layer to application where the data is stored for later use. Processing in this sense means, that the analog signals from sensors are turned into digital output, basically ones and zeroes.

The gateway device can also collect information from multiple sensors and in some predefined situations alert the users. These situations can happen, for example, if some of the sensors detect ambiguous readings, which may put resources such as business processes, tools or human lives at risk.

The second “thing” mentioned on the picture are actuators, which can used mitigate the risks of aforementioned resources by commanding, for example, safety devices or shutting down the device(s) all together. In short actuators transform digital input to analog signals, so that traditional devices can operate from software commands.

Of course there are tons of uses that actuators can be used, think of it as limbs in a human body, that receive commands from the brain. Whereas sensors are the eyes, ears etc. that can perceive the world.

This whole concept of sensors, actuators and gateways is called *edge computing*. When thinking of commercial smart objects for regular customers, these sensors and actuators are usually built inside the device forming the “edge” itself. But in industrial environments, IoT devices are usually split, because some legacy devices in the industrial environment are not possible to replace easily with modern smart objects.

For me, the realization, that the things in IoT are this “edge”, whether they are a single smart object or multiple sensors connected to gateways etc., was the biggest surprise. 

I would alsl like to point out that the higher-level chapters broke the concept of IoT especially well, thus making rest of the book easier to understand, even for beginner like me. Really good work!

# Building an IoT network
The next part dove much, much deeper in to the world of IoT, such as what kind of sensors, actuators and smart objects there can be used to form the edge, how to network them, how to build the communication between the edge and the software, such as cloud servers.

This part really made me interested in networking in general and I really want to program something utilizing the knowledge gained from these chapters.

What I enjoyed the most was the different protocols and ways to build IoT network, especially in industrial settings, where the smart objects can be really limited in terms of processing power, as well as electricity. These are known as a constrained device, picture below, redrawn from the book.

![Constrained IoT device](/assets/iot_constdev.svg)

So as can be seen, constrained devices are built to environments where they spent as little electricity as possible and because of that, the components are really limited as well as communication in terms of speed and signal strength. Speaking of the constrained, the protocols used in these situations are optimized as well, since they aim to transfer as much as data as possible in one packet.

An example of these protocols is [IPv6 over Low -Power Wireless Personal Area Networks][6lowpan]. This protocol aims to limit the number of network packets that need to be transferred from a smart object by compressing header information of network and transport protocols, thus more than doubling the actual data content per network packet.

These are just a small sampler on what kind of tricks and optimization can be done to make devices perform even in the toughest of situations where electricity is not available, and data must be transferred from smart device to gateway in non-optimal radio situations, where data can get lost.

Of course, not all smart objects are in constrained environments and even the most advanced hardware and fastest modern protocols can be used to transfer data, such as the case with vehicle telematics device that can be connected to very fast LTE/5G mobile networks. Be it constrained or non-constrained, security is important.

# Security in IoT
I have been always interested in security of any system and was eager to read second part of the IoT Fundamentals, which also has a chapter about security. This chapter mostly focuses on challenges of fitting together modern Information Technology (IT) and traditional industrial Operation Technology (OT).

Since IoT tries to combine these together, it often leads to security issues. The reason behind this is the fact that IT has a long history of securing networks from attacks, whereas OT has been kept in its own environment outside of hazards that the online networking presents.

Example of security issue when connecting industrial OT systems to the modern world of IT, is the fact that these systems have long lifecycles. Therefore, when connected to form an IoT solution, they might have vulnerabilities that are not going get patched, since the system is longer maintained.

Legacy systems rarely support certain protocols that offer security to modern networking, such as [IPv6’s][ipv6] cryptographic algorithms for secure communication between devices on the network. However, as not all smart objects work in the constrained, or industrial environment with legacy systems.

Thus, the IT must be also secured and IoT creates plenty of new attack vectors, and for that I have found very interesting sources of information. For example [Industrial Internet Consortium][iic] provides an excellent security framework known as [Industrial Internet of Things Volume G4: Security Framework][iisf].

I have been studying the framework and learned so much about building a secure environment for IoT. To solve the issue mentioned previously they provide solution by securing the legacy systems to their own "silo" and transferring the data through secured gateway with one way communication.

Really cool stuff and I was really amazed to learn of this solution.

Another interesting point thus far has been endpoint protection on the chapter 8. Especially the *root of trust* concept that:

>provides a foundation to secure other functions at the endpoint, from the hardware to applications including firmware, virtualization layer, operating system, execution environment and application.

The root of trust creates a secure environment for the smart object, and  forming a chain of trust between all the elements of smart object. Chain and root of trusts make sure that when smart object operates, it can be trusted to perform like the designer(s) intended, free from unauthorized tampering, such as replacing hardware components or installing malicious firmware, operating system or other software.

Chain of trust also makes sure that the smart object can be trusted to connect to the network, so that it can be allowed send data to the server. If any of the chain is broken however, then data sending might be compromised and security be at risk.

Bottom line: In order to make everything safe in the IoT, the security framework is a must!

# Discoveries
The world of the embedded system requires for me to combine all my past knowledge. Therefore, I have been very thrilled to have noticed, that I can still learn more and combine my knowledge from past studies such as my vocational education in electronic engineering.

I also have found out that even though I might have not even touched the subject before, I can still start from the bottom and work my way up learning new things along the path. There has not been any sign of me giving up, conversely, I still want to learn more and really feel that I’m nowhere near understanding all the necessary stuff, but I’m getting there!

With my second full month coming, before the on-the-job training ends, I’m ready to continue on this path! Also, expect more frequent updates from now on!

-sorhanp
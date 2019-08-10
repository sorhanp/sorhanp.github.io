--- 
layout: post 
title:  "A month in IoT" 
categories: programming 
description: My findings about IoT, Internet of Things, IIoT, Industrial Internet of Things, protocols, networking and security
tags: IoT, Internet of Things, IIoT, Industrial Internet of Things, protocols, networking, security
excerpt_separator: <!--more--> 
--- 

[last]:/programming/2019/05/26/DevSecOps-weekly-8-2.html

# July 3
Started by first reading on how to install custom, small as possible custom ROM to my Huawei by reading about it from here: https://www.getdroidtips.com/install-unofficial-lineage-os-14-1-honor-8/

Of course first come the rooting: https://www.getdroidtips.com/root-install-twrp-honor-8/

And bootloader unlocking: https://www.getdroidtips.com/unlock-bootloader-honor-8/

Learned that it is no longer possible to unclock huawei... let see if there is a crack... nope..

Well back to Z1 first unlock:
https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader/#unlock-code

Sitten lähdettiin https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader/how-to-unlock-bootloader/#warranty ohjeiden mukaan liikkelle.

Platform toolit käyty: https://developer.android.com/studio/releases/platform-tools.html

Tehty ohjeiden mukaan ja bootloaderin unlokkaus tehty. Seuraavana olisi sitten saada puhelin käyntiin... wanha akku tuntui siltä, että ei jaksanut enää

Mutta jaksoipa kuitenkin! Jatkuu huomenna....

# July 4

Puhelin nytkähtelikin käyntiin, joten seuraava steppi onkin alkaa rootata laitetta! Bootloader on unlokattu!

Illan mittaan sain homman toimimaan ohjeen: 
https://www.cyanogenmods.org/forums/topic/download-and-install-lineage-os-16-on-xperia-z1/

yhdistäen ohjeeseen, jota luin Huaweista ja bingo! Sehän toimii!

# July 6

Aloittelin lukemana Leshanista, joka on Java toteutus LwM2M ratkaisusta. https://github.com/eclipse/leshan/blob/master/README.md

Sitten muistin, että tämän piti olla C/C++, joten hyppäsin takaisin ja tarkastelin Eclipsen Wakaama:
https://projects.eclipse.org/projects/iot.wakaama

Ja asensin Android Studiooni mahdollisuuden kehittää C/C++:
https://developer.android.com/studio/projects/add-native-code

Aloitin tutustumalla https://github.com/eclipse/wakaama koodiin kloonamalla sen.

https://github.com/eclipse/wakaama/blob/master/README.md avulla sainkin jo esimerkki serverin ja testin pyörimään!

Seuraava steppi olikin alkaa luoda serveriä Google Cloudiin ja siitä sitten kokeilla saada yhteys tältä koneelta.

Hyvinhän se yhteys pelaa ja sain esimerkki serverin puhkottua ja nyt sitten se lukee yhteyttä esimerkki clientistä.

Seuraavaksi sitten tutustumaan itse koodiin. Avaan Clionin ja alan tutkia projektia sillä.

# July 7

Aloittelin taasen koodin katselmointia. Opin heti aamusta paljon, esimerkiksi struct:
https://en.wikipedia.org/wiki/Struct_(C_programming_language)

Ja kuinka käyttää sitä linked listoihin:
https://www.learn-c.org/en/Linked_lists
Linked listit ovat kuin arrayt, mutta ne ovat dynaamisia, eli kasvavat ja kutistuvat tarvittaessa. Huonona puolena tietysti, että niihin ei voi vain hypätä, eli PAKKO mennä iteroiden.

Tottakai piti myös vähän kerrata pointereita, varsinkin pointereita pointereihin:
https://www.tutorialspoint.com/cprogramming/c_pointer_to_pointer.htm

Koodi alkoi olla selkeämpää kokoajan. Samalla tutustuin myös:
http://openmobilealliance.org/RELEASE/LightweightM2M/V1_1-20180612-C/OMA-TS-LightweightM2M_Core-V1_1-20180612-C.pdf olevaan APPENDIX E joka opetti, että jokaisella LwM2M objektilla on Object ID:t, jotka sisältävät dataa, eli esimerkiksi objekti 0 sisältää:
Security Object (id: 0)

Server Object (id: 1)

Access Control Object (id: 2) as a skeleton

Device Object (id: 3) containing hard-coded values from the Example LWM2M Client of Appendix E of the LWM2M Technical Specification.

Connectivity Monitoring Object (id: 4) as a skeleton

Firmware Update Object (id: 5) as a skeleton.

Location Object (id: 6) as a skeleton.

Connectivity Statistics Object (id: 7) as a skeleton.

Test Object (id: 31024) with the following description:

Tutustuin myös:
http://www.openmobilealliance.org/wp/OMNA/LwM2M/LwM2MRegistry.html

Testailin myös nettisivulla:
https://leshan.eclipseprojects.io/#/clients/testlwm2mclient

miten tietoa voidaan lukea/observoida/muuttaa laitteesta ja miten lähettää käskyä. Todella kätevää!

Viimeisenä vielä DTLS:n opettelut, eli miten tunnistaudun serverille avaimella. Ei oikein vielä auennut, eli tätä pitää töissä tutkailla!

# July 12
Nyt on aika aloitella koodata omaa versiota clientistä/serveristä ja bootstrapista C++ -kielellä. Ensimmäisenä oman clientin luominen.

Aloittelin lukemalla socketeista 
https://www.geeksforgeeks.org/socket-programming-cc/
JA
https://stackoverflow.com/questions/52727565/client-in-c-use-gethostbyname-or-getaddrinfo

Mutta, koska haluan mahdollisimman helpon yhteyden luomisen, suuntasin katseeni boost.asioon:
https://www.codeproject.com/Articles/1264257/Socket-Programming-in-Cplusplus-using-boost-asio-T

# July 13
Aloittelin uudelleen boost asion katsomista, sillä se jäi eilen kesken ja sainkin socketin ja yhteyden UDP:llä luotua. Pienen boost/make taistelun jälkeen :) Serveri ei vielä vastannut, mutta se on siis seuraava steppi.

# July 14
Tänään ensimmäinen päivä pitkään aikaan kun saa keskittyä toden teolla tekemiseen! Socketit ja yhteydet serverille kunnossa, nyt siis enää ollut pähkäilyä siitä, kuinka luokka tehdään järkevästi.

Sain luotua järkevästi clientin connection classin.  Huomasin kuitenkin, että haasteita edetä seuraavissa stepeissä. Huomasin kuitenkin myös erään kiinnostavan projektin:
https://openhab-nodes.github.io/wakaamaNode/

Klooonaan tämänkin, jotta voin tutustua, millä tavalla tämä API on toteuttu. Tämä ei kuitenkaan sujunut sen kummemmin, sillä päivä alkoi olla jo vähän liian pitkällä. Jatkan tästä myöhemmin lisää.

# July 20
Aloittelin työskentelemään siitä, miten includetaan projektiin vielä wakaaman filut. Kello 12.00 mennessä tämäkin oli vihdoin korjattu sillä aloin ymmärtää paremmin miten CMAKE toimii näiden osalta. Hienoa huomata, että kehitystäkin tapahtuu. Seuraavaksi onkin sitten oman clientin tekemisen aloittaminen!

Aloittelin lightclientin opiskelusta ja teinkin samaan aikaan myös ensimmäisen commitin githubiin. Tästä se sitten alkaa, ja jatkuu huomenna! Kello 14.00 oli aika laittaa hommat pakettiin tältä päivältä ja lähteä liikkumaan ulos.

# July 21
Noniin ensimmäinen päivä, jolloin ei tarvitse keskittyä "säätämiseen" eli seuraavat asiat ovat kunnossa:
- Puhelin laitettu
- Serveri ja Client asennettu ja harjoiteltu niiden logiikkaa
- Clion säädetty kohdilleen
- Harjoiteltu kirjastojen käyttöä, niin ulkoiset kuin sisäiset
- Cmake asetettu uomiinsa

Nyt onkin sitten aika tarttua härkää sarvista ja alkaa oikeasti tekemään!

# July 26
Työviikon päätteeksi vielä perjantai-illan ratoksi vähän koodia. Tutkiskelen vielä, voiko boost.asion saada palauttamaan integerin. Sieltähän se löytyi, eli native handle! Tällä mennään siis viikonloppuun! Nyt kuitenkin alkaa olla niin paljon koodin tuijottelua takana, että siirryn suosiolla tekemään muuta.

#July 27
Sain kasaan ensimmäistä object-luokkaa. Opin myös ennen lopettelua, että liblwm2m.c:n lwm2m_step tekee serverille yhdistämisen.

#July 28
Aloittelin luomaan lisää object-luokkia. Security oli valmis, seuraavana lenkin jälkeen maaliin server.

#August 3
Aika palata Wakaaman pariin ja tehdä server objektille lisää metodeja!
Objektit tulivat valmiiksi, nyt aika saada "game loop" valmiiksi, mutta lwm2m_step failaa, eli aika laittaa se kuntoon.

#August 4
Jatkan stepin tutkimista ja sainkin samalla confin kautta homman kuntoon. Tällä hetkellä siis data liikkuu clientin ja serverin välillä mainiosti! Seuraavaksi aika tehdä tästä hieman dynaamisempi ja ennen kaikkea OOP:n mukainen.

Sain brachin ajettua sisään ja nyt seuraavaksi alkaa ahkera refactorointi. Tämä kuitenkin vasta tulevaisuudessa! 

-sorhanp
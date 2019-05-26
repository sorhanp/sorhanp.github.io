---
layout: post
title:  "DevSecOps weekly, eighth issue. part 1"
categories: programming
description: My findings about database, databases, conceptual model and domain model
tags: database, databases, conceptual model, domain model
excerpt_separator: <!--more-->
---

[last]:/programming/2019/04/19/DevSecOps-weekly-3.html
[mooc_db]:https://tietokantojen-perusteet-19.mooc.fi/osa-3/2-kasiteanalyysi
[oop]:/programming/2018/11/03/Object-Oriented-Programming.html
[data_types]:https://www.w3schools.com/sql/sql_datatypes.asp
[oop_inheritance]:/programming/2018/11/21/You-have-just-inherited-a-large-sum-of-blog-postage.html
[part2]:/programming/2019/05/26/DevSecOps-weekly-8-2.html

This is the final week before my on-the-job learning period begins. I have strongly focused my last couple of weeks on what kind of knowhow I need in order to operate with best of my knowledge at the job. These include finishing “Programming with Java I”-course and started working on “Introductory to Databases”-course. On this blog post, I want to focus on how a conceptual model and domain model can be utilized when designing databases. <!--more--> 

## Overview 
Let’s begin by setting up an example of what kind of requirements may present for a software. The text below is translated and modified a bit from [Introductory to Databases MOOC][mooc_db], that is only available in Finnish. 

>Our online auction service needs to offers registered customers the opportunity to place their products on auction. Each registered customers' contact information must be stored. Each product is linked to one or more categories, which are used as a search term. There may be several products in each category. Adding a product to the online store needs to be straightforward: the customer writes the product information, marks the categories the product belongs to, determines the start and end time of the auction, and sets a minimum price. Anyone can bid on the product and when leaving an offer, the bidder provides their contact information. Those interested in the product may also send questions to the seller through the system. Questions must pass through the system to the seller, as well as the seller's possible answers to the questions are sent through the system to the inquirer. The seller may choose to publish the question and answer, in which case both are released along the product information. 

These requirements mean, that problem has been found and that it needs to be solved via a software, namely with a database at the back end. I will call above text problem description from now on. 

Even though the problem is well defined, it is still very abstract, in terms of an application, and it needs to be made more concrete. To put it simply, main **concepts** and the **features** of these concepts must be found. 

## Conceptual model 
Conceptual model helps to conceive the problem at hand. Of course, programs and databases can be written without any care in the world and not give a hoot about the concepts behind the problem. Needless to say, this method is not very productive and can lead to mistakes that need to be corrected later down the line. 

Aim of a conceptual model is to provide a data model of the problem. This data model includes all the necessary concepts and their relationships, as well as attributes associated to each concept. Goal is to prevent mishaps, such as not taking every aspect of the problem into account. Alternatively, too many aspects can be considered, allowing creation of a system that is way out of scope of the problem. 

*A good beginning makes a good ending*, especially when working in a team. When conceptualizing the problem, it is much easier to discuss about the problem with your co-workers, leaders or customers. Since every stakeholder might have a different view on the problem, conceptualizing creates a common interpretation of it, thus preventing misunderstandings.  

It also provides key decision-making elements for leaders, such as scope of the project, what kind of personnel are needed etc. When the problem is conceptualized, it is much easier to know what needs to be solved and what is not necessary to be added to final product. 

I have dabbled with the idea of conceptualization in the past. For example, [my object-oriented programming blog post][oop] revolves around the same idea, in which I stated: 

> Classes are like blueprints, or guidelines, for the object, so one can go and build an object (in this case one mobile phone) from it... 

Like classes, concepts are abstractions. Concepts can be, and usually are, related to each other. I learned from object-oriented programming that mobile phone can have an owner, and owner can go to work in a certain company etc. This is the case also with concepts. 

## Gone conceptualizing 
Now that you understand what the conceptual model aims to bring to the table, the *what* and *why* of it. Next step is to understand *how* conceptual model is formed. The process is fivefold: 

1. Recognize the concept candidates 
2. Recognize the relationships between concepts 
3. Recognize and define the cardinality constraints 
4. Recognize the attributes of concepts 
5. Generalize and individualize the concepts 

I will go through each of them in their own header, using the problem description presented in the overview header as an example. 

# Recognize the concept candidates  
The process starts with finding out what are the possible concepts candidates from the description. Goal is to find out **noun phrases and words**, and at this stage it is not important to find the correct ones, but rather gather all of them to a list. There are at least these candidates: 

- auction service 
- customers 
- products 
- contact information 
- categories 
- search term 
- store 
- product information 
- price 
- offer 
- bidder 
- question 
- seller 
- system 
- inquirer 
- answer 

What happen next, is thinking which one of these concepts are necessary in terms of the scope of the upcoming program. For example, system is right out, because it is what is being designing here, it isn’t part of the final system, it **IS** the system. Here I have crossed out the concepts that I believe are not necessary, and added a brief reason why: 

- ~~auction service~~ - this is the same as “system”. 
- customers 
- products 
- ~~contact information~~ - this can be *an attribute* of “customers”. 
- categories 
- ~~search term~~ - this is something that each “products” and “categories” determines, no need to make a concept out of it. 
- ~~store~~ - this is the same as “system”. 
- ~~ product information~~ - this can be *an attribute* of “products”. 
- ~~price~~ - this can be *an attribute* of “products”. 
- offer 
- ~~bidder~~ - “customers” is already a chosen concept, type of “customers” can be determined as *an attribute*, if necessary. 
- question 
- ~~seller~~ - this is the same as “bidder”. 
- ~~system~~ - already defined why on the paragraph above. 
- ~~inquirer~~ this is the same as “bidder”. 
- answer 

I have recognized few nouns as *attributes* of a certain concept. What does that mean? Well in short, they are features, that concepts have. I will go deeper about attributes on the header “Recognize the attributes of concepts”.  

So, all in all there are six concepts recognized from the problem description. It is important to turn them all in to nominative form so that they represent a single concept, thus customers become customer and so forth. Here is the final list of concepts in their nominative form: 

- customer 
- product 
- category 
- offer 
- question 
- answer 

When doing this step, I felt that it made that long text scroll that I provided much simpler to understand. I could think in my head that, “this system is going to need a database with customers table in it, and each customer has a product to sell, so it must be linked to the customer via foreign key” etc. Making me already see the vision inside my head on how to carry on from this.  

I found this to be very powerful method that provides direction on where to go, even at the first step and I’m sure that this comes in handy in general programming also, since these concepts can be turned in to classes when doing object-oriented programming. 

# Recognize the relationships between concepts  
Whereas last step was all about nouns, this is a section where we are doing things. That’s right, it is time to go hunting for verbs. To put in broad terms, the idea is to find out by reading the problem description, what sort of relation each concept might have with each other. Let’s go through the text and find out sentences that connects concepts together: 

> ...registered customers the opportunity to place their products on auction... 

> ...product is linked to one or more categories... 

> Anyone can bid on the product and when leaving an offer, the bidder provides their contact information. 

> Those interested in the product may also send questions to seller... 

> Questions must pass through the system to the seller... 

> …the seller's possible answers to the questions are sent through the system to the inquirer 

> ... seller may choose to publish the question and answer, in which case both are released along the product information. 

From the we know that **customer** is related to *product*, **product** is related to *category*, **offer** is related to *product* AND *customer*, **product** is related to *question*, and finally **answer** is related *question*. 

Here are the relationships drawn as a primitive domain model: 

![Concepts relationship](/assets/concepts_relationships.svg) 

# Recognize and define the cardinality constraints  
Cardinality constraints is a fancy way of saying limitations between relationships. Example of such constraint is this real-life example: “every **human being** has exactly one biological *father*”. 

Third step of the process of conceptualization is to observe and specify said limitations between discovered concepts. Limitations are marked with special markings to the domain model’s lines between concepts. Limitations are as follows: 

- One to many (1-*) 
    - A relationship between two concepts where a concept can have multiple relations on another concept. For example; “each product is linked to one or more categories”. 

- One to one (1-1) 
    - A relationship between two concepts where a concept can have only one relation to another concept. This is a very rare one, but for example; “The seller may choose to publish the question and answer”, since there is one question and only one answer to that question, one to one relationship is made when question is answered. 

- Many to many (\*-\*) 
    - A relationship between two concepts where a concept can have as many relations to other concept. For example; “there may be several products in each category”. 

Often these limitations are stated by the problem description, like in above examples provided, but that is not always the case. Sometimes deeper knowledge about the subject at hand is also necessary when finding out the constraints. This is when the power communication with stakeholders comes to play, since they are the experts. 

Via communication one may learn, how the problem has been solved before and device a cardinality constraint from there. For example, if the old online auction shop only has ability to store only one question-answer-pair per product, then the question is simple, do we keep the old way of doing or is it necessary to improve the design? 

From reading the problem description, it is possible to conclude that one product can have multiple categories, and each category can hold multiple *different* products. Customer can have multiple product on sale and one customer can offer a bid on multiple products. There can multiple offers on a product. One product can have multiple questions, but one question can have only one answer. 

Here are the cardinality constraints added to the primitive domain model:  

![Concepts relationship with cardinality constraints](/assets/concepts_relationships_cardinality_constraints.svg) 

# Recognize the attributes of concepts  
Fourth step is finding out the attributes to the concepts provided. But what are these attributes then? I brought up the subject already on the first step when discovering nouns from the problem description. 

Attributes define and differentiate the same type of concepts from each other, Customer A’s name is A and leaves in Atown, whereas Customer B’s name is B and Btown. In short attributes are features that define the concept, such as product that has categories the product belongs to, the start and end time of the auction, and a minimum price.  

I have mentioned the scope of the problem before. It means that only the defined problem should be solved without unnecessary features.  This is the point where scope should be very closely kept in mind. There is no need to add attributes that do not contribute to the final product, such as weight of the customer in an online auction. 

As seen, when recognizing attributes, the problem definition can help finding them, and as always communication with stakeholders is important. Since someone usually knows what kind information they want, or wish, to gather from their customers or products. 

Here are the attributes and their [data types][data_types] added to the not-so-primitive-anymore domain model:  

![Concepts relationship with attributes](/assets/concepts_relationships_attributes.svg) 

As can be seen from the picture, attribute name is followed by planned data type for that attribute. Data type defines what kind of data can stored inside the attribute. Quick recap of the data types used in the attributes. String is text, Boolean is one of two possible values (true or false), Date is date stored in day-month-year-format and Double is floating point value such as 3.14. 

Conceptual model is getting to the territory where it is starting to look like it can be used to form a database. 

# Generalize and individualize the concepts 
Final step is sort of like a cleanup to make sure that conceptual model doesn’t have overlapping or repetition, as don’t repeat yourself (DRY), is in effect here too. Thus, if any of the concepts have exactly same attributes in them, it could mean that one concept is a “special case” of another concept. Goal is to identify them and generalize them. 

I already did something like that at the first step. Take a look at these concepts: 
- customers  
- ~~bidder~~ - “customers” is already a chosen concept, type of “customers” can be determined as *an attribute*, if necessary. 
- ~~seller~~ - this is the same as “bidder”. 

In this case if there would have been no customer, but rather two different concepts such as “bidder” and “seller”, both of them would have looked like this on the domain model:

![Concepts relationship, dry example](/assets/dry_example.svg) 

As can be seen, the same information is repeated twice. Because of that it is a good idea to generalize both concepts in a one singular concept called “customer”. 

Individualizing needs to happens in situations where there would have been three concepts, such as “customer”, “bidder” and “seller”, again all with the same information, but with slight differences:

![Concepts relationship, dry example](/assets/another_dry_example.svg)  

In this case it would have been an excellent idea to keep all the “customer” attributes as it is and leave only the unique attributes (marked in red text with green background) of “bidder” and “seller” remain in their respective concepts.  

One might wonder how on earth can be same attributes be utilized by both. This is possible because both concepts can inherit all the attributes from “customer”-concept. This way, there is only one instance of each attribute, and repeatable attributes are copied by inheritance to other concepts. For further reading, I have written an article about [inheritance in object-oriented programming][oop_inheritance]. 

# Conclusion 
Road to databases has just begun! Next up is processing the ready conceptual model to a database schema, which can be then used to build real life database. Join me on my next [blog post][part2], which I will go through the process in greater detail.

-sorhanp
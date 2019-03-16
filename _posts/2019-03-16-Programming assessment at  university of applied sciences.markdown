---
layout: post
title:  "Programming assessment at university of applied sciences"
categories: programming
description: My findings about C++ (CPP, or cpp), programming assessment, MySQL, mysql, database and databases
tags: programming, c++, object-oriented, cpp, mysql, MySQL, database, databases
excerpt_separator: <!--more-->
---

[last]:/programming/2019/03/06/Exponents-raised-to-the-power-of-C++.html
[jamk]:https://www.jamk.fi/en/
[github_page]:https://github.com/sorhanp
[relational_db]:https://computer.howstuffworks.com/question599.htm
[virtualbox]: https://www.virtualbox.org/
[ubuntu]:https://www.ubuntu.com/
[emma]:http://www.ubuntugeek.com/emma-graphical-toolkit-for-mysql-database-developers-and-administrators.html
[sql_workbench]:https://www.mysql.com/products/workbench/
[sqldriverconnect]:https://docs.microsoft.com/en-us/sql/odbc/reference/syntax/sqldriverconnect-function?view=sql-server-2017
[visual_studio]:https://visualstudio.microsoft.com/
[cppconn_windows]:http://download.nust.na/pub6/mysql/doc/refman/5.1/en/connector-cpp-apps-windows-visual-studio.html
[cppconn_ubuntu]:https://codeforces.com/blog/entry/48328

This week I attended to my [local University of Applied Sciences][jamk] programming competence assessment. The assessment came in to parts; first, I filled a self-evaluation form to give information about me, my prior programming knowledge and of course important links, such as my [Github-page][github_page]. Second part was to participate in a programming examination at the campus’s computer lab. After the examination, lecturers reviewed and gave feedback based on the results. Here is a documentation of that day, and what I managed to produce during the five hours allocated to the examination. <!--more-->

The goal of the examination was to program a dictionary-program that allows users to add words to the program and execute a search for word. The program was graded on how many features the program had, so for example if the program had database where the words are added instead of plain text file, or if the program has a graphical user interface, the greater the score. I did not aim for highest possible score, but instead took the day as learning experience. I knew that I could program a very simple, yet effective, command line-program that follows object-oriented paradigm in a matter of hours. So instead I spent most of my time learning about how to implement database to C++-program, because I know that it is something that is required from me later. Of course I already knew how to create and manage [a relational databases][relational_db] from my past experiences with PHP and data warehouses, but I have not implemented that knowledge to other programming languages, such as C++, but that was about to change.

I will go through the day in chronological order, hence I started with creation of the database. The database was installed on a [VirtualBox][virtualbox] running an [Ubuntu-Linux’s desktop edition][ubuntu]. I used software called [Emma][emma], which is graphical toolkit for MySQL databases, it allows create and modify databases, tables and associated indexes with dialog boxes instead of typing the commands to MySQL-command line. I’m not so familiar with creation of tables with commands, so I thought that this would be bit faster. I created database called dictionary and added single table for Finnish-Swedish word pairs. The table in question looked like this, with example row 1:

| fi_swe_id <br/>(primary key) | fi_word  | swe_word  |
|:-:|:-:|:-:|
| 1 | koira | hund |

After that I tested if I can access the database from the main operating system of the computer, since I wanted to make program with [Visual Studio 2017 on Windows-platform][visual_studio]. For testing the connection between main and guest operating system I used [MySQL Workbench][sql_workbench] for Windows. Everything worked fine and connection was established as it should have been. Next I started working on the connection to the database with a test program written in C++. However, the [SQLDriverConnect Function][sqldriverconnect] was not installed on the Visual Studio 2017 and I did not have admin rights to install new addons to the program. So instead of adding [MySQL Connector/C++ for Windows][cppconn_windows], I decided to keep on writing the program also on Ubuntu, because I have already used enough time studying about Visual Studio’s database-drivers.

Before lunch break I installed [Mysql Connector/C++ on Ubuntu][cppconn_ubuntu] and used the example code to test the connection. It worked nicely, so it was time for me to start programming the dictionary application after lunch break. I first created a class for database, so that the database connection and query running can be done via dedicated class, instead of repeating code through the program. Here is the header file database.h for class “Database”:
{% highlight cpp %}
//include cppconn-header files to database.h-file
#include "mysql_connection.h"

#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/statement.h>

//Create Database-class
class Database{
  //declare private data members of database-class
private:
  sql::Driver *driver;
  sql::Connection *connection;
  sql::Statement *statement;
  sql::ResultSet *result;
  std::string query;

  //declare public methods of database-class
public:
  ~Database();
  bool Connect();
  bool Disconnect();
  bool SetQuery(std::string queryInput);
  void RunQuery();

};
{% endhighlight %}

Here is the implementation file database.cpp:
{% highlight cpp %}
#include "database.h"

Database::~Database(){

};

bool Database::Connect(){
  //Try to create a connection to database
  try{
  driver = get_driver_instance();
  connection = driver->connect("tcp://127.0.0.1:3306", "root", "root");

  //Connect to the database table dictionary
  connection->setSchema("dictionary");

  //Return "0" if connection was succesful
  return 0;
  }
  //Catch possible errors
  catch(sql::SQLException &e){
    std::cout <<"# ERROR: SQLException in " << __FILE__;
    std::cout << "# ERROR: " << e.what();
    std::cout << " (MySQL error code: " << e.getErrorCode();
    std::cout << ", SQLState: " << e.getSQLState() << " )" << std::endl;
    //Return "1" if connection was unsuccesful
    return 1;
  }

};

bool Database::Disconnect(){
  delete result;
  delete statement;
  delete connection;
}

bool Database::SetQuery(std::string queryInput){
  query = queryInput;
  return 0;
};

void Database::RunQuery(){
  try{
  statement = connection->createStatement();
  statement->execute(query);
}
//Catch possible errors
  catch(sql::SQLException &e){
  std::cout <<"# ERROR: SQLException in " << __FILE__;
  std::cout << "# ERROR: " << e.what();
  std::cout << " (MySQL error code: " << e.getErrorCode();
  std::cout << ", SQLState: " << e.getSQLState() << " )" << std::endl;
  }
}
{% endhighlight %}
Idea of this class being that SetQuery-method can be used for setting SQL-query in to query-variable which is of string-type. After that RunQuery-method executes the query stored to variable.

Next up I created another class for user interface called “Interface”. Here is the declaration file called interface.h:
{% highlight cpp %}
#include "database.h"

class Interface{
  //declare private data members of interface-class
private:
  Database dictionary;
  //declare public methods of interface-class:
public:
  //Constructor for interface-class:
  Interface();
  //Other public methods:
  void Greetings();
  bool Selection();
  void AddWord();
  void SearchWord();
};
{% endhighlight %}

And here the implementation:
{% highlight cpp %}
#include "interface.h"

Interface::Interface(){
  Greetings();
  Selection();
};

void Interface::Greetings(){
  std::cout << "Welcome to Finnish-Swedish dictionary v.0.01 alpha" << std::endl;
};

bool Interface::Selection(){
  int UserInput;
  std::cout << "Press corresponding key to make selection" << std::endl;
  std::cout << "1) Add word pair to dictionary" << "\n";
  std::cout << "2) Search from dictionary" << "\n";
  std::cout << "9) Quit" << "\n";
  std::cout << ">> ";
  std::cin >> UserInput;

  if(UserInput == 1){
    AddWord();
    Selection();
  }
  else if(UserInput == 2){
    SearchWord();
    Selection();
  }
  else if(UserInput == 9){
    return 0;
  }
  else{
    Selection();
  }

};

void Interface::AddWord(){
  std::string FinnishUserInput;
  std::string SwedishUserInput;

  std::cout << "Adding Finnish-Swedish word-pair to dictionary" << "\n";

  std::cout << "Please type in the Finnish word: ";
  std::cin >> FinnishUserInput;

  std::cout << "Please type in the Swedish word pair: ";
  std::cin >> SwedishUserInput;

  dictionary.Connect();
  dictionary.SetQuery("INSERT INTO dictionary.fi_swe(fi_word, swe_word) VALUES ('" + FinnishUserInput + "', '" + SwedishUserInput + "');");
  dictionary.RunQuery();
};

void Interface::SearchWord(){
  std::string UserInput;

  std::cout << "Search Finnish-Swedish word-pair to dictionary" << "\n";

  std::cout << "Please type in the Finnish or Swedish word: ";
  std::cin >> UserInput;


  dictionary.Connect();
  dictionary.SetQuery("SELECT fi_swe_id, fi_word, swe_word FROM fi_swe WHERE (fi_word LIKE '" + UserInput + "' OR swe_word LIKE '" + UserInput + "');");
  dictionary.RunQuery();
};
{% endhighlight %}

The most interesting part of this was to learn how to use variables in a SQL-statement such as INSERT INTO. To do this SQL-statements ‘-characters must be enclosed like this: " + YourVariableHere + ". So the statements become like this: 
> SELECT fi_swe_id, fi_word, swe_word FROM fi_swe WHERE (fi_word LIKE '" + UserInput + "' OR swe_word LIKE '" + UserInput + "');

With these I was able to gather about half of the points from the possible features. The code can, and should be expanded, which is the reason why I “took the code home”, so that I can add rest of the features, which were necessary for higher grade. Anyway, I had much fun learning how to connect to database using other programming languages, instead of good ole PHP. I also got good feedback from lecturer on my past blog entries, since I send address to this blog on the self-evaluation form. My self esteem grew a lot and it also felt really good to program, since I have not been planning and programming a program in this scope in a long while. 

-sorhanp
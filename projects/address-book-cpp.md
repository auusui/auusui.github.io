---
layout: project 
type: project
image: images/linux.png
title: "Address Book C++"
permalink: projects/address-book-c
# All dates must be YYYY-MM-DD format!
date: 2020-12-14
labels:
  - C++ coding
  - Debug mode
  - Linking and Compiling
summary: Created a simple address book that takes user input and stores it into the struct record.  The struct record holds the items in a "record" and allows the database to find it in the memory.
---

## Operating System

For this project, I used Linux, which is an operating system just like iOS and Mac OS.  This is the system that my class dealt with the whole course.  On Linux, I learned the different commands you can use such as, ls (to list the files in the directory), mkdir (to make a new directory), cp ./filename.c ../data/file.c ( to copy contents of one file into another), cat filename (to see what is inside a file without having to go into it), and so many more.  The beauty of this system is that you can use different languages, and the languages we used were C, C++, and Java.  I also learned compilation and linkage through the system and how it works.  Compilation was mostly done in a Makefile that updates everything inside of the directory that is mentioned in this Makefile.  For example for C language: 
```ruby
project: user_interface.o
        gcc -o project user_interface.o

user_interface.o: user_interface.c record.h
        gcc -ansi -pedantic-errors -Wall -c user_interface.c
        
clean:
        rm *.o project
```

The first section creates the object file and project will be the name of it.  The second section is to compile the file with the linkage as well.  Makefile would typically be used for a large amount of files that need to be compiled so that all files can be compiled and linked with one work "make" instead of writing out the 4th line 100 times.  


## About the Project

The address book has the options add record, delete record, find record, print all records, and quit.  The whole database will be using the struct record which acts as one whole address with the elements account number, name, and address as shown below. 

```ruby
#ifndef Record_H
#define Record_H

struct record
{
    int accountno;
    char name[25];
    char address[80];
    struct record * next;

};

#endif
```

The database will be able to access all three of these elements.  The user will be asked to fill in the appropriate information for the option he or she picks.  The way the user picks an option will be to type "add", "delete, "find", "printall", and "quit", but the user can also input a partial of the words given ("ad", "fin", "del").  Another addition to the address book record is that each time the user adds a record, it will be organized into descending order.  The program will loop and keep showing the user the options once each operation is carried out.  The program will end when the user choose to quit.  This is when all the records in the memory will be saved to a text file, and the memory will then be wiped.  The user will still be able to access these files when he or she reenters the database.  A readfile function will activate and copy the records from the file back into the struct records.  


## My Thoughts

This was a remake of my previous address book listed, but in C++ language.  I honestly say that I like C++ language a lot more that C.  I feel like it is easier to code and get direct results than C.  I am no expert on it, but I definitely coded a lot smoother with C++.  I had way less errors to fix, and it was easy to fix the errors that showed up.  This project was still challenging in its own ways because we were required to make two different makefiles, and I had trouble figuring out how to make them separate and not be the same linking.  Let's just say that Google and StackOverflow was my best friend during this course :).  I had the easiest time creating the cases for all the problems that could occur because we couldn't let our program crash.  One of my issues in the first take was the delete option would delete everything if the first record was deleted.  I fixed that problem in this second take.  I fixed it up as much as I could, but if time wasn't a pressing matter, I feel like it could've been a lot better.  

### Links to my code
* [User Interface](https://github.com/auusui/auusui.github.io/blob/master/user-interface-cpp.md)
* [Functions](https://github.com/auusui/auusui.github.io/blob/master/functions-cpp.md)

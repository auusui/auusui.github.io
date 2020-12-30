---
layout: project 
type: project
image: images/linux.png
title: "Address Book"
permalink: projects/address-book-c
# All dates must be YYYY-MM-DD format!
date: 2020-12-14
labels:
  - C coding
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

The database will be able to access all three of these elements.  The user will be asked to fill in the appropriate information for the option he or she picks.  The way the user picks an option will be to type "add", "delete, "find", "printall", and "quit", but the user can also input a partial of the words given ("ad", "fin", "del").  The program will loop and keep showing the user the options once each operation is carried out.  The program will end when the user choose to quit.  This is when all the records in the memory will be saved to a text file, and the memory will then be wiped.  The user will still be able to access these files when he or she reenters the database.  A readfile function will activate and copy the records from the file back into the struct records.  


## My Thoughts

This project gave me a lot of headaches, but what's new?  This course was challenging because our professor made the project descriptions vague so that we would research and learn how to do it on our own.  I may not be a fan of this process because I like to know why I am doing what I am doing in code so that I can use it again in the future should it come up again.  I did learn a lot during this course, however.  I learned how to fix my mistakes and figure out where the problems stemmed without using a debug to help me.  I learned how to work around different options and coded different techniques to get the result I wanted.  I feel like this course made me think literally like a database, which really helped me in many of my other classes as well.  It was difficult learning on my own, but no one said the best rewards come from easy work.  I definitely earned my grade in this class.

### Links to my code
* [User Interface]()
* [Functions]()

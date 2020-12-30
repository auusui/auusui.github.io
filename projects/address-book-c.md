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



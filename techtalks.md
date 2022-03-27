---
layout: page
title: Tech Talk Notes
subtitle: Notes for each Tech Talk
---
# Navigating Notes and Plans for Each Tech Talk
In each Tech Talk, I will prepare questions and review the Tech Talk material beforehand. I will take notes on important key concepts for each TT.

After completing the challenges associated with each TT, I will record my progress, struggles & key learnings in this Github Page (or on an alternative Jekyll site). TT challenge code will be executable through Repl.it.

### TT0:

Data Structures are: method of organizing data. Types of data structures --> primitive (intger, float, String, Boolean) & Non-primitive (Arrays, Lists)
![image](https://user-images.githubusercontent.com/40574565/158223705-2bd7992a-ca34-415a-a161-fdfd26a12b1e.png)

Data Structures and Algorithms go together
* Data structures have the data & the algorithms access the data
* similar to how a for loop iterates through an array to access the data in an array

Imperative Paradigm & Object Oriented Paradigm
* Imperative paradigm -- uses statements to change a program's states
* Procedural Programming is a type of imeprative programming based on procedures
* Object Oriented programming -- classes and objects (what we've been doing in class) -- defining classes, extending classes, subclass-specific behavior & polymorphism

Structured programming has techniques to improve maintainability (diff from imperative paradigm)

### TT1:
Linked Lists:
![image](https://user-images.githubusercontent.com/40574565/158735792-66ba4670-8bf5-478f-86de-c7704b990110.png)
Each object in a linked list have the data and a pointer to the next object.
* Linked lists are a way of managing a list of objects 

To access the data from an object, tmp illustrates this

##### Queues (First in First out)
keeping track of first in & first out
* need to keep track of current node for iteration

##### Stacks (Last in First Out)
* built using linked list objects keep track of last item inserted 


### TT2
Mathematical expressions are essentially a finite combination of symbols that execute according to certain rules

We convert strings to Reverse Polish Notation using Shunting-yard algorithm

##### Shunting-Yard Algorithm
Essentially an algorithm used to parse arithmetical expressions (so, algorithm for PEMDAS expressions)
* It is stack-based

Infix expressions: The mathematical notation most people are used to
* e.g.: 3 + 4
* 3 + 4 x (2-1)

The program converts the infix expressions to **Reverse Polish notation**
* "3 4 +"
* "3 4 2 1 - x +"

![image](https://user-images.githubusercontent.com/40574565/159420116-28297795-8713-40aa-996a-60418749962f.png)

For the challenge this week: 
* Need to consider how numbers need to be formatted from infix expressions to RPN
* Figure out the operators & seperators Hash Map thing

##### STEPS for calculating RPN:
1. seperate numbers from String into tokens
2. Put the tokens into RPN 
3. Change RPN to calculation

CHALLENGES:
need to write calculator
write "power of" operation


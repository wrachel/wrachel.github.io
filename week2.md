---
layout: page
title: Week 2 Challenges
subtitle: Notes & Code for week 2
---
### Challenge #1:
[Link to code on Github](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/Calculator.java)

Code snippet:
```java
    private void rpnToResult()
    {
        // Stack used to hold calculation while process RPN
        Stack calculation = new Stack();

        // for loop to process RPN
        for(String a : this.reverse_polish){
            if(!isOperator(a))// If the token is a number
            {
                calculation.push(a); // Push number to stack
                //System.out.println("Enqueued: "+ a);
            }
            else// else
            {
                Double topEntry = Double.valueOf((String) calculation.pop());// Pop the two top entries
                Double nextEntry = Double.valueOf((String) calculation.pop());

                // Based off of Token operator calculate result
                Double result = 0.0; //create variable to store the resulting calculation
                if(a.equals("+")){
                    result = nextEntry + topEntry;
                    //System.out.println("Result: " + result);
                }
                else if(a.equals("-")){
                    result = nextEntry - topEntry;
                    //System.out.println("Result: " + result);
                }
                else if(a.equals("*")){
                    result = nextEntry * topEntry;
                    //System.out.println("Result: " + result);
                }
                else if(a.equals("/")){
                    result = nextEntry / topEntry;
                    //System.out.println("Result: " + result);
                }
                else if(a.equals("%")) {
                    result = nextEntry % topEntry;
                    //System.out.println("Result: " + result);
                }
                else if(a.equals("^")){
                    Double value = nextEntry;
                    for(int i = 0; i < topEntry - 1; i++){
                        value *= nextEntry;
                    }
                    result = value;
                }
                //System.out.println("Result: " + result);
                calculation.push(String.valueOf(result)); // Push result back onto the stack
            }
        }
        // Pop final result and set as final result for expression
        this.result = Double.valueOf((String) calculation.pop());
    }
```
Essentially how the calculator works is, after the expression is in RPN format, I iterate through the String Arraylist reverse_polish which is the reverse polish notation.

Then, if the token is not an operator (essentially, it is a number) I push it to the stack. 

Otherwise, if the token is an operator than I pop the top two values off the stack and perform an operation on these values.
I had to create individual (if) statements to check the operator. If it is a %, ^, +, -, *, /, etc. Then, I store the value obtained from the operation in "result" and push result back into the Stack
This is essentially how we calculate from RPN notation.

One thing that is notable is that when you pop the value off of the stack, it is initially an object. You need to convert that object into a Double. 


### Challenge 2: 
[link to code](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/Calculator.java#L158)

In order to add a "^" function, you need to make sure that the ^ function is available in the Operators hash map, and in the necessary method (e.g. tokensToReversePolishNotation) so that the ^ operator is recognized as a token.
```java
 OPERATORS.put("^", 2);
```
```java
private void tokensToReversePolishNotation () {
        ...
    case "^":
        }
```
And then, in the rpnToResult() function, add an additional "if" statement that considers what to do with the values when the "^" operator is used.
```java
else if(a.equals("^")){
                    Double value = nextEntry;
                    for(int i = 0; i < topEntry - 1; i++){
                        value *= nextEntry;
                    }
                    result = value;
                }
```
and of course, push "result" back to the stack
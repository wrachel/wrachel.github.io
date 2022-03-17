---
layout: post
title: Challenge Week 0
subtitle: Notes & Review from Tech Talk Week 0
tags: [challenges, week0]
---
### TT0:

Links to Github for Code: [Challenge 1: menu](https://github.com/wrachel/tri3Individual/blob/master/tri3Individual/src/menu.java)
**KEY LEARNINGS**: using the HashMap to with a **Runnable action** so that the main file of each challenge can be run. This was probably the most important, key part to figuring out this challenge. This also helps keep all the challenges organized so that the menu can iterate through the HashMap.
'''
Map<Integer, menu> Menu = new HashMap<>();

        Menu.put(1, new menu("IntByReference", () -> IntByReference.main(null) ) );
        Menu.put(2, new menu("Matrix", () -> Matrix.main(null) ) );
        //print the menu
        System.out.println("Menu:");

        for (Map.Entry<Integer, menu> pair : Menu.entrySet()) {
            System.out.println(pair.getKey() + " - " + pair.getValue().getTitle());
        }

        //scanner gets user input for menu selection
        int input = sc.nextInt();

        try {
            //according to user input, return the method at the Map's index
            menu m = Menu.get(input);
            //run action
            m.getAction().run();
            System.out.println("");

Another interesting thing was the **try and catch** implementation. Essentially, the try & catch helps account for user error (if the user puts an int that is invalid)

        } catch (Exception e){
        
            System.out.println("Something went wrong. Please try again. \n");


Links to Github for Code: [Challenge 2: IntByReference (put lower number first)](https://github.com/wrachel/tri3Individual/blob/master/tri3Individual/src/IntByReference.java)
**Key Learnings**
implementing getters and setters so that in the swapToLowHighOrder function, we can actually use the getters and setters to swap the values

    public void swapToLowHighOrder(IntByReference a){
        //if condition to switch if the 1st value is bigger than the 2nd
        if(this.value > a.getValue()){
            //swapping values of a, b
            int temp = this.value; 
            this.value = a.getValue(); //using getter
            a.setValue(temp); //using setter
        }
    }

Also, another interesting thing to mention is that with this method, using a "temp" variable is necessary in order to be able to actually swap the values.

Links to Github for Code: [Challenge 3: Matrix (format Array output)](https://github.com/wrachel/tri3Individual/blob/master/tri3Individual/src/Matrix.java)

**KEY TAKEAWAYS** : the Matrix challenge was definitely a little harder, but the most **key** takeaways here is understanding the toString method and nested for loops to iterate through a 2D array.

First, for **toString method**, it's key to solving this challenge to understand that toString methods can be used to access data within an Array. So, for each value in the 2D array, I would assign it to a returnStatement variable which I then had to format (through \n statements and spaces, etc.).

        public String toString(){
        ...
           return returnStatement;
        }

For the **nested for loops**, I used it to actually access the values within the 2D array and assign them to the return Statement.

        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[i].length; j++){
                //nested for loop to access values in 2D array
                if(matrix[i][j] < 0 ) {
                    returnStatement += "  ";
                }
                else if (matrix[i][j] > 9){
                    returnStatement += Integer.toHexString(matrix[i][j]) + " ";
                }
                else {
                    returnStatement += matrix[i][j] + " ";
                }

            }
            returnStatement += "\n";
        }

Notably, I also had to add if statements to deal with certain conditions (e.g., if the number is less than 0 it becomes a space and if the number is greater than 9 it becomes hex. Although technically if its greater than 0 its hex, but it's just easier for my brain to process this way.) The printed statement also needs the values in the 2D array in reverse, so I just did this by having the same nested for loop, but starting from the end of the 2D array and going backwards.

        for(int i = matrix.length - 1; i >= 0; i--){
            for(int j = matrix[i].length - 1; j >= 0; j--){

---
layout: page
title: Week 1 Challenges
subtitle: Notes & Code for week 1
---
### TT1:
Review of Linked Lists
* Essentially Linked lists are a way of organizing data
* Linked lists contain Data and a node that points to the next object (links to other nodes)

``` java
//constructor
public LinkedList(T data, LinkedList<T> node) {
    this.setData(data);
    //sets data
    this.setPrevNode(node);
    //sets previous node
    this.setNextNode(null);
    //sets next node as null 
}
```

Review of Java Generic T
* in the code, the Java Generic T is used for LinkedList
```java
LinkedList<T> head, tail;
```
* Generics essentially help create related methods or classes with a single declaration 
* Generic classes are kind of like a template to be used to create concrete classes from
  * they help reduce compile-time errors
* Specifically, the java Generic T is used here:
```java
class QueueIterator<T> implements Iterator<T>
```

#### Links to Github for Code: [Challenge 1: Displaying the Queue](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/Queue.java) & the [tester function](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/QueueTester.java)

How the "add" process works
add function
```java
public void add(T data) {
        // add new object to end of Queue
        LinkedList<T> tail = new LinkedList<>(data, null);
        
        if (head == null)  // initial condition
            this.head = this.tail = tail;
            
        else {  // nodes in queue
            this.tail.setNextNode(tail); // current tail points to new tail
            this.tail = tail;  // update tail
        }
    }
```
is used in the addList function
```java
public void addList(T[]... seriesOfObjects) {
        for (T[] objects: seriesOfObjects)
            for (T data : objects) {
                this.queue.add(data);
                //adds the data from the current object into the queue 
                this.count++;
                System.out.println("Enqueued data: " + data);
                printQueue();
            }
    }
```
Essentially, how the "Enqueue" data process works is that the addList function iterates through the series of Objects, then adds the object to the queue. The Enqueued data statement tells users what data entry is being added. Then the function calls the printQueue() function which prints the queue.

How the "delete" process works:
```java
public void deleteList(T[]...seriesOfObjects){
        for (T[] objects: seriesOfObjects)
            for (T data : objects){
                this.queue.delete(data);
                this.count--;
                System.out.println("Dequeued data: "+ data);
                deQueue();
            }
    }
```
Here, the deleteList function calls the "delete" method which essentially deletes the data
```java
    head.getNext().setPrevNode(tail);
        head = head.getNext();
```
by setting the "current" head as the next head, it essentially removes a piece of data
Finally, the dequeue function prints out the current queue 

#### Links to Github for Code: [Challenge 2: Merging Queues](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/MergingQueues.java)

To merge two queues, we need to use the peek() method. Essentially, the peek method allows you to see the data inside of the Queue.

```
    while(!first.isEmpty() && !second.isEmpty()){
        //uses peek() function to look at values in the Queues
        Integer init = first.peek(); 
        Integer next = second.peek();
        

            //if the first queue has a value smaller than 2nd queue
            if(init < next){
                mergedQueue.add(first.poll());
            }
            //if second queue has a value smaller than 1st queue
            else{
                mergedQueue.add(second.poll());
            }
        }
 ```       
Essentially, how the merge works is that we "peek" at the values in the queues and assign them to variables init (for 1st queue) and next (for 2nd queue.)
If the value of init is less than next (or the value from the 1st queue is less than the 2nd), then we add the data from the first queue first. This is to create the chronological order for the integers.
If the value of next is greater than init, then we add the data from the 2nd queue first. 

Of course, there are other statements as checks to ensure that if the first queue is empty and the 2nd is not or vice versa, but this is basically how the merge works.

#### Links to Github for Code: [Challenge 3: Reversing the Queue](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/reverseQueues.java)
In order to reverse a queue, the easiest way is to create a Stack, push the elements of the queue into the stack, and then pop elements from the stack back into the queue
(I don't know how to do this without creating an additional stack)

1. When we move elements from the queue to the stack, it is FIFO 
2. Now, from the stack, when we use the pop() method, it becomes LIFO (elements are popped from the top of the stack) and effecitvely reverses the order of the queue 
3. Then, we just print the queue.


code snippet:
```java
        Stack<Integer> temp = new Stack<>(); //creates a temporary stack

        //pushes element from queue to stack
        while(!initQueue.isEmpty()){
            temp.push(initQueue.poll());
        }

        //pop elements from stack to Queue
        while(!temp.isEmpty())
        {
            initQueue.add(temp.pop());
        }

        //print values from queue
        for(Integer value2: initQueue) {
            System.out.print(value2 + " -> ");
        }
```
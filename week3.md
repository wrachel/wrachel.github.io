---
layout: page
title: Week 3 Challenges
subtitle: Notes & Code for week 3
---
# Week 3 Challenges

## Building Bubble Sort
[Link to code with algorithm](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/BubbleSort.java)
Essentially, how Bubble Sort works is that it compares two items, and swaps them. It repeats this until all 
items are in the correct position.

Code snippet:
```java
    public void sort(ArrayList<Integer> arr){
        int n = arr.size();

        for(int i = 0; i < n -1; i++){ //iterate through the array; needs to compare first two elements, then next two elements, etc.
            for(int j = 0; j < n - i - 1; j++){ //iterates to actually get & swap the two values

                //if value on left is greater than value on right
                if (arr.get(j) > arr.get(j+1)){
                    //swap value on left with value on right
                    Integer temp = arr.get(j);
                    arr.set(j, arr.get(j+1));
                    arr.set(j+1, temp);
                    swaps++;
                }
                comparisons++;
            }
        }
        FinalArr = arr;
    }
```
Essentially, we first use a for loop to iterate through the arraylist. 
Then, if the current value is greater than the next value, we swap them. 
We need to do this multiple times in order to sort the loop, which is why it is a nested loop.

#### Big O Complexity
The worst time complexity of the Bubble Sort algorithm is (n^2).
This is because, at worst, we have to make n swaps n number of times, which is apparent through the nested loops.

## Building Selection Sort
[Link to Code with Algorithm](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/SelectionSort.java)
Selection sort essentially finds the lowest value in the array, and moves it to the front. 
It then has a "sorted" part and an "unsorted" part, and it continues to find
the lowest value in the "unsorted" part until the data is fully sorted.

Code snippet:
```java
 public void sort(ArrayList<Integer> arr)
    {
        Integer n = arr.size();

        // move boundary of unsorted subarray (thus creating sorted & unsorted subarrays)
        for (int i = 0; i < n-1; i++)
        {
            // Find the minimum element in unsorted array
            int min_idx = i;
            for (int j = i+1; j < n; j++) {
                if (arr.get(min_idx) > arr.get(j)) {
                    min_idx = j;
                }
                comparisons++;
            }
            if(min_idx != i) {
                // Swap the found minimum element with the first element
                int temp = arr.get(i);
                arr.set(i, arr.get(min_idx));
                arr.set(min_idx, temp);
                swaps++;
            }
        }
    }
```
In order to implement thes election sort, we iterate through the array.
Each iteration, we find the smallest value, and swap it with the leftmost space in the unsorted array 
We do this until all values are sorted

#### Big O Complexity
The Big O Complexity is also O(n^2) com, as it uses nested for loops.   

## Building Insertion Sort
[link to code](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/InsertionSort.java)
How Insertion sort works is that it iterates through the data, and compares the 
current element to all the previous elements, and moves it to the right position.

Code snippet: 
```java
    public void sort(ArrayList<Integer> arr)
    {
        int n = arr.size();
        for (int i = 1; i < n; ++i) { //iterate from arr[1] to arr[n]
            Integer key = arr.get(i); //assigns current element to a "key"
            int j = i - 1;

            // Move elements of arr[0..i-1] greater than key to one position ahead of current position
            while (j >= 0 && arr.get(j) > key) {
                //if arr[i - 1] is greater than arr[i] then set i to i-1 and i-1 to i (essentially flip them)
                arr.set(j + 1, arr.get(j));
                j = j - 1;
                swaps++;
                comparisons++;
            }
            arr.set(j + 1, key); //sets arr at i-1 to i
            comparisons++;
        }

        FinalArr = arr;
    }
```
In the code implementation, we iterate through the data and assign the current element to a variable.
Then, all the previous elements greater than the variable moves up a position, and we set the current element to the correct position.

#### Big O Complexity
Runs O(n^2) in worst and average cases. Again, this sort uses nested loops.

## Building Merge Sort 
[link to code](https://github.com/wrachel/Data-Structures-Indiv/blob/test-branch/MergeSort.java)
Merge sort works by dividing the data set into two halves, sorting the halves, and then merging the halves. In order to do this, we need a "sort" function and a "merge" function

SORT FUNCTION:
```java
    public void sort(ArrayList<Integer> arr, int start, int end){

        if(start < end){
            comparisons++;
            //sets what the middle of the array would bd
           int middle = (end - 1)/2 + 1;

           //essentially what happens next is recursive function on the sorts that occurs until the array is 1

           //sort first half
           sort(arr, start, middle);
           //sort second half
           sort(arr, middle + 1, end);

           //merge two sorted halves
            MergeSort(arr, start, middle, end);
        }
    }
```
recursively calls sort until the size of the array is one

Then the merge function (MergeSort) recompiles all the data in the correct order:
```java
    public void MergeSort(ArrayList<Integer> arr, int init, int middle, int end){
         int size1 = middle - init + 1;
         int size2 = end - middle;

         //creates two arrays that the initial array will split into
         ArrayList<Integer> leftArray = new ArrayList<>(size1);
        ArrayList<Integer> rightArray = new ArrayList<>(size2);

        //essentially adds all the values on the left into the leftArray
        for(int i = 0; i < size1; i++){
            leftArray.add(arr.get(init + i));
        }
        //adds all the values on the right into the rightArray
        for(int j = 0; j < size2; j++){
            rightArray.add(arr.get(middle + 1 + j));
        }

        int leftIndex = 0; //creates counter for leftArray
        int rightIndex = 0; //creates counter for rightArray

        int mergedIndex = 0;

         if(leftIndex < size1 && rightIndex < size2){ //iterates through array
            if(leftArray.get(leftIndex) <= rightArray.get(rightIndex)){ //essentially, if left value is less then right value
                //if the leftIndex is less than rightIndex (essentially, it is in the proper order), then assign the value
                //at the left index to the arr
                arr.set(mergedIndex, leftArray.get(leftIndex));
                leftIndex++;
                comparisons++;
            }
            else{
                //if value on right is bigger than the one on the left, set the arr to the value on the right
                arr.set(mergedIndex, rightArray.get(rightIndex));
                rightIndex++;
                comparisons++;
            }
            mergedIndex++;//essentially repeats this while loop until all values are acocunted for
        }
         else if(leftIndex < size1){ //if there are still values left in the left array but not the right array
             arr.set(mergedIndex, leftArray.get(leftIndex));
             leftIndex++;
             mergedIndex++;
             comparisons++;
         }
         else if(rightIndex < size2){// if there are still values left in right arraylist but not left one
             arr.set(mergedIndex, rightArray.get(rightIndex));
             rightIndex++;
             mergedIndex++;
             comparisons++;
         }
    }
```
#### Big O Complexity
O(n*logn) --> this is because of the "divide & conquer" method that the merge sort uses. 
Because we break the data into single elements and thus "base problems" that sort the given array.

## Analysis
The fastest sorts are in this order:
1. Merge sort (fastest by far)
2. Insertion Sort
3. Selection Sort
4. Bubble Sort

The image below displays the **running analytics** from IntelliJ console. For some reason, it doesn't run properly on Replit which I suspect has something to do with Replit IDE. 

In order to accomodate for the comparisons & swaps for each sort, I essentially added a variable "comparisons" and "sorts" that acted as a counter in each sort.
After each comparison or each sort, I increased the counter by 1. Then, there is a getter that returns these variables. 

Notably, the faster the sort is the less comparisons and swaps. 

![image](https://user-images.githubusercontent.com/40574565/161466775-97c9a811-0bf0-4705-9bc8-4d4dedfa5c16.png)

## Quick Sort using Python

> 
 [<- Go Back to Index ](https://carboncoffee.hashnode.dev/datastructures) 


## What do we understand by Sorting in general?

Sorting refers to the arrangement of the data values in a particular order according to our needs. To perform sorting in any coding language we make use of the sorting algorithms. **A sorting algorithm** is just a series of orders or instructions. In this, an array is an input, on which the sorting algorithm performs operations to give out a sorted array.


# What is Quick Sort?
- Quick Sort is a **Divide and Conquer algorithm** in this we first pick an element as pivot and partitions the given array around the picked pivot. Let's understand this with an example, assume we have the below set of integers -

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612771745147/dJYlND1FJ.png)
- Here the first element is 11 and we chose this as a PIVOT.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612771889785/E9TQBcYqt.png)

- Now we will try to put Pivot in its right position. In this all the elements left-hand side of 11 are smaller than 11 also all the elements on the right-hand side of 11 should be greater than 11.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612771967434/2tzt4i2WJ.png)
- Now we can mark this 11 sorted and focus on one side. Here in this case we will first ignore the right side and take a look on the left-hand side. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772139080/NK55Iyod2.png)
- Now on the left-hand side we will perform the same task, make the first element which is 7 as the PIVOT and then put in the position where the left side of 7 is smaller than it and the right side of 7 is greater than it.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772278629/XJK7NRqM3.png)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772317170/3DQ1vlUns.png)
- Now we can see that only single elements are left on both sides of 7 hence. This we can put sorted till 11. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772416667/_3ihm5HMB.png)
- Now we need to focus on the right side we were left out and perform the same operations there. We will make the first element which is 29 as the PIVOT.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772521667/Xke4AgdKH.png)

- When we put 29 in its actual position we see that there is no right partition as of now because all the elements left are less than 29

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772592082/s-mJJSePq.png)
- So again we need to repeat the same process recursively.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772645820/cge-JQOpy.png)
- Therefore the elements are sorted using quicksort.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772733890/ZDy_fMk83.png)

## How did we put Pivot in its right position?

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612772949778/gr8pbGOK6.png)

The next question which arises that how to put Pivot in the middle so that all the elements on the left are less than the Pivot and the elements to the right are greater than the Pivot. This process is know as **Partitioning.**

There are two methods to do that ->

- Hoare Partition 
- Lomuto Partition 

### Hoare Partition 
- The way that Hoare Partition works is by making two indexes that start at two ends, the two indexes move toward each other until a smaller value on the left side and greater value on the right side is found. When its found those values are swapped and the process is repeated.

- let's understand this using the below example 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612776908168/PhXPowM4I.png)
- Here we mark 9 as the start and 28 as the end after making 11 the Pivot. We will start from 9 itself and comparing it will the Pivot which is 11, till we find element greater than the pivot.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612777701678/1e1Oz-ozI.png)
- Once you find an element greater than Pivot just stops at that element. Now we need to focus on the endpoint which is 28, we will move until and unless we find an element less than 11 which is the Pivot.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612777883419/d7GqjAnbv.png)
- Now our start = 29 and end = 2, and they have stopped now and then we need to swap their positions. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612777964772/QQBZ_OzBe.png)
- After swapping we need to again repeat this process until either start is greater than the Pivot or end is less than Pivot and then do the swap. This process goes on to start crosses end. Once you stop swap end and Pivot as we did below 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612778250177/e3zAYsLlr.png)

### Let's Implement Quicksort (Hoare Partition) using Python
- First, we will see how we want to give the Input by making the main function 

```
if __name__ == '__main__':
    mylist = [34,54,23,56,10,20,30,21]
    quick_sort(mylist,0,len(mylist)-1)
    print(mylist)
``` 
- Now we will create a function for doing the quick sort. We can see in the above code how we recursively called quicksort function. we create one more function to do the partitioning.

```
def quick_sort(mylist,start_index,end_index):
    if start_index < end_index:
        partition_index = partition(mylist,start_index,end_index)
        quick_sort(mylist,start_index,partition_index-1)
        quick_sort(mylist,partition_index+1,end_index)
``` 
- Now we will make the function for partitioning the list into left and right partition

```
def partition(mylist,start_index,end_index):
    pivot_index = start_index
    pivot = mylist[pivot_index]

    while  start_index < end_index:
        while start_index < len(mylist) and mylist[start_index] <= pivot:
            start_index += 1

        while mylist[end_index]>pivot:
            end_index -= 1 
            
        if start_index < end_index:
            swap(start_index,end_index,mylist)
    swap(pivot_index,end_index,mylist)
    return end_index
``` 
- We are only left with a Swap function

```
def swap(a,b,arr):
    if a != b:
        temp = arr[a]
        arr[a]=arr[b]
        arr[b]=temp
``` 

- Let's Sum up all the codes under one complete program.

```
def swap(a,b,arr):
    if a != b:
        temp = arr[a]
        arr[a]=arr[b]
        arr[b]=temp
def partition(mylist,start_index,end_index):
    pivot_index = start_index
    pivot = mylist[pivot_index]

    while  start_index < end_index:
        while start_index < len(mylist) and mylist[start_index] <= pivot:
            start_index += 1

        while mylist[end_index]>pivot:
            end_index -= 1 
            
        if start_index < end_index:
            swap(start_index,end_index,mylist)
    swap(pivot_index,end_index,mylist)
    return end_index
def quick_sort(mylist,start_index,end_index):
    if start_index < end_index:
        partition_index = partition(mylist,start_index,end_index)
        quick_sort(mylist,start_index,partition_index-1)
        quick_sort(mylist,partition_index+1,end_index)
    

if __name__ == '__main__':
    mylist = [34,54,23,56,10,20,30,21]
    quick_sort(mylist,0,len(mylist)-1)
    print(mylist)
    
``` 
- Finally, we are completed with Quicksort using one method for partitioning. There is one more method to perform the partitioning.

### Lomuto Partition 
- In this case, we decide that the right end element is the Pivot 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612856688752/UEDJfZ7SU.png)
- The start element which is 11 will be called as P index.
- We keep on moving the P index until we find and element which is greater than Pivot (which is 28)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612857242950/4N62K63Lz.png)
- Then we start a new counter I, and I Index will be the same as the P index.
- The I index will keep on moving until it finds the element less than Pivot (which is 28). 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612857452965/bku4VXLjO.png)
- Now we swap the elements 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612857498565/vCR056WoX.png)
- We again perform the same task, the rule for P index is that you move P until you find the element which is greater than Pivot whereas in case of I Index we move I till we find the element less than Pivot.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612859144592/dn6JtRXOk.png)
.
- Then once we find that element we make a Swap.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612859132249/VlYCCQ1uf.png)
- Once again we perform the same task and swap when we reach the conclusion 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612859201449/cOWBWyNq_.png)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612859252667/eAV-IfghS.png)
- When we finally reach the End we can see that the Pivot which is 28 is now at the right position.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612859284295/qeTPuc0uk.png)

- Now you can try giving it a shot by implementing this way of partitioning using python.

**So, This was the quick overview of Quick Sort using Python. I hope you liked the article. Follow back for more upcoming articles**


> Leave a like if you learned something today.

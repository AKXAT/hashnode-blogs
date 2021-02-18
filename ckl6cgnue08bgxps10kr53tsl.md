## Insertion Sort Using Python

> 
 [<- Go Back to Index ](https://carboncoffee.hashnode.dev/datastructures) 


## How does the Insertion Sort Works 
Let's understand this with the help of an example - 

- You have the below-unsorted list of numbers 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372327531/WEYILrzrC.png)

- one way you can sort this is by creating a different array on the left-hand side which will store the sorted array 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372377520/-L2LEqfTD.png)

- Pick an element from the unsorted array and put in the left array in such a way so that array remains sorted 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372462508/lZD7MXMUT.png)
- we can see in the above image that there were no elements in the left array hence we just inserted 21.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372515314/uXOrJoiGo.png)
- Now we put 38 next to 21 because it is greater than it. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372566203/dmItQ0cpN.png)

- Now the next number is 29, which has to be between 21 and 38. So we need to do a little bit of array shuffling here.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372758480/6uq1rDn1u.png)

- Hence now comes 17, which needs to be compared with the elements on the left array 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613372810600/nrcMvCaZV.png)
- So we can continue this way and on the left-hand side, we will get the sorted Array on the left side. This approach is fine but **it requires using a separate array**

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613373547657/uc_5S00Nv.png)
- **Can you do it without using a separate array** This is what we will see that how to do this without using a separate array

 ## Implementing using Python - 
- First, we will create a function for Insertion sort and will implement the approach. Remember we need to swap the elements without storing them into any other array.


```
def insertion_sort(mylist):
    for i in range(1,len(mylist)):
        pointer = mylist[i]
        j = i - 1
        while j>=0 and pointer < mylist[j]:
            mylist[j+1] = mylist[j]
            j-=1 
        mylist[j+1]=pointer
    return mylist
``` 

- Now we can go ahead and add the main function.

```
if __name__ == '__main__':
    mylist = [90,56,21,54,78,23,67]
    print(insertion_sort(mylist))
``` 
- let's assemble the above codes into a once single program.

```
def insertion_sort(mylist):
    for i in range(1,len(mylist)):
        pointer = mylist[i]
        j = i - 1
        while j>=0 and pointer < mylist[j]:
            mylist[j+1] = mylist[j]
            j-=1 
        mylist[j+1]=pointer
    return mylist
if __name__ == '__main__':
    mylist = [90,56,21,54,78,23,67]
    print(insertion_sort(mylist))


``` 

- Output will come-out as **[21, 23, 54, 56, 67, 78, 90]**

**So, This was the quick overview of Insertion Sort using Python. I hope you liked the article. Follow back for more upcoming articles**


> Leave a like if you learned something today.
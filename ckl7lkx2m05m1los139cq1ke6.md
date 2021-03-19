## Shell Sort using Python

> 
 [<- Go Back to Index ](https://carboncoffee.hashnode.dev/datastructures) 

# What is Shell Sort?
It is an optimization over the  [Insertion Sort](https://carboncoffee.hashnode.dev/insertion-sort-using-python). I would like you to go through my  [article on Insertion Sort](https://carboncoffee.hashnode.dev/insertion-sort-using-python)  before continuing with Shell Sort.  

- Disadvantage of Insertion Sort is that when the small elements are towards the end of the list which needs to be sorted then it takes a lot of comparisons and a lot of swaps to finally sort the given list.

- In case of Shell sort we will try to move the heavy elements to the right-hand side of the list, it is not necessary that they will be sorted just a rough sketch which represents the larger number to the right-hand side and the lower numbers to the left-hand side of the element.

## Let's see this using an example 
- We will start with a GAP of 3. Shell sort uses the concept of a Gap which means it starts with the selection of few elements at a certain Gap or spaces.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613381781077/-8gAtdLla.png)
- We kind of make it a subarray and then sort this selected Gaped array 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613381926181/n1msdMXDM.png)
- Now you move to the different Subarray with the same Gap (GAP = 3).

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613381969686/-lMn81g2Q.png)
- Now we Sort them again. As we can see we are just sorting the elements present at the GAP not the Array as a whole.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613382008274/DezngG7g_.png)
- Now we move to the next set of Arrays. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613382103031/L4EzKep-j.png)
- Now we sort them again.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613382131535/3paynESvv.png)
- We keep on doing this till the end with the GAP = 3 and the final list will look something like 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613382245236/VaWih4qkF.png)
- We can see that the larger elements are at the right side and the smaller elements are in the left side of the Array. Now we need to change the GAP to 2 and perform the same task of comparison and sorting the sub-arrays. We will get the below list after doing this.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613382412869/momcWKKTY.png)
- Yes you guessed it right, the ultimate goal is to make GAP = 1  and perform the same operations of comparisons. We will finally get the sorted list.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1613382653314/eMZYwEl3y_.png)
 
### General algorithm for this is ->
- Start with GAP = n/2 and sort subarrays 
- keep reducing GAP by 1/2 and keep sorting the sub-arrays 
- The last insertion should have Gap = 1. At this point, it is same as insertion sort.

## Let's Implement Shell Sort in Python 

- Keeping the above rules in mind we will start making logics, we will keep the GAP = size of array / 2 and the also after the first iteration we need to again update the GAP.

```
def shell_sort(mylist):
    size = len(mylist)
    gap = size//2
    while gap>0:
        for i in range(gap,size):
            pointer = mylist[i]
            j = i
            while j >= gap and mylist[j-gap]>pointer:
                mylist[j] = mylist[j-gap]
                j -= gap
            mylist[j]=pointer
        gap = gap // 2
``` 
- Now let's add the main function for the same

```
if __name__ == '__main__':
    mylist = [90,56,21,54,78,23,67]
    print(shell_sort(mylist)) 
``` 
- Let's now implement the whole code at once

```
def shell_sort(mylist):
    size = len(mylist)
    gap = size//2
    while gap>0:
        for i in range(gap,size):
            pointer = mylist[i]
            j = i
            while j >= gap and mylist[j-gap]>pointer:
                mylist[j] = mylist[j-gap]
                j -= gap
            mylist[j]=pointer
        gap = gap // 2
    return mylist
if __name__ == '__main__':
    mylist = [90,56,21,54,78,23,67]
    print(shell_sort(mylist)) 
``` 

- When we run it ,we will get the output as -> [21, 23, 54, 56, 67, 78, 90]

## Thank-you! 

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups. 


> 
- [My GitHub Repos](https://github.com/akxat)  
- Connect with me on  [Linkedin](https://www.linkedin.com/in/sharma-akshat/) 
- Start  [your own blogs ](https://hashnode.com/@AkshatSharma/joinme) 

%%[wid-1]
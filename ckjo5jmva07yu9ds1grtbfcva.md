## Introduction to Arrays

> 
 [<- Go Back to Index ](https://carboncoffee.hashnode.dev/datastructures) 


# What are Arrays?

An array is a data structure that contains a group of elements. Typically these elements are all of the same data type, such as an integer or string. 

In Python, List is implemented as a Dynamic Array, In other languages like JAVA and C++ we have static array and dynamic array. 

### Static Array 
In the case of a static array, the size of the array is fixed. So assume that you made a array with 5 as the capacity and you tried to add more than the capacity then it will through exception: **Array Index Out of Order 
**

### Dynamic Array 
In the case of a Dynamic array, for this you need not specify any size here you can keep on adding elements.

**How does Dynamic Array works? **
When you are inserting in a Dynamic Array, first it will allocate random continues memory location and when it gets filled it will again allocate double the size of a memory location.

1. Assume firstly it allocates a 10 block memory location, you keep on adding elements until it gets filled. Now you want to add the 11th element. 
2. now 10*2 = 20 blocks will be allocated making the total capacity = 10 (initial) + 20(After) = 30 Final capacity.
3. Now all the elements will be copied to a new capacity of 30 and then it will insert the 11th element. 
4. Similarly if we want to add the 31st element the new set of blocks will be 30 + 30*2 = 90 Blocks 
 

### How are arrays stored in memory?

Let's take an example. Remember that the Indexing of array starts at 0. 

```
scores = [30,40,50,60]
print(scores[2])
#the value will be 30 because the indexing starts from 0
``` 


We know that our computer only communicates using 0 and 1 . so lets assume we want to store **30** in some memory locations so first **30 will be converted to binary**
**30 = 00011110** in binary  

Now we store integers in 4 bytes which is the capacity of integers in most programming languages hence **30** will be stored like 


```
30 = 00000000 00000000 00000000 00011110 
#because  (1 byte = 8 bits)
``` 

Now the integer **30** will be stored in the memory like - 
 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610097055358/i9R7vtTRi.png)

but for general understanding we will consider **scores = [30,40,50,60] ** in below table - 



![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610099762255/BPVCWKqoU.png)

Now taking the above example let's find what will be the result of **print(scores[2])**

1. The Indexing starts from 0 hence when scores is assigned the value **[30,40,50,60]** it is pointing to the memory address at **0th index which is 0x00500**
2. In order to find scores[2] = the initial address + 2 * size of (Integer)
3.  score[2] =0x00500 + 2 * 4
4. **score[2] =0x00508**

### Adding an element in an array

Assume you want to add 35 at the Index =1 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610099426610/HqzGKLKXM.png)

For this, Every element that occurs after the index 1st will be shifted by 1 index and the resulted Array will look like -


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610099972715/8G9_hclXT.png)
[The Big O Time complexity of this will be O(n).](https://carboncoffee.hashnode.dev/big-o-notation-quick-recap) 

Similarly, we can do deletion in an array and when the element is deleted all the elements shift up by one index.

## Thank-you! 

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups. 


> 
- [My GitHub Repos](https://github.com/akxat)  
- Connect with me on  [Linkedin](https://www.linkedin.com/in/sharma-akshat/) 
- Start  [your own blogs ](https://hashnode.com/@AkshatSharma/joinme) 

%%[wid-1]
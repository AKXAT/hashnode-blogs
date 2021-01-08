## Big O Notation - Quick recap

# What is Big O Notation 

Big O Notation is used to measure the running and space requirements of a particular code as the input size increases or decreases.

Measuring time of a program might depend upon the factor that how fast your computer is so we have to use a mathematical representation of the same. This** mathematical representation is know as the Big O**

# Time Complexity 

> 
Formula - **time = a*n + b **

### Rules for deriving the Big O

Let's take an example using python - 

```
square = []
numbers = [2,3,4,5]
for each_number in numbers :
    square.append(each_number*each_number)
print(square)
``` 
In this program we are running **n** iteration (I have mentioned **4 input** so the for loop did **4 iterations** but it can be a long list of **n integers** hence it will do **n iterations** )

we will use the general representation as - **time = a*n + b **

1.  we can neglect **b **since **a*n** is fastest growing term and adding of ** b** wont affect it on a large scale.
2. we will not consider the constants , which is **a** .
3. hence time = **O(n)**

### Let's see some quick examples


- **O(1) **- In the below code what ever you give the input as (small or large) the time will remain constant .

```
def division(n,m):
    div = n/m
    print(div)
``` 


- **O(n²)** - In the below program the outer loop executes N times. Every time the outer loop executes, the inner loop executes M times. Therefore , the statements in the inner loop execute a total of **N * M times. Thus,  the complexity is O(N * M)** but **We always consider the worst case scenario** which means that the inner loop will go on till N iterations hence the total complexity for the two loops is **O(N2).**


```
n=5
for x in range (n):
    for y in range(x+1):
        print("*",end='')
    print("\n")
``` 


- **O(n²)** - So in the code below - we can see there are 3 loops . we have already seen that the first two loops have a complexity of n² and the single outer loop will have a complexity of n. 
taking the equation - **time = a*n² + b*n + c** after applying the rules we will get the **Big O as O(n² + n )** but still the actual answer will be **O(n²).**


- **Reason** for this is - we always consider the worst case scenario , assuming the value of **n is 10000** , now in that case **n²** is be very very large that **n itself** . So discarding n won't impact the Big O. 

```
#code to create a flag 
n=5
for x in range (n):
    for y in range(x+1):
        print("*",end='')
    print("\n")
for x in range(n):
    print('*')

``` 


-  ** Binary Search O(log n)**


1. Consider a list of sorted n number - **my_list = [1,2,3,4,5,6,7,8]**
2. Now in-order to search **index of 6** in the **my_list** we have many ways and the first way you might think of is using a for loop and going through each number one by one and **comparing to 6**. 
The time complexity will be **O(n)** , but what if we have billion numbers in the list , we can't do billion iterations.
3. Second method is **Binary search **, you divide **my_list** from the middle element . We select the middle element and compare with the required element. **So 4 < 6** , Hence we will **discard the left **including the middle element.
4. **[1,2,3,4] discarded ** and the left is **[5,6,7,8]   = n/2 iterations** 
5. we apply the same and the iterations will ne (n/2)/2 until we reach the element which is **n/2*2 .... and n /2^k **
6. so basically in each iterations we are dividing it by half.
7. so for **k Iterations = n/2^k **
8. keeping  k iterations as 1 we have 1 = n/2^k
          
```
n = 2^k
log₂ n    =  log₂ 2^k
log₂ n = k *  log₂ 2
log₂ n = k * 1 ( because log₂ 2 value is 1)

``` 

Hence k (which is the number of iterations) = **O(log n)**


# Conclusion 
Time and space complexity depends on lots of things like hardware, operating system, processors, etc. However, we don't consider any of these factors while analyzing the algorithm.


 [OG Image credits](https://unsplash.com/@hellokellybrito) 







## #1 - Introduction to NumPy

# What is NumPy?
- NumPy is an algebra library for Python. All of the main libraries in PyData are dependent on the NumPy library. You can think of NumPy as the main building block. NumPy is extremely fast as it has bound with the C library.

- NumPy includes two major things -> Vectors and Matrices

- We can install NumPy using the Anaconda distribution to make sure that all the Linear Algebra Libraries are in sync, for this if you have Anaconda as your Python distribution then you can use the below command to install NumPy

> conda install   numpy 

- If you do not have the Anaconda distribution we can use the following command. 

> pip install numpy


## NumPy Array and Functions
- This is the main way we will be using the NumPy library most of the time. Let's create a 1D array and pass it under the NumPy.

```
import numpy as np 
my_arr = [1,2,3]
arr = (np.array(my_arr))
print(arr)
``` 
- Now will see how to make a 2D array and pass it under the NumPy.

```
import numpy as np 
my_maths = [[1,2,3],[4,5,6],[7,8,9]]
arr_2d = np.array(my_maths)
print(arr_2d)
``` 
- The output will be like ->

```
[[1 2 3]
 [4 5 6]
 [7 8 9]]
``` 
- If you want to find out what type of array is there, we can use the command *my_arr.dtype()* and this should return the datatype.
- We have **np.arange()** just like range() we have inbuit in python.

```
my_arr = np.arange(0,10)
print(my_arr)
my_arr = np.arange(0,10,2) # stepsize 
print(my_arr)
``` 
- If we want arrays with only zeros we can use the following code where 2 is the number of rows and 3 is the number of columns.

```
print(np.zeros((2,3)))
#Output is 
#[[0. 0. 0.]
 #[0. 0. 0.]]
``` 
- Similarly, if we want arrays with only 1s then we could use the below code.

```
print(np.ones((2,3)))

#output is 
#[[1. 1. 1.]
 #[1. 1. 1.]]
``` 
- There is one more function that is very useful. What if we want to find 10 evenly spaced list of numbers between 0 to 5 then we can use **linspace().**

```
print(np.linspace(0,5,10))
``` 
- The output will be 

```
[0.         0.55555556 1.11111111 1.66666667 2.22222222 2.77777778
 3.33333333 3.88888889 4.44444444 5.        ]
``` 

- Let's now see how to create an Identity Matrix using NumPy. In linear algebra, the identity matrix of size n is the n × n square matrix with ones on the main diagonal and zeros elsewhere. we will make use of the function **eye(row, column).**


```
print(np.eye(3,4))
``` 

- The Output will be a 3 x 4 Identity matrix.

```
[[1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]]
``` 

- NumPy has many ways to create arrays of a random number, for this we make use of the random function and there are a lot of methods using the **random function.**

```
print(np.random.rand(5,5)) # row x column 
``` 
- Output will be 

```
[[0.87483345 0.60611197 0.9678342  0.3993925  0.02271506]
 [0.85309447 0.25019304 0.95934887 0.95432309 0.88792417]
 [0.3908287  0.79850892 0.67151527 0.9452553  0.33640735]
 [0.1877965  0.87941149 0.74109454 0.82023618 0.63707257]
 [0.60260015 0.12833896 0.23137757 0.87692375 0.15997293]]
``` 
- If you want to generate random integers, we can make use of the **randint method** under the random function. While using **randint** we should mention the Low, High the total distribution of integers we want. If you don't mention the distribution then you will only get an integer by default between the low and the high.

```
print(np.random.randint(1,5,10))
# Output will be [3 2 2 3 4 4 1 1 3 2]
``` 
- We have a **reshape function** which will reshape any given matrix to a row x column matrix ( it might give an error if all the number in the main array are not complete to fill the derived array, if you want to make a 3 X 3 matrix using just 5 elements then it will throw an error). 
- We can also use the **arr.shape** function to find the shape of the current array.


```
arr = np.random.randint(1,90,16)
arr = arr.reshape(4,4)
print(arr)
``` 
- Output will be

```
[[ 6 70 17  5]
 [29 16 15 44]
 [31 84 69 42]
 [35 75 75 81]]
``` 

- We can find the maximum and the minimum using the **arr.max() and arr.min()** functions. Also if you want to find the Index location of the maximum and the minimum then we can you the function **arr.argmax() and arr.argmin().**


```
arr = np.random.randint(1,90,16)
print(arr)
print(arr.min())
print(arr.max())
print(arr.argmax())
print(arr.argmin())
``` 

- So here are the most commonly used functions and methods that will help you get started with the Numpy

## Thank-you! 

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups. 


> 
- [My GitHub Repos](https://github.com/akxat)  
- Connect with me on  [Linkedin](https://www.linkedin.com/in/sharma-akshat/) 
- Start  [your own blogs ](https://hashnode.com/@AkshatSharma/joinme) 

%%[wid-1]
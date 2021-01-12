## Hash Table in Python

## What is Hash Table ?
A hash table is a data structure that implements an associative array abstract data type, a structure that can map keys to values. In other words we can say that , Hash Table is a data structure that stores the values using a **KEY:VALUE pairs.**

In Python we make use of** Dictionaries** to store data values in **KEY:VALUE pairs. ** . So Dictionaries is the Python specific implementation for the Hash Table or Hash Map . Though we can implement same thing using 2D Arrays .

In the example given below , we are storing the price of the fruits and then printing the desired fruit price.

```
mydict = {'Apple' : 25 , 'Oranges' : 40 , 'Banana' :12 }
print(mydict['Apple'])
``` 

## Memory Representation in Hash Table 

- When you create a **Dictionary** the first thing it dose is it creates a array of a random size (here it creates **Array of size 10**)  to store the **Value**

- Then it takes the first **Key** ,  this **Key** will be matched to specific **Value** in the list, and to get the **index **of the **Value** we make use of **Hash Function**

See the below example , how **march **6 is mapped with **310** in the List using the hash function.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610437378258/HFrA_imDh.png)


## What is Hash Function ?

 A hash function is a function that takes a set of inputs of any arbitrary size and fits them into a table or other data structure that contains fixed-size elements.

There are various ways to implement this **hash function ** . Today we will see one way which is using ASCII Numbers.

### Lets take the above example and see how **march 6** was mapped with **310**

- The ASCII representation of **ASCII of march 6** including space will be :

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610438599348/uhFfmvbAG.png)

- Since initially we assigned the Array = 10 . we can perform a MOD operation :
**MOD ( 609/10 ) --> 9 **

- So this is you generated 9 using Hash Function .

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610438879443/Hghi-OUp4T.png)

- And then the value **310** is placed at the Index 9


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610438961507/3ln4w5UEB.png)


## Let's Implement Hash Table in Python

- First we create a Hash Function which will give the sum of  ASCII Values


```
def hash_key(key): # funtion for finding the hash key using ASCII 
        h = 0 # this is varialbe for saving the sum
        for char in key:
            h += ord(char) #ord - will convert each character in the key to the ASCII value 
        return h % 100 # assuming that 100 will the size of the list so we are calculating mod using 100
        
``` 

- Defining a Hash Table class and implementing the above function

```
class HashTable:
    def __init__(self):
        self.max = 100 #for initiating 100 sized list 
        self.arr =[None for i in range(self.max)]
    def hash_key(self,key): # funtion for finding the hash key using ASCII 
        h = 0 # this is varialbe for saving the sum
        for char in key:
            h += ord(char) #ord - will convert each character in the key to the ASCII value 
        #print(h%self.max)
        return h % self.max # assuming that 100 will the size of the list so we are calculating mod using 100
        
if __name__ == '__main__':
    t = HashTable() 
    t.hash_key('march 6')
``` 

- Creating a function adding a Key : Value pairs

```
def add(self,key,value):
        h = sef.hash_key(key)
        self.arr[h]= value
``` 

- Creating a function for returning the Value using the input Key


```
def get(self,key):
        h = self.hash_key(key)
        #print(self.arr[h])
        return self.arr[h]
``` 

- Let's Integrate all the functions under the class Hash Table 


```
class HashTable:
    def __init__(self):
        self.max = 100 #for initiating 100 sized list 
        self.arr =[None for i in range(self.max)]
    def hash_key(self,key): # funtion for finding the hash key using ASCII 
        h = 0 # this is varialbe for saving the sum
        for char in key:
            h += ord(char) #ord - will convert each character in the key to the ASCII value 
        #print(h%self.max)
        return h % self.max # assuming that 100 will the size of the list so we are calculating mod using 100
    def add(self,key,value):
        h = self.hash_key(key)
        self.arr[h]= value
    def get(self,key):
        h = self.hash_key(key)
        #print(self.arr[h])
        return self.arr[h]
        
if __name__ == '__main__':
    t = HashTable() 
    t.hash_key('march 6')
    t.add('march 6',310)
    t.get('march 6')

``` 

Though you will not use this **Hash Table in Python** because there is already **Dictionary** . Dictionaries are Python's implementation of a **Hash Table or Hash Map** that is more generally known as an associative array. A dictionary consists of a collection of key-value pairs. Each key-value pair maps the key to its associated value.


## Collision Handling 

### What Happens in Collision 
In the above examples we saw how the **Key** was matched with the **Index ** of the **value** using **Hash Functions **. 

Assume a situation where more than one **Keys** are assigned the **same Index** by the hash function . This is known as **Collision**. 

In the below example both **march 6 and march 17** are assigned the **Index 9**

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610445180671/8UAYnexP_.png)

## How to handle collisions 

## Chaining 

- In order to handle collisions we can make use of a method called **Chaining**

- In **Chaining** Instead of directly storing the **Value** at the **Index** , we can store a **Linked List** of the Key-Value Pairs    


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610445522455/GAISfD8gv.png)

## Implementing Chaining in Python

- Initializing an Empty Array , because each value is storing KEY-VALUE pair 

```
def __init__(self):
        self.max = 100 #for initiating 100 sized list 
        self.arr =[[] for i in range(self.max)]
``` 
- All Other function remains same . Now we need to edit the ADD function because while fetching the **Value** we need to iterate through the Array 

```
def add(self,key,value):
        h = self.hash_key(key)
        found = False
        for idx,element in enumerate(self.arr[h]):
            if element[0]== key and len(element) == 2:
                self.arr[h][idx] = (key,value)
                found = True 
                break
        if not found:
            self.arr[h].append((key,value))

``` 
- Now In-order to get the required value from the key we need to update the GET function as well


```
def get(self,key):
        h = self.hash_key(key)
        for each in self.arr[h]:
            if each[0] == key:
                #print(each[1]) 
                return each[1]
``` 
- Let's Integrate all the functions under the class Hash Table

```
class HashTable:
    def __init__(self):
        self.max = 100 #for initiating 100 sized list 
        self.arr =[ [] for i in range(self.max)]
    def hash_key(self,key): # funtion for finding the hash key using ASCII 
        h = 0 # this is varialbe for saving the sum
        for char in key:
            h += ord(char) #ord - will convert each character in the key to the ASCII value 
        #print(h%self.max)
        return h % self.max # assuming that 100 will the size of the list so we are calculating mod using 100
    def add(self,key,value):
        h = self.hash_key(key)
        found = False
        for idx,element in enumerate(self.arr[h]):
            if element[0]== key and len(element) == 2:
                self.arr[h][idx] = (key,value)
                found = True 
                break
        if not found:
            self.arr[h].append((key,value))
    def get(self,key):
        h = self.hash_key(key)
        for each in self.arr[h]:
            if each[0] == key:
                #print(each[1]) 
                return each[1]
        
if __name__ == '__main__':
    t = HashTable() 
    t.add('march 6',310)
    t.add('march 17',400)
    t.add('march 6',489)
    t.get('march 6')

``` 


## Linear Probing 

- Second Method is **Linear Probing** .  In this case when we see that an Index is already filled then it searches for a new Index and keeps on finding Index until it's empty.

- In the below example you can see how **march 17** is stored at the **Index 1**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610446224424/2ACywj5zD.png)


Now you can try Implementing Linear Probing in Python .

**I hope you liked this article . Feel free to leave suggestions in the comments below.**


> 
Leave a Like , If you learned something today !  
# Python objects (mutable/inmutable) and built-in types (tuples, lists, dictionaries)

## Explain an easy way to understand the difference between objects and variables (example in console is a must).

A Python variable is a symbolic name that is a reference or pointer to an object. Once an object is assigned to a variable, you can refer to the object by that name. But the data itself is still contained within the object.

In object-oriented programming languages like Python, an object is an entity that contains data along with associated metadata and/or functionality. In Python everything is an object, which means every entity has some metadata (called attributes) and associated functionality (called methods). These attributes and methods are accessed via the dot syntax.

Let me show you on console the explanation from above:

```python
#As I mentioned above, everything in Python is an object...
#and has a unique identifier

#For example this number has an identifier
>>> id(1)
4559735536
#But if you see the identifier from another random number, this is different 
>>> id(2)
4559735568
#Even if you combine 1 and 2 their identifiers has not combined, we get new one
>>> id(12)
4559735888
#If you assigned the number 1 to a variable call n, the id number is the...
#same that the number 1 because variable n just is pointing to the object 1
#and now you can refer to 1 using n
>>> id(n)
4559735536
#We can validate if n and 1 belong to an integer object
>>> type(n)
<class 'int'>
#If you create a new variable pointing to the same 1 number, is the id..
#different from n? Let's see
#As you can see the id is the same because both are pointing to the same object
>>> id(n)
4559735536
>>> id(m)
4559735536
#But if you replace the object of n or m, the id must change
#n is not anymore assigned to object 1, now n is pointing to 3
#Effectively the id has changed
>>> n = 3
>>> id(n)
4559735600
>>> id(m)
4559735536
#If you create an equality of n and m, both will have the same id number
>>> n = m
>>> id(n)
4559735536
>>> id(m)
4559735536
```

We concluded that an object has a unique id so are different each others. On the other hand the variable is able to point a specific object and you can refer to that object using the variable name, if multiple variables pointing to the same object so the variables will have the same id. The id number will change just if the object has changed not the variable.

## Provide 1 example of, at least 6 different Built-in types in python.

Data types are the classification or categorization of data items. It represents the kind of value that tells what operations can be performed on a particular data. Since everything is an object in Python programming, data types are actually classes and variables are instance (object) of these classes.

We are going to create six different variable types to provide examples:

```python
#numeric type
>>> h = 10
>>> type(h)
<class 'int'>

#string type
>>> a = "Hi"
>>> type(a)
<class 'str'>

#set type
>>> myset = {"apple", "banana", "cherry"}
>>> type(myset)
<class 'set'>

#list type
>>> p = [1,2,3,4]
>>> type(p)
<class 'list'>

#tuple type
>>> o = (1,2,3,4)
>>> type(o)
<class 'tuple'>

#dictionary type
>>> contacts = {"Juan" : 1234, "Pedro" : 5678}
>>> type(contacts)
<class 'dict'>
```

## Show with an example how can you determine that an object is mutable and when an object it is not (console is a must).

A quick definition is a mutable object can change it is state or contents and immutable objects cannot.

**Mutable objects:**

*list, dict, set, byte array*

**Immutable objects:**

*int, float, complex, string, tuple, frozen set [note: immutable version of set], bytes*

The best example to demonstrate is shown below:

```python
#The list and tuples are very popular in Python because are very similar...
#but has different properties.

#As mentioned above, tuple is immutable and list is mutable. So we are going to...
#try change some item in both and comparate the results

#list type
>>> p = [1,2,3,4]
>>> type(p)
<class 'list'>
#Modifying an item
>>> p[0] = 3
#Here we can see that the item[0] has been replaced by 3
>>> p
[3, 2, 3, 4]

#tuple type
>>> o = (1,2,3,4)
>>> type(o)
<class 'tuple'>
#Modifying an item
>>> o[0] = 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

> **Immutable objects doesn’t allow modification after creation**
> 

## Apply and explain at least 3 different attributes of the 6 different Built-in types mentioned below.

We are going to create six different variable types to provide examples:

```python
#numeric type
>>> h = 10
>>> type(h)
<class 'int'>
#This show you the numerator and denominator from an integer 10/1 
>>> h.numerator
10
>>> h.denominator
1
#Return the real number of the variable
>>> h.real
10

#string type
>>> a = "Hi there"
>>> type(a)
<class 'str'>
#Searches the string for a specified value and returns the position...
#of where it was found
>>> a.find("t")
3
#Returns True if all characters in the string are decimals
>>> a.isdecimal()
False
#Returns True if all characters in the string are ascii characters
>>> a.isascii()
True

#set type
>>> myset = {"apple", "banana", "cherry"}
>>> type(myset)
<class 'set'>
#Adds an element to the set
myset.add("orange")
>>> myset
{'banana', 'orange', 'cherry', 'apple'}
#Removes the specified element
>>> myset.remove("orange")
>>> myset
{'banana', 'cherry', 'apple'}
#

#list type
>>> p = [1,2,3,4]
>>> type(p)
<class 'list'>
#Removes the element at the specified position
>>> p.pop(3)
4
>>> p
[1, 2, 3]
#Adds an element at the end of the list
>>> p.append(4)
>>> p
[1, 2, 3, 4]
#Reverses the order of the list
>>> p.reverse()
>>> p
[4, 3, 2, 1]
#Removes all the elements from the set
>>> myset.clear()
>>> myset
set()

#tuple type
>>> o = (2,2,2,3,4,5)
>>> type(o)
<class 'tuple'>
#Returns the number of times a specified value occurs in a tuple
>>> o.count(2)
3
#Searches the tuple for a specified value and returns...
#the position of where it was found
>>> o.index(5)
5

#dictionary type
>>> contacts = {"Juan" : 1234, "Pedro" : 5678}
>>> type(contacts)
<class 'dict'>
#Returns a list containing the dictionary's keys
>>> contacts.keys()
dict_keys(['Juan', 'Pedro'])
#Returns a list of all the values in the dictionary
>>> contacts.values()
dict_values([1234, 5678])
#Removes the element with the specified key
>>> contacts.pop("Juan")
1234
>>> contacts
{'Pedro': 5678}

```
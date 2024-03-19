# Python Basic Guide

## This document is a basic tutorial to learn Python, we will cover the installation and some concepts to build no complex programs.

## Installation

There are different ways to install Python but in this case we are going to explain the official installer. You can download a Python installer from the official [Python download website](https://www.python.org/downloads/). This method does not give you automatic updates, and I would recommend it only if you don’t have access to the Microsoft store or you don't already have installed on Mac terminal.

1. Go to the official website and click on the download button
2. Then just execute the installation file 
3. Finally just follow the instructions to complete.

![Screen Shot 2021-09-06 at 19.11.19.png](Python%20Basic%20Guide%201fa967f289c2479aa6bcccbb48adcba0/Screen_Shot_2021-09-06_at_19.11.19.png)

![Screen Shot 2021-09-06 at 19.22.55.png](Python%20Basic%20Guide%201fa967f289c2479aa6bcccbb48adcba0/Screen_Shot_2021-09-06_at_19.22.55.png)

![Screen Shot 2021-09-06 at 20.42.50.png](Python%20Basic%20Guide%201fa967f289c2479aa6bcccbb48adcba0/Screen_Shot_2021-09-06_at_20.42.50.png)

## Introduction to Python: Learn the Python basics

If you have Python installed on your system, you are now ready to start learning the basic with this introduction.

We are going to start with basic concepts such as:

- Strings
- Numbers
- Booleans
- Dictionaries
- Variables

> We can find the below data types, here we are going to discuss the basics.
> 

[Data Type](Python%20Basic%20Guide%201fa967f289c2479aa6bcccbb48adcba0/Data%20Type%208396d5d8c7324aadbebfd8a9c7e5583c.csv)

### Python String: Working with text

So, in Python, a piece of text is called a string and you can perform all kinds of operations on a string. But let’s start with the basics first!

**What is Python String?**

A string in Python is a sequence of characters

**How to create a Python String**

A Python string needs quotes around it for it to be recognized as such, like this:

```python
>>>'Hello, World'
Hello, World
```

We can use some math operators on the string. Try it with the following expressions:

```python
>>>'a' + 'b'
ab
>>> 'ab' * 4
abababab
>>> 'a' - 'b'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

This is what happens in the code above:

- The plus operator glues two Python strings together.
- The multiplication operator repeats our Python string the given number of times.
- The minus operator doesn’t work on a Python string and produces an error.

**Single or double quotes?**

We have used single quotes, but Python accepts double-quotes around a string as well:

```python
>>> "a" + "b"
ab
```

Issues using quotes? Please find the below example:

```python
>>> mystring = "It's a string, with a single quote!" #Conflict word
>>> mystring = 'It's a string, with a single quote!'
  File "<stdin>", line 1
    mystring = 'It's a string, with a single quote!'
                   ^
SyntaxError: invalid syntax
```

There’s actually a way around this problem, called escaping. You can escape a special character, like a quote, with a backward slash:

```python
>>> mystring = 'It\'s an escaped quote!'
>>> print(mystring)
It's an escaped quote!
```

**Multiline strings**

Python also has a nice syntax for creating multiline strings, using triple quotes:

```python
>>> my_big_string = """This is line 1,
... this is line 2,
... this is line 3."""
>>> print(my_big_string)
This is line 1,
... this is line 2,
... this is line 3.
```

All mentioned about is enough to handle strings and write easy programs to print basic information or text.

### Python Integer: Explained With Example Code

The Python integer is a non-fractional number, like 1, 2, 45, -1, -2, and -100. It’s one of the three types of numbers Python supports natively, the other being floating point numbers and complex numbers.

**Max size of a Python integer**

Unlike many other programming languages, integers in Python 3 can have large values. In fact, they are unbounded, meaning there is no limit to their size, for example:

```python
>>> num = 98762345098709872345000
>>> num + 1
98762345098709872345001
```

Of course there is a limit, since your computer does not have unlimited memory. However, for all practical purposes you don’t have to worry about it.

**Integer types**

Unlike Python 2 and many other languages, Python 3 has only one type of integer. This is part of Python’s aspiration to be a clean, easy to learn language. It’s one less thing we have to worry about. 

**Converting from and to an integer**

**String to integer**

To convert a [string](https://python.land/introduction-to-python/strings) to integer in Python, use the `int()` function:

```python
>>> int('100')
100
```

**Integer to string**

To convert an integer to string in Python, use the `str()` function:

```python
>>> str(200)
'200'
```

**Float to integer**

To convert a float to an integer, use the `int()` function:

```python
>>> int(2.3)
2
```

**Is it a Python integer?**

To check if a value is an integer, we can use the `type()` function. It will return `int` for integers:

```python
>>> type(2)
int
```

## Python’s Boolean Operators

The ability to use conditions is what makes computers tick; they make your software smart and allow it to change its behavior based on external input. We can use `True` and `False`, but more expressions evaluate to either `True` or `False`. These expressions often include a so-called boolean operator.

```python
>>> 2 > 1
True
>>> 2 < 1
False
>>> 2 < 3 < 4 < 5 < 6
True
>>> 2 < 3 > 2
True
>>> 3 <= 3
True
>>> 3 >= 2
True
>>> 2 == 2
True
>>> 4 != 5
True
>>> 'a' == 'a'
True
>>> 'a' > 'b'
False
```

This is what all the boolean operators are called:

[Untitled](Python%20Basic%20Guide%201fa967f289c2479aa6bcccbb48adcba0/Untitled%20Database%20246bfee428ee4f14ac58dd7221f2b46a.csv)

**Creating a Python Dictionary**

Let’s look at how we can create and use a Python dictionary in the [Python REPL](https://python3.guide/introduction-to-python/the-repl):

```python
>>> phone_numbers = { 'Jack': '070-02222748',
'Pete': '010-2488634' }
>>> my_empty_dict = { }
>>> phone_numbers['Jack']
'070-02222748'
```

The first dictionary associates keys (names like Jack and Pete) with values (their phone numbers). The second dictionary is an empty one.

## What is a Python variable?

Let’s start by defining more formally what a variable is:

**Variable**

A variable is used to store information that can be referenced later on.

So a variable is what we use to name the result of, for example, a calculation we make. Or, in other words, we can assign the result of that calculation to a variable. We can create an unlimited amount of variables; we just have to make sure we give them unique names.

**Creating a Python variable**

We can create a Python variable called `result` in the REPL. But before we do so, we’ll try and see if Python already knows what result is:

```python
>>> result
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'result' is not defined
```

> This is the way Python lets you know about errors. Ignore the first two lines and focus on the actual error instead. Python reports: name 'result' is not defined. Python errors tend to be very helpful if you know where to look. That’s why I wanted to show you one. Eventually, you’ll need to write code on your own, and running into errors is, unfortunately, a big part of the job. Being able to decipher errors will be a useful skill!
> 

Now let’s define the name result as a variable and try this again:

```python
>>> result = 3 * 5
>>> result
15
```

Step by step this is what happens:

1. Python sees a so-called assignment: we assign the result of 3 * 5 to the variable called `result`. Assignments are done with the ‘=’ character, which is conveniently called ‘is’. So we just told Python: result is 3 times 5.
2. Next, we type `result`.
3. Python does not recognize this as a command, so it tries to see if, perhaps, there’s a variable with this name. There is, and we assigned 15 to it. Hence this line evaluates to the number 15, which is printed on the screen.

> I hope you find this guide useful, see you on the next, have a good one!
> 

I would like to mention that I have included different MarkDown useful characteristics such as text as code and code blocks to show basic examples and implement the concepts discussed.
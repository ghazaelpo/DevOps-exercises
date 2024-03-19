# Classes and decorators

In the following points I'm going to mentioned just the requested information and at the bottom of this document I will show all the code and a screenshot of how it works.

# Create two classes that represents an abstract form with at least 3 parameters and methods

```python
class Employee:
class Car:
```

# Initialize some objects from this classes

```python
employee_1 = Employee("Genaro", "Paredes", "DevOps intern")
car_1 = Car("Ford", "Mustang", 1967)
```

# Use one magic method

```python
def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year
```

# Create a function decorator and a class decorator, try to make something useful

```python
def my_decorator(func):
    def wrapper():
         func()
    return wrapper
    
def second_sample_class():
    print("\n----------Second sample class----------")

second_sample_class = my_decorator(second_sample_class)
second_sample_class()
```

### All the code looks like the below:

```python
#!/usr/bin/env python

import time
# Creating Classes 
# First sample Class
class Employee:

    # Using magic method __init__
    def __init__(self, name, last_name, employee_position):
        self.name = name
        self.last_name = last_name
        self.employee_position = employee_position

    # 1 sample method
    def welcome(self):
        b = " "
        print("\n..........welcome method..........")
        print("Welcome to the office:\n" + self.name + b + self.last_name + b + b + time.ctime())

    # 2 sample method
    def seeu2morrow(self):
        print("\n..........seeu2morrow method..........")
        print(f"See you tomorrow {self.name}, have a nice day")

    # 3 sample method
    def employeePosition(self):
        print("\n..........employeePosition method.........")
        print(f"{self.employee_position}")

# Objects
employee_1 = Employee("Genaro", "Paredes", "DevOps intern")
print("\n----------First sample class----------")
employee_1.welcome()
employee_1.employeePosition()
employee_1.seeu2morrow()

#Second sample class
class Car:

    # Using magic method __init__
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year

    # 1 sample method
    def carOn(self):
        print("\n..........carOn method..........")
        print(f"Car {self.brand} using engine")

    # 2 sample method
    def carOff(self):
        print("\n..........carOff method..........")
        print(f"Old motor car, year: {self.year}, it doesn't work")
    
    # 3 sample method
    def carMoving(self):
        print("\n..........carMoving..........")
        print(f"{self.model} car moving forward at 90 km/h")

    # My first decorator function
def my_decorator(func):
    def wrapper():
         func()
    return wrapper
    
def second_sample_class():
    print("\n----------Second sample class----------")

second_sample_class = my_decorator(second_sample_class)
second_sample_class()

car_1 = Car("Ford", "Mustang", 1967)
car_1.carOn()
car_1.carOff()
car_1.carMoving()
```

![Screen Shot 2021-09-21 at 2.23.02.png](Classes%20and%20decorators%200f7d1fa9ac3748bf805fc3fd7b08ccc8/Screen_Shot_2021-09-21_at_2.23.02.png)
# Pseudo-functional Python

# Based on a list of dictionaries create a function with normal loops that iterate over the list of dictionaries and generate a tuple with all the values for keys:"name"

```python
collection = [{"name" : "Juan",   "last_name" : "Rodriguez"},
							{"name" : "Emilio", "last_name" : "Barragan"},
							{"name" : "Jose",   "last_name" : "Lopez"}]

def OverTheList(collection):
	tuple1 = ()
	for i in collection:
		tuple1 += (i.get("name"),)

	return tuple1

# Printing normal function
print("\n_______Normal Function_______")
print(OverTheList(collection))
```

# Transform that normal function loops into a list of comprehension

```python
print("\n______List of comprehension")
o = tuple([c.get("name") for c in collection])
print(o)
```

# Transform that list of comprehension into a generator and consume it

```python
print("\n_______Generator______")
gen = o
for ob in gen:
print(ob)
```

# Based on this object: lista = []

```python
lista = ["elefante", "rana", "jirafa", "perro", "puerco", "tigre"]
```

# Create a function using lambda and filter that creates a list with all the strings that contains at least one "a"

```python
print("\n_______Lambda filter_______")
print(list(filter(lambda x: "a" in x, lista)))
```

# Create a function using map that creates a new list with the same string but adding "kun" at the end

```python
print("\n_______Map function______")
list_kun = list(map(lambda x: x + "kun", lista))
print(list_kun)
```

## All the code looks like the below:

```python
#!/usr/bin/env python

#Pseudo-functional python
# Based on a list of dictionaries create:
collection = [{"name" : "Juan",   "last_name" : "Rodriguez"},
              {"name" : "Emilio", "last_name" : "Barragan"},
              {"name" : "Jose",   "last_name" : "Lopez"}]

# A function with normal loops that iterate over the list
# of dictionaries and generate a tuple with all the values for keys:"name"
def OverTheList(collection):
    tuple1 = ()
    for i in collection:
        tuple1 += (i.get("name"),)

    return tuple1

# Printing normal function
print("\n_______Normal Function_______")    
print(OverTheList(collection))

# Transform that normal function loops into a list of comprehension
print("\n______List of comprehension_______")
o = tuple([c.get("name") for c in collection])
print(o)

# Transfomr that list of comprenhention into a generator and consume it
print("\n_______Generator______")
gen = o
for ob in gen:
    print(ob)

# Based on this object: lista = []
lista = ["elefante", "rana", "jirafa", "perro", "puerco", "tigre"]

# Create a function using lambda and filter that creates a list with
# all the strings that contains at least one "a"
print("\n_______Lambda filter_______")
print(list(filter(lambda x: "a" in x, lista)))

# Create a function using map that creates a new list with the same
# string but adding "kun" at the end
print("\n_______Map function______")
list_kun = list(map(lambda x: x + "kun", lista))
print(list_kun)
```

![Screen Shot 2021-09-21 at 1.51.21.png](Pseudo-functional%20Python%202913ce49bf3a429c9d151ff289a70f3d/Screen_Shot_2021-09-21_at_1.51.21.png)

### Write an explanation of why reduce is not totally recommended in python 3

The main reason is that `reduce()` is not totally clear and readable, maybe sometimes you spend more time figuring out how the expression works but just in cases because is very useful.

Quick, what's the following code doing?

```python
total = reduce(lambda a, b: (0, a[1] + b[1]), items)[1]
```

You can figure it out, but it takes time to disentangle the expression to figure out what's going on. Using a short nested def statements makes things a little bit better:

```python
def combine (a, b):
    return 0, a[1] + b[1]

total = reduce(combine, items)[1]
```

But it would be best of all if I had simply used a for loop:

```
total = 0
for a, b in items:
    total += b

```

Or the sum() built-in and a generator expression:

```
total = sum(b for a,b in items)

```

Many uses of reduce() are clearer when written as for loops.
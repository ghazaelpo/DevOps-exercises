# Handling Exceptions

I have created a class that inherits functionalities from Exception class, it is called DOU_Error. After that I created another class to give a name to the specific error that we want to raise.

We will raise the error using a function called customError, we are going to type a word and the function will validate if this word has not only alphabet characters using an If statements , otherwise the else part will execute and print "All characters are alphabet".

This is the code:

```python
#!/usr/bin/env python

# define Python user-defined exception and inherit from Exception class
class DOU_Error(Exception):
    """Base class for other exceptions"""
    pass

# We defined the specific error class here
class NotAlphabetCharacters(DOU_Error):
    """All characters are not alphabets"""
    pass

# A function to raise the custom error for the demostration
# We used a While to repeat the execution until the user type a entire word alphabet characters
def customError():
    while True:
        try:
            user_input = input("Type a word with all alphabetic characters: ")
            if user_input.isalpha() == False:
                raise NotAlphabetCharacters
            else:
                print("All characters are alphabets")
            break
        except NotAlphabetCharacters:
            print("Characters are not alphabets")

customError()
```

![giphy.gif](Handling%20Exceptions%20edef18838e234e2a835e9593c33c52e5/giphy.gif)

### Give an explanation to the class about when you should try to handle an exception and when not (Examples required)

It is a good idea handle exceptions when you are already awareness about the kind of error that your code is generating but just when you don't have control about the incoming data, for example:

```python
# We have this function
# The data of this parameter is from outside of your code, so maybe...
# this data could generate an error and you can handle the error using...
# try and except
def example(data_file):
    return data_file
```

> Within your script you can check variables for type, lists for length, etc. and you can be sure that the result will be sufficient since you are the only one handling these objects. As soon however as you handle files in the file system or you connect to remote hosts etc. you can neither influence or check all parameters anymore nor can you be sure that the result of the check stays valid.
>
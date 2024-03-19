# Unittesting

The following code is my script to test my previous exercises:

- Fibonacci
    - For this code I created three different functions, test_fib_0, test_fib_1 y test_fib_2. 0 and 1 are the same case but with different results. We know that for the two first elements from Fibonacci Sequence are always 0 and 1. So this is a great parameter to evaluate our code, so the statement is the below:
        - Positive statement "If n = 1 the fibonacci number should be 0", for this case we will compare the result to 0, and effectively is positive.
        - Negative statement "If n = 1 the fibonacci number should be 1", for this case we will compare the result to 1, and effectively is negative.
- Webhook
    - For this code I created test_Webhook_1 function just to validate if our function is executed and return the same message that we introduced it. This case will positive.
- Generator
    - In this example I created test_Generator_1 function just to validate if the reverse function from generator script is working and applied to the input string.

```python
from Fibonacci import *
from Webhook import *
from Generator import *

import unittest

class TestFib(unittest.TestCase):
    # 1
    # Positive
		# Evaluate fibonacci sequence if n = 1
    def test_fib_0(self):
        print("\nif n = 1 the fibonacci number should be 0")
        self.assertEqual(fib(1), 0)

    # 1
    # Negative
		# Evaluate fibonacci sequence if n = 1
    def test_fib_1(self):
        print("\nif n = 1 the fibonnaci number should be 0")
        self.assertEqual(fib(1), 1)

    # 2
    # Positive
		# Evaluate fibonacci sequence if n = 45
    def test_fib_2(self):
        print("\nTest n = 18")
        self.assertEqual(fib(45), 701408733)
    # 3
    # Negative 
		# Evaluate fibonacci sequence if n = 0, as per our code...
		# this evaluation will return None and just print...
		# "Type an integer number"
    def test_fib_3(self):
        print("\nTest for check if n = 0 return None")
        self.assertIsNotNone(fib(0))

    # 4
    # Positive
		# Evaluate if the function return the same messagge that we introduced
    def test_Webhook_1(self):
        print("\nCheck if the function return the message that you sent")
        print(text)
        self.assertEqual(Webhook(text),text)

    # 5
    # Positive
		# Evaluate if the reverse function works
    def test_Generator_1(self):
        print("\nCheck if the rev_str function is executed")
        self.assertTrue(rev_str(my_str), True)

if __name__ == '__main__':
    unittest.main()
```

Example of how it works:

![Screen Shot 2021-09-24 at 16.59.32.png](Unittesting%206c3bbc910c574d84a804c05ef471ae0e/Screen_Shot_2021-09-24_at_16.59.32.png)
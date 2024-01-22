# Python
## introduction
* Don't need to explicitly compile and run your code like C.
* Use interpreter, a program to read and run your code.
* Less code, more work.
* A good ecosystem with lots of libraries to solve problems which have been solved by others.
```
code hello.py
python hello.py         # python means the interpreter program here 
```

```py title="hello.py"
print("hello, world")
```
## Types
`bool`, `int`, `float` and `str` are types in python.
Use `input` to get ***str*** from your keyboard
```py title="calculator.py"
x = input("x: ")
y = input("y: ")

print(x + y)        # str can be connected with a single '+'
```
> you can even use '*' to str like `print("?" * 4)`

Run the code and we get following result. The variable type that `input` returns is `str` explains the reason why output is 12, i.e. '1' + '2'
```
python .\calculator.py
x: 1
y: 2
12
```
The correct version is shown below
```py title="new_calculator.py"
x = int(input("x: "))
y = int(input("y: "))

print(x + y)
```
A traceback will appear if the input isn't number.

## Conditions
* Indentation is important in python

```py
if x < y:
    print("x is less than y")
elif x > y:
    print("x is greater than y")
else:
    print("x is equal to y")
```
## Object-Oriented Programming
Some functions are built into objectives themselves. These functions called `method` comes with some data types, like a string.
```py title="agree.py"
s = input("Do you agree? ")
# method for string to convert it to lowercase
s = s.lower()               

if s in ["y", "yes"]:
    print("Agreed")
elif s in ["n", "no"]:
    print("Not agreed")
```

Click <a herf="docs.python.org">here</a> for official documentation

## Loop
=== "while loop"
    ```py
    i = 0
    while i < 3:
        print("meow")
        i += 1
    ```

=== "for loop"
    ```py
    # on every iteration of this loop, 
    # Python is assigning `i` to the next value in the list behind `in`
    for i in range(3):          # range(3) returns a list of integers from 0 to 2
        print("hello, world")
    ```

A forever loop
```py
while True:
    print("meow")
```
> True and False are capitalized in Python

You can loop over almost anything that is iterable in Python, such as string.
```py title="uppercase.py"
before = input("Before: ")
print("After: ", end="")
for c in before:
    print(c.upper(), end="")    
    # end is a second parameter here telling print to insert nothing instead of a new line after every output
    # otherwise each letter will be outputed in seperate lines
print()     # move cursor to next line
```
Actually if you want to convert a string to uppercase, you just need to call the method
```py
before = input("Before: ")
after = before.upper()
print(f"After: {after}")
```
When you want to implement a `do-while` loop, just put the loop body into a forever loop and jump out when something happens.
In Python, even a for loop can have a `else` clause.
```py
names = ["Cat", "Dog", "Bird"]

name = input("Name: ")

for n in names:
    if name == n:
        print("Found")
        break
else:
    print("Not Found")
```
If the for loop terminates without calling `break`, then the code in `else` will execute.
This is just an example to explain `for-else`. Actually it can be solved below
```py
names = ["Cat", "Dog", "Bird"]

name = input("Name: ")

if name in names:
    print("Found")
else:
    print("Not Found")
```
## Function
Practically, we want the main part of a program at the top of the file so that we can dive right in and know what the file is doing. Let's look at the following way.
```py
for i in range(3):
    meow()

def meow():
    print("meow")
```
If we run the code, we will find a traceback.
```
Traceback (most recent call last):
  File "C:\Users\86156\desktop\meow.py", line 2, in <module>
    meow()
    ^^^^
NameError: name 'meow' is not defined
```
This could happen because the interpreter read the file from top to down and `meow()` is called before its defination.
To solve this problem, we need to define a function called `main` and takes no arguments.
```py
def main():
    for i in range(3):
        meow()

def meow():
    print("meow")

main()
```
Note that the last line is necessary since the beginning only define the `main` function and it will be executed only when we call it.
Now, let's add some parameter so that we can control the times the loop will run.
```py
def main():
    meow(5)

def meow(n):
    for i in range(n):
        print("meow")

main()
```
## truncation, imprecision and overflow
Python won't truncate the result if it has fractional component. It will convert type automatically.
```py title="calculator.py"
x = int(input("x: "))
y = int(input("y: "))
z = x / y
print(z)
```
Run the code
```
python .\calculator.py
x: 1
y: 3
0.3333333333333333
```
We can use f string to show more digits after the decimal point
```py
x = int(input("x: "))
y = int(input("y: "))
z = x / y
print(f"{z:.50f}")
```
The result below shows that the floating point imprecision problem remains in Python
```
python .\calculator.py
x: 1
y: 3
0.33333333333333331482961625624739099293947219848633
```
In Python, integer won't overflow no matter how big it is because Python will reserve more and more memeory for that integer to fit it.
## Exceptions
In C, we often return some distinct value to signifies the function failed to achieve its goal. In Python, we can use `exception` to handle it.
```py
def main():
    x = get_int("x: ")
    y = get_int("y: ")

    print(x + y)

def get_int(prompt):
    return int(input(prompt))

main()
```
In the above program, the `get_int()` function works well when we input some numbers. But a exception happens when we input other things.
```
python .\calculator.py
x: cat
Traceback (most recent call last):
  File "C:\Users\86156\desktop\calculator.py", line 10, in <module>
    main()
  File "C:\Users\86156\desktop\calculator.py", line 2, in main
    x = get_int("x: ")
        ^^^^^^^^^^^^^^
  File "C:\Users\86156\desktop\calculator.py", line 8, in get_int
    return int(input(prompt))
           ^^^^^^^^^^^^^^^^^^
ValueError: invalid literal for int() with base 10: 'cat'
```
The `ValueError` tells us what kind of exception we have. We can revise it in this way:
```py title="get_int()"
def get_int(prompt):
    try:
        return int(input(prompt))
    except ValueError:
        print("Not an interger")
```
In this program, we use `try` and `except` to tell the interpreter we try to do something and if `ValueError` exception happens, we will see "Not an integer" instead of traceback.
Only `try` and `except` are not enough. We need to add a loop so that the function will loop again and again until get a valid input.
```py title="get_int()"
def get_int(prompt):
    while True:
        try:
            return int(input(prompt))
        except ValueError:
            print("Not an interger")
```
## list
List is something like array but their memory is automatically handled for you.
An array is about having contiguously in memory. In Python, a list is more like a linked list. It will allocate memory for you and you don't have to know about pointers and nodes. 
```py 
scores = [72, 73, 33]           # List using square brackets
# use the bulid-in functions to get the sum and length of the list
average = sum(scores) / len(scores)
```
`append()` method helps to add sth. into a list. Or you can use `+`
```py
scores = []
for i in range(3):
    score = get_int("Score: ")
    scores = scores + [score]           # Or 'scores.append(score)'

Average = sum(scores) / len(scores)
```
## dist
Dictionary is essentially a hash tabel, a collection of key-value pairs.
```py
people = [
    {"name": "Carter", "number": "12345"},     # dist uses curly brace
    {"name": "David", "number": "12335"},
    {"name": "John", "number": "16345"},
]

name = input("Name: ")

for person in people:
    if person["name"] == name:
        number = person["number"]
        print(f"Found {number}")
        break
else:
    print("Not Found")
```
A big dist can be used, which is tidier in this case:
```py
people = {
    "Carter": "12345",
    "David": "12335",
    "John": "16345",
}

name = input("Name: ")

if name in people:              # Python will look for the name among the keys in the dist
    number = people[name]
    print(f"Found {number}")
else:
    print("Not Found")
``` 
## Other
### sys
The sys library has system-related functionality. 
In C, we got access to command-line arguments with `main()`, `argc` and `argv`.
You can do command-line arguments in Python with the help of `sys`
```py
from sys import argv

if len(argv) == 2:
    print(f"hello, {argv[1]}")
else:
    print("hello, world")
```
If you give one argument, the output is `hello, world`. If two, then different. 
Note that the command `python` is ignored from `argv`
```
$ python greet.py
hello, world
$ python greet.py David
hello, David
```
You can also exit the program with `sys`
```py
import sys

if len(sys.argv) != 2:
    print("Missing command-line argument")
    sys.exit(1)

print(f"hello, {sys.argv[1]}")
sys.exit(0)
```
### pip
Using `pip` to install third-party libraries.
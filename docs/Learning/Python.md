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
    # on every iteration of this loop, Python is assigning `i` to the next value in the list behind `in`
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

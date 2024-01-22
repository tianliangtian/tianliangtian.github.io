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
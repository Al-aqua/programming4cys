# Chapter 2: Python Fundamentals

## Objectives:

- Understand the basics of control structures, functions, and error handling.
- Work with Python data structures to store and manipulate data effectively.

### 2.1 Control Structures

#### Lecture Content:

1. **If-Else Statements**
   ```python
   age = int(input("Enter your age: "))
   if age >= 18:
       print("You are an adult.")
   else:
       print("You are a minor.")
   ```
1. **For Loops**
   ```python
   for i in range(5):
       print(f"Number {i}")
   ```
1. **While Loops**
   ```python
   password = "password123"
   user_input = ""
   while user_input != password:
       user_input = input("Enter the password: ")
       if user_input == password:
           print("Access granted.")
   ```

#### Exercises:

1. Write a script to determine if a number is even or odd.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

2. Create a program that repeatedly asks the user for input until they type "exit".

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

3. Write a script that prints all prime numbers between 1 and 100.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

______________________________________________________________________

### 2.2 Functions and Modules

#### Lecture Content:

1. **Defining and Calling Functions**

   ```python
   def greet(name):
       return f"Hello, {name}!"

   print(greet("Alice"))
   ```

1. **Importing Modules**

   ```python
   import math
   print(math.sqrt(16))
   ```

1. **Using `os` and `sys` Modules**

   ```python
   import os
   print(os.getcwd())  # Print current working directory
   ```

#### Exercises:

1. Create a function to calculate the factorial of a number.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

______________________________________________________________________

### 2.3 Error Handling and Exceptions

#### Lecture Content:

1. **Try-Except Blocks**
   ```python
   try:
       num = int(input("Enter a number: "))
       print(f"The square is {num ** 2}")
   except ValueError:
       print("Invalid input. Please enter a number.")
   ```
1. **Finally Clause**
   ```python
   try:
       file = open("example.txt", "r")
       print(file.read())
   except FileNotFoundError:
       print("File not found.")
   finally:
       print("Execution complete.")
   ```

#### Exercises:

1. Write a script that catches division by zero errors.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

______________________________________________________________________

### 2.4 Working with Data Structures

#### Lecture Content:

1. **Lists**

   ```python
   fruits = ["apple", "banana", "cherry"]
   fruits.append("orange")
   print(fruits)
   ```

1. **Dictionaries**

   ```python
   user = {"name": "Alice", "age": 25}
   print(user["name"])
   ```

1. **Sets and Tuples**

   ```python
   unique_numbers = {1, 2, 3, 3}
   print(unique_numbers)  # Output: {1, 2, 3}

   coordinates = (10, 20)
   print(coordinates[0])
   ```

#### Exercises:

1. Use a list to store the grades of students in a class. Calculate the average grade.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

______________________________________________________________________

### Additional Challenge:

Build a password manager application that uses dictionaries to store usernames
and passwords. Allow users to add, update, delete, and retrieve passwords
using functions. Include error handling for invalid inputs or operations.

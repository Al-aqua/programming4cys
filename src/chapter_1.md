# Chapter 1: Introduction to Python

## Overview

This chapter introduces Python, a powerful and versatile programming language widely used in cyber security for automation, scripting, and tool development. By the end of this chapter, students will:

- Understand why Python is essential for cyber security.
- Set up the Python environment on their systems.
- Learn basic Python syntax and write simple programs.

---

# Chapter 1: Introduction to Python

## 1.1 Overview of Python and its Relevance to Cyber Security

Python is one of the most widely used programming languages in cyber security due to its simplicity, versatility, and powerful libraries. It allows security professionals to automate tasks, analyze vulnerabilities, and develop tools for both offensive and defensive purposes. Python's large community ensures regular updates and extensive documentation, making it an excellent choice for tasks such as:

- Automating penetration testing
- Developing malware and payloads for ethical hacking
- Performing data analysis and threat intelligence
- Writing scripts for system monitoring and defense

### Why Python for Cyber Security?

1. **Ease of Learning:** Python's simple syntax enables even beginners to write functional scripts quickly.
1. **Cross-Platform:** Python runs seamlessly on Windows, macOS, and Linux, crucial for cross-platform security tasks.
1. **Extensive Libraries:** Libraries like Scapy, Requests, and PyCrypto provide ready-made functionality for network analysis, API interaction, and cryptography.
1. **Integration:** Python integrates well with other languages and tools, making it a go-to language for cyber security professionals.

---

## 1.2 Setting up the Python Environment

Before diving into Python programming, it is essential to set up the development environment. Follow these steps to configure Python for cyber security purposes:

### Step 1: Install Python

1. Visit [python.org](https://www.python.org/downloads/) to download the latest version of Python.
1. Ensure that the **"Add Python to PATH"** option is checked during installation.

### Step 2: Install an IDE or Text Editor

- **Recommended IDEs:** PyCharm (Community Edition), Visual Studio Code, or Jupyter Notebook.
- **Setting up VS Code:**
  - Install Python extension from the Extensions marketplace.
  - Configure linting and debugging tools for smoother coding.

### Step 3: Use Virtual Environments

Virtual environments allow you to manage dependencies for specific projects without affecting the global Python installation.

- Create a virtual environment:
  ```bash
  python -m venv venv_name
  ```
- Activate the virtual environment:
  - On Windows:
    ```bash
    venv_name\Scripts\activate
    ```
  - On macOS/Linux:
    ```bash
    source venv_name/bin/activate
    ```

### Step 4: Install Required Packages

Use `pip` to install necessary packages. For example:

```bash
pip install requests scapy paramiko pycrypto
```

---

## 1.3 Basic Syntax: Variables, Data Types, Input/Output

Understanding Python’s basic syntax is critical for building more complex scripts.

### 1.3.1 Variables and Data Types

Variables store data values. Python supports several data types:

- **Integer (int):** Whole numbers.
  ```python
  num = 10
  ```
- **Float (float):** Decimal numbers.
  ```python
  pi = 3.14
  ```
- **String (str):** Text values enclosed in quotes.
  ```python
  message = "Hello, Cyber Security!"
  ```
- **Boolean (bool):** True/False values.
  ```python
  is_active = True
  ```

### 1.3.2 Input/Output

#### Taking Input

Use the `input()` function to get user input:

```python
username = input("Enter your username: ")
print("Welcome, " + username + "!")
```

#### Printing Output

Use the `print()` function to display messages:

```python
print("Python is awesome!")
```

#### Formatting Output

Leverage f-strings for formatted outputs:

```python
name = "Alice"
age = 25
print(f"{name} is {age} years old.")
```

### 1.3.3 Comments

Comments explain code and are ignored during execution.

- **Single-line comments:**
  ```python
  # This is a comment
  ```
- **Multi-line comments:**
  ```python
  """
  This is a
  multi-line comment
  """
  ```

---

## Practical Exercises

### Exercise 1: Print a Welcome Message

Write a script to print a welcome message with user input:

```

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

### Exercise 2: Simple Calculator

Create a script that takes two numbers as input and performs the following basic arithmetic operations:

- Addition
- Subtraction
- Multiplication
- Division

```
-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

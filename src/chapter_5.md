# Chapter 5: Database Handling and Common Python Libraries for Cyber Security

## 5.1 Working with Databases

### 5.1.1 Overview of Databases

Databases are essential in cyber security as they store sensitive information that attackers often target. Understanding how to interact with databases securely is crucial for both offense and defense in cyber security.

- Common databases: SQLite, PostgreSQL, MySQL
- Importance of secure database handling

### 5.1.2 Setting Up SQLite in Python

SQLite is a lightweight, serverless database engine perfect for practice.

```python
import sqlite3

# Connect to a database (or create one if it doesn't exist)
connection = sqlite3.connect('cyber_security.db')

# Create a cursor object to interact with the database
cursor = connection.cursor()

# Create a table
cursor.execute('''CREATE TABLE users (
                    id INTEGER PRIMARY KEY,
                    username TEXT NOT NULL,
                    password TEXT NOT NULL)''')

# Commit changes and close the connection
connection.commit()
connection.close()
```

### Exercise 1: Setting Up Your First Database

1. Create a new SQLite database called `students.db`.

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

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

2. Add a table named `students` with columns `id`, `name`, and `grade`.

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

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

3. Insert three sample records.

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

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

4. Retrieve and print all records.

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

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

______________________________________________________________________

## 5.2 Writing Secure SQL Queries

### 5.2.1 Avoiding SQL Injection

SQL injection is a common attack where malicious SQL code is injected into queries. Use parameterized queries to prevent this.

#### Vulnerable Code:

```python
username = input("Enter username: ")
password = input("Enter password: ")
query = f"SELECT * FROM users WHERE username = '{username}' AND password = '{password}'"
cursor.execute(query)

result = cursor.fetchone()
if result:
    print("Login successful!")
else:
    print("Invalid username or password.")
```

#### Secure Code:

```python
query = "SELECT * FROM users WHERE username = ? AND password = ?"
cursor.execute(query, (username, password))
```

### Exercise 2: Secure Authentication Simulation

1. Write a script that asks the user for a username and password.
1. Check if the user exists in the `users` table.
1. Ensure the query is parameterized to prevent SQL injection.

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

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

______________________________________________________________________

## 5.3 Python Libraries for Cyber Security

### 5.3.1 Scapy: Packet Manipulation

Scapy is a powerful library for packet crafting and network analysis.
It allows users to analyze network traffic, simulate attacks, and
understand protocols.

#### Example: Sending an ICMP Ping

```python
from scapy.all import ICMP, IP, sr1

# Create an ICMP packet
packet = IP(dst="8.8.8.8")/ICMP()

# Send the packet and receive the response
response = sr1(packet, timeout=2)
if response:
    print("Ping successful")
else:
    print("Ping failed")
```

This example demonstrates how to test connectivity using Scapy. Such scripts
are useful for network diagnostics and penetration testing.

### 5.3.2 Requests: HTTP Requests

The Requests library simplifies HTTP interactions, making it easy to fetch and
send data over the web.

#### Example: Making a GET Request

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
if response.status_code == 200:
    print(response.json())
```

### Exercise 3: API Interaction

1. Use the Requests library to fetch data from the `https://jsonplaceholder.typicode.com/posts` API.
1. Parse the JSON response and print the title of each post.

______________________________________________________________________

## 5.4 Using Python for API Interactions

APIs are a cornerstone of modern cyber security workflows, enabling
programmatic interactions with web services.

#### Example: Posting Data

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"
data = {
    "title": "Cyber Security Post",
    "body": "Python is great for cyber security.",
    "userId": 1
}

response = requests.post(url, json=data)
print(response.json())
```

This example shows how to send data to an API. Understanding API interactions
is critical for tasks like automation, monitoring, and integration.

### Exercise 4: Automating API Calls

1. Write a Python script to automate sending multiple POST requests to `https://jsonplaceholder.typicode.com/posts`.
1. Use a loop to send 5 requests with different `title` and `body` values.
1. Print the response of each request.

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

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

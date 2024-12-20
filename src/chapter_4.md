# Chapter 4: Multithreading, Networking, and Sockets in Python

## Objectives:

- Understand the concepts of multithreading and multiprocessing.
- Learn the basics of socket programming for network communication.
- Explore the TCP/IP and UDP protocols and implement client-server models.

---

### 4.1 Introduction to Threading and Multiprocessing

#### Lecture Content:

1. **Threading Basics**

   ```python
   import threading

   def worker_function(name):
       print(f"Hello, {name} from worker thread")

   # Create a thread object
   thread = threading.Thread(target=worker_function, args=('World',))

   # Start the thread
   thread.start()

   # Wait for the thread to complete
   thread.join()
   ```

1. **Using Multiple Threads**

   ```python
   import threading
   import time

   def worker_function(text):
       counter = 1
       while counter <= 10:
           print(f"{text}: {counter}")
           counter += 1
           time.sleep(1)

   t1 = threading.Thread(target=worker_function, args=("Thread 1",))
   t2 = threading.Thread(target=worker_function, args=("Thread 2",))

   t1.start()
   t2.start()

   t1.join()
   t2.join()

   print("Done")
   ```

1. **Introduction to Multiprocessing**

   ```python
    import math
    import time
    from multiprocessing import Process

    def expensive_calculation(numbers):
        for number in range(numbers):
            math.sqrt(number**2)

    # Check if this script is being run directly (not imported as a module)
    if __name__ == "__main__":
        numbers = 5000000

        start = time.time()  # Record the start time
        expensive_calculation(numbers)
        expensive_calculation(numbers)
        expensive_calculation(numbers)
        end = time.time()  # Record the end time
        print(f"Single Process: {end - start}")  # Print the elapsed time

        # Create multiple processes
        p1 = Process(target=expensive_calculation, args=(numbers,))
        p2 = Process(target=expensive_calculation, args=(numbers,))
        p3 = Process(target=expensive_calculation, args=(numbers,))

        start = time.time()  # Record the start time
        p1.start()
        p1.join()
        end = time.time()  # Record the end time
        print(f"Multiprocessing: {end - start}")  # Print the elapsed time
   ```

#### Exercises:

1. Write a Python program to create two separate threads. Each thread should
   print numbers from 1 to 5 in parallel with a one-second delay between each
   number. Calculate and print the total time taken for both threads to
   complete their tasks.

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

How much time did the threads take to complete their tasks?

```

-----------------------------------------------------------------------------

```

2. Rewrite the above program using multiprocessing. Calculate and print the
   total time taken for both processes to complete their tasks.

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

How much time did the processes take to complete their tasks?

```

-----------------------------------------------------------------------------
```

1. Which of the two is faster, single-threaded or multi-threaded? and why?

```

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

---

### 4.2 Socket Programming Basics

#### Lecture Content:

1. **Creating a Simple Server**

   ```python
   import socket

   server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
   server.bind(("localhost", 8080))
   server.listen(1)
   print("Server is listening...")

   conn, addr = server.accept()
   print(f"Connection from {addr}")
   conn.sendall(b"Hello from server!")
   conn.close()
   ```

1. **Creating a Simple Client**

   ```python
   import socket

   client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
   client.connect(("localhost", 8080))
   data = client.recv(1024)
   print(f"Received: {data.decode()}")
   client.close()
   ```

1. **UDP Communication**

   ```python
   # Server
   import socket

   udp_server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
   udp_server.bind(("localhost", 8081))
   print("UDP Server is listening...")

   data, addr = udp_server.recvfrom(1024)
   print(f"Received message: {data.decode()} from {addr}")
   udp_server.sendto(b"Acknowledged", addr)
   udp_server.close()

   # Client
   import socket

   udp_client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
   udp_client.sendto(b"Hello UDP Server!", ("localhost", 8081))
   data, server = udp_client.recvfrom(1024)
   print(f"Received: {data.decode()} from {server}")
   udp_client.close()
   ```

#### Exercises:

1. Modify the UDP server and client example to allow sending multiple messages in a loop.

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

2. Create a Python script that scans open ports on a given host using sockets.

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

---

### 4.3 Understanding TCP/IP and UDP Protocols

#### Lecture Content:

1. **TCP vs. UDP**

   - **TCP**: Reliable, connection-oriented protocol ensuring data delivery.
   - **UDP**: Unreliable, connectionless protocol for faster communication.

1. **Packet Analysis with `socket`**

   - Using Python’s `socket` module to analyze packet data.

1. **Simulating Packet Loss (UDP Example)**

   ```python
   # server.py
   import random
   import socket

   # Create UDP socket
   server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
   server_address = ("localhost", 12345)
   server_socket.bind(server_address)

   print(f"Server listening on {server_address}")

   while True:
       try:
           # Receive data
           data, client_address = server_socket.recvfrom(1024)

           # Simulate 30% packet loss
           if random.random() > 0.3:
               print(f"Received from {client_address}: {data.decode()}")
               # Send acknowledgment
               response = f"ACK: {data.decode()}"
               server_socket.sendto(response.encode(), client_address)
           else:
               print(f"Packet lost (simulated): {data.decode()}")

       except KeyboardInterrupt:
           print("\nServer shutting down...")
           break

   server_socket.close()
   ```

   ```python
   # client.py
   import socket
   import time

   # Create UDP socket
   client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
   server_address = ("localhost", 12345)

   # Set timeout for receiving response
   client_socket.settimeout(1)

   message_count = 0

   while True:
       try:
           # Create message
           message = f"Message {message_count}"
           print(f"Sending: {message}")

           # Send data
           client_socket.sendto(message.encode(), server_address)

           try:
               # Wait for acknowledgment
               data, _ = client_socket.recvfrom(1024)
               print(f"Received: {data.decode()}")
               message_count += 1
           except socket.timeout:
               print(f"Timeout: No response received for message {message_count}")

           time.sleep(1)  # Wait 1 second before next message

       except KeyboardInterrupt:
           print("\nClient shutting down...")
           break

   client_socket.close()
   ```

#### Exercises:

1. When should you use TCP or UDP in a network application?

```

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------
```

---

### Additional Challenge:

Develop a multithreaded TCP server that handles multiple clients concurrently. The server should accept messages from clients and broadcast the messages to all connected clients.

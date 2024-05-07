# Hackhoven's SSTI-Class-Indexer

## Description
SSTI-Class-Indexer is a simple yet powerful tool designed to assist security researchers in identifying and indexing Python classes from outputs typically generated during Server-Side Template Injection (SSTI) vulnerability testing. This tool can help pinpoint potential classes useful for further exploitation, such as those that might allow command execution.

## Background
Server-Side Template Injection (SSTI) occurs when an attacker injects template code into a server-side template, leading to the execution of unintended commands or code. Python, with its rich introspection capabilities, allows researchers and attackers alike to explore object attributes like `__class__`, `__mro__`, and `__subclasses__` through simple template injections. Identifying classes that permit deeper system access or command execution is crucial in assessing the severity of SSTI vulnerabilities.

## Usage
To use SSTI-Class-Indexer, simply clone this repository, navigate to the directory, and run the script with Python. You'll be prompted to enter class names for which you wish to find indices based on SSTI output.

### Example Scenario
1. Retrieve current class instance: `http://MACHINE_IP/profile/{{ ''.class }}`
2. Climb up the inheritance tree: `http://MACHINE_IP/profile/{{ ''.class.mro }}`
3. Access the root object: `http://MACHINE_IP/profile/{{ ''.class.mro[1] }}`
4. List subclasses of the root object: `http://MACHINE_IP/profile/{{ ''.class.mro[1].subclasses() }}`

The next step is to find the correct index of the desired class, and use the payload `http://MACHINE_IP/profile/{{ ''.__class__.__mro__[1].__subclasses__()[INDEX] }}` thereafter.

### How It Works
The script parses the provided output, extracts all Python class references, and allows the user to search for specific classes to find their indices. This can be especially useful when identifying classes like `subprocess.Popen` which can be leveraged to execute arbitrary commands on the host machine.

### Installation
```bash
git clone https://github.com/Hackhoven/SSTI-Class-Indexer
cd SSTI-Class-Indexer
python3 ssti-class-indexer.py
```

# Developed by Hackhoven !




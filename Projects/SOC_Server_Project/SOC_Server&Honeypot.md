# SOC Server and Honey pot

Using cowrie for the honey pot.

### 1. Created the cowrie user. -- A seperate Linux account for running the honeypot. This helps limit its permissions if something goes wrong.
```sudo adduser --disabled-password --gecos "" cowrie```

### 1.1. Downloaded cowrie's source code.
```git clone https://github.com/cowrie/cowrie.git```

### 2. Created a Python virtual environment. -- A seperate Python environment called cowrie-env, and activated it inside the cowrie directory using: 
```python3 -m venv cowrie-env```

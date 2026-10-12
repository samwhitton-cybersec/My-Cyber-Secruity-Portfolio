# SOC Server and Honey pot

Using cowrie for the honey pot.

1. Created the cowrie user. -- A seperate Linux account for running the honeypot. This helps limit its permissions if something goes wrong.
```sudo adduser --disabled-password --gecos "" cowrie```

1.1. Installed cowrie on the raspi 5.
```git clone https://github.com/cowrie/cowrie.git```

2. Downloaded 

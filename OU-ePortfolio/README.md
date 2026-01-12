# My OU ePortfolio and my academic work

## Self-assessment Activity
### Using iptables to restrict port access.
Used iptables to set the firewall to accept incoming TCP traffic to ports 139 and 445 from the webmaster computer only.
- ```sudo iptables -A INPUT -p tcp -s 192.168.20.2 --dport 139 -j ACCEPT```
- ```sudo iptables -A INPUT -p tcp -s 192.168.20.2 --dport 445 -j ACCEPT```

Saved the config file:
- ```sudo sh -c "iptables-save > /etc/iptables/rules.v4"```
- Checked the file using:
```sudo iptables -S```

Then, set the firewall to accept all incoming traffic to port 80 from any connection.
- Using ```-s 0.0.0.0/0``` to specify from any device.

## Self-assessment Activity
### Using nmap to scan for open ports
```nmap -p0-35565 192.168.20.1```

- After restricting ports the output from the attacker machine now shows only port 80 as being open.
- On the webmaster's machine, all ports appear as open.

# My Home Lab Experiments and Projects

## Pi-hole setup and troubleshooting
### 1. Installation
- Installed Pi-hole on Raspberry Pi
- Set Pi-hole admin password ```pihole -a -p```
- Verified Pi-hole services were running ```systemctl status pihole-FTL```

### 2. Firewall and Port Configuration
- Checked open ports with ```sudo netstat -tulpn | grep :53```
- Found UFW blocking DNS queries -> allowed LAN access: ```sudo ufw allow from 192.168.0.0/24 to any port 53```
- Confirmed Pi-hole binding to port 53

### 3. Local DNS Testing
- Ran ```dig google.com @127.0.0.1``` on the Pi
- Verified DNS resolution worked locally
- Pinged external domains to confirm name resolution

### 4. Client Testing
- Configured host to use Pi-hole IP as DNS manually
- Flushed DNS cache ```ipconfig /flushdns``` on Windows
- Confirmed DNS queries resolved through Pi-hole
- Verified ads were being blocked (query log + test websites)

### 5. Router Integration
- Set Pi-hole IP as primary DNS in router
- Left Secondary DNS blank
- Verified network-wide DNS was routed through Pi-hole

### 6. Troubleshooting
- Fixed issues with Pi-hole not resolving DNS on clients -> UFW was blocking traffic
- Fixed "cannot bind to port 53" by restarting ```pihole-FTL```
- Fixed NTP resolution error by ensuring DNS worked before time sync
- Corrected Stubby ```.yml``` formatting (YAML indentation)

### 7. DNS-over-DoT Setup using Stubby
- Installed stubby ```sudo apt install stubby```
- Edited ```/etc/stubby/stubby.yml```:
```upstream_recursive_servers:
    -address_data: 1.1.1.1
      






docker-compose.yml
```
version: '3'

services:
  pptp:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: pptp-server
    hostname: pptp-server
    volumes:
      - ./dockerfiles/chap-secrets:/etc/ppp/chap-secrets
    environment:
      - WASP_ENDPOINT=https://endpoint
    restart: unless-stopped
    privileged: true
    network_mode: host
    
```
WASP_ENDPOINT: The server will send information when client connect or disconnect. Your endpoint must like these
    
    1. https://endpoint/api/pptp/up
    2. https://endpoint/api/pptp/down

chap-secrets:
```
#username server password ip
waspnet * waspnet *
```
Change chap-secrets with your username and password.

Mikrotik Remote Access

Get the last Octet of your Local IP then add 10000 for API and 20000 for Winbox

```
Example:
Your local ip is 10.1.0.2 get the last octet which is "2" then add 20000, your remote access url or ip is <public-ip>:20002 to access your winbox.

Where <public-ip> is your server public ip
```

-This Project is a Part of WASP RADIUS (All in One Hotspot & PPPoE System)
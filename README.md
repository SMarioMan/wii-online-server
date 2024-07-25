# wii-online-server

A preconfigured VM to host Wii and DS online games

Download here: https://github.com/SMarioMan/wii-online-server/releases/latest/

## VM Info

Ubuntu username: `marioman"`  
Ubuntu password: ` `  

Admin page: `http://[server ip here]:9009`  
Admin username: `marioman`  
Admin password: [leave blank]

## Configuring DNS
network connections -> right click network adapter -> properties -> Internet protocol version 4 (TCP/IPv4)  
Set DNS to IP of server  
The IP may not match the one I set. Check it with `ifconfig` in the VM. You must also change the file in `/etc/dnsmasq.conf` to match the server's IP.  

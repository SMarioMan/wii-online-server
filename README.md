# wii-online-server

A preconfigured VM to host Wii and DS online games

Download here: https://github.com/SMarioMan/wii-online-server/releases/latest/

## VM Info

Ubuntu username: `marioman"`  
Ubuntu password: ` `  

Admin page: `http://[server ip here]:9009`  
Admin username: `marioman`  
Admin password: [leave blank]

## Configuring Games

Games must have SSL disabled.
There are guides to do this for [Wii](https://github.com/barronwaffles/dwc_network_server_emulator/wiki#nintendo-wiiwii-u-configuration) and [DS](https://github.com/barronwaffles/dwc_network_server_emulator/wiki#nintendo-dsdsi3ds2ds-configuration).
The cheat code below should work in Dolphin for all Wii titles.

```ini
$No SSL [Fix94]
C0000000 0000000E
3C004E80 60000020
900F0000 3D808000
618C3000 3C00017F
6000CFFC 7C0903A6
3D607474 616B7073
800C0000 7C005800
40A20034 394C0003
392C0002 7D455378
38600000 8C050001
2C000000 38630001
4082FFF4 8C0A0001
9C090001 3463FFFF
4082FFF4 398C0001
4200FFC0 4E800020
*This code will work on ALL Wii Games, not just Mario Kart Wii.
*This code changes any instance of https to http on the url writes of your game. This is a good code for users of DWC-Emulator servers. You can use this code instead of configuring the Private Server NoSSL option within USB Loader GX.
*Region-Free
```

## Server Installation and Configuration
1. Download and install [VMWare Workstation Pro](https://blogs.vmware.com/workstation/2024/05/vmware-workstation-pro-now-available-free-for-personal-use.html). A direct download is available [here](https://softwareupdate.vmware.com/cds/vmw-desktop/ws/17.6.0/24238078/windows/core/). VMWare is free to use non-commercially.
1. Open the VM image provided here: https://github.com/SMarioMan/wii-online-server/releases/latest/. 
1. Log in to the VM, using the username "`marioman`" and the password "` `".
1. Within the VM, run `ifconfig` and note the IPv4 address. It will likely look something like `192.168.0.x`. Also note the MAC address associated with that interface.
1. Update the DNS configuration to match by running `sudo nano /etc/dnsmasq.conf`. Scroll to the bottom using the `Page Down` key. Replace all occurrences of `192.168.0.108` with the actual IP assigned to the server. Reload the DNS server by running `sudo /etc/init.d/dnsmasq restart`, which will apply the changes.
1. Change your system DNS settings to point to the custom server's DNS. In Windows, go to `Network Connections->Right-click main network adapter->Properties->Internet protocol version 4 (TCP/IPv4)` and select `Use the following DNS server addresses:`. Set the `Preferred DNS server:` to your VM's IP. Set `Alternate DNS server:` to a normal server, such as [8.8.8.8](https://developers.google.com/speed/public-dns) or your own router's DNS. Without this second DNS, your machine will be unable to resolve DNS queries whenever your VM isn't running. Alternatively, you can revert the manual DNS settings back to automatic in Windows when you aren't using this multiplayer setup.
1. (Optional): Go to your router's network settings and create a static IP rule bound to the DNS address you noted earlier, to ensure the IP address doesn't change from what you noted. The steps to do this vary with each router, so you will need to look this up yourself. If you don't do this, you will have to check and potentially update the dnsmasq rules (steps 4-6) each time you start the server.

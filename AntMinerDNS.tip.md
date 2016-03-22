#Tip - Fixing DNS Problems

If your miner takes a while to start hashing, you may have a DNS problem. When you connect it up to your LAN it uses DHCP to get its IP address and other local network information.

Mine would not find URLs on the Internet straight way (could not ping www.google.com) so it sat there doing nothing.

If you have this problem...

ssh to your miner:

root@myhost:~# ssh root@antminer.local (or its IP address if your router doesn't give it a name)

password is 'admin'

root@antMiner:~# vi /usr/share/udhcpc/default.script

add

dns="8.8.8.8 8.8.4.4"

to the file before the 'exec run-parts' line and save the change.

Now, when DHCP sets up your interface it will add these two IP addresses as name servers in /etc/resolv.conf. Try it by running

root@antMiner:~# udhcpc

You should see....

root@antMiner:~# udhcpc

udhcpc (v1.20.2) started

Sending discover...

Sending select for 192.168.1.66...

Lease of 192.168.1.66 obtained, lease time 86400

/etc/udhcpc.d/50default: Adding DNS 8.8.8.8

/etc/udhcpc.d/50default: Adding DNS 8.8.8.4

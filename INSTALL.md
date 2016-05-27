To install these scripts on your S5, follow the following steps:

1) Download onto a suitable computer using

```bash
$ wget https://github.com/minerchuck/AntMusic/archive/master.zip
```

I tried this directly on the miner but wget does not seem to like https.

2) Copy to your miner:
```bash
$ scp master.zip root@antMiner.local:.
```
3) Log onto the miner:

$ ssh root@antMiner.local

4) Extract the archive

$ unzip master.zip

5) Move the files

$ cd AntMusic-master

$ cp -a etc /

$ cp -a usr /

$ cp -a config /

6 Make the files executible

$ chmod +x /usr/local/bin/antstat

$ chmod +x /usr/local/bin/antrota

$ chmod +x /usr/local/bin/antthrottle

$ chmod +x /etc/init.d/antrota

$ chmod +x /etc/init.d/antthrottle

7 Customise your configutation

a) Examine and adapt files in /etc/antrota

b) Adjust MAXTEMP and MINTEMP in /usr/local/antthrottle or create a file called /config/antthrottle.conf containing two lines:

MAXTEMP=[your maximum threshold]

MINTEMP=[your minimum threshold]

8 Start the service(s) you want to use

$ /etc/init.d/antrota start

$ /etc/init.d/antthrottle start

9 Check that everything is OK

$ tail -f /var/log/ant*.log

==> /var/log/antrota.log <==
Starting...
Date: Thu May 26 13:19:13 2016

==> /var/log/antthrottle.log <==
Starting... 
Average Temperature: 51

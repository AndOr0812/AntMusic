To install these scripts on your S5, follow the following steps:

1) Download onto a suitable computer using

$ wget https://github.com/minerchuck/AntMusic/archive/master.zip

2) Copy to your miner:

$ scp master.zip root@antMiner.local

3) Log onto the miner:

$ ssh root@antMiner.local

4) Extract the archive

$ unzip master.zip

5) Move the files

$ cd AntMusic-master

$ cp -a etc /

$ cp -a usr /

6 Make the files executible

$ chmod +x /usr/local/bin/antstat

$ chmod +x /usr/local/bin/antrota

$ chmod +x /usr/local/bin/antthrottle

$ chmod +x /etc/init.d/antrota

$ chmod +x /etc/init.d/antthrottle

7 Customise your configutation

a) Examine and adapt files in /etc/antrota

b) Adjust MAXTEMP and MINTEMP in /usr/local/antthrottle

8 Start the service(s) you want to use

$ /etc/init.d/antrota start

$ /etc/init.d/antthrottle start

9 Check that everything is OK

$ tail -f /var/log/ant*.log

==> /var/log/antrota.log <==
Setting Date and Time using pool.ntp.org
Date: Wed May 25 12:42:31 2016

==> /var/log/antthrottle.log <==
Starting AntThrottle
Average Temperature: 52

# AntMusic
Tools to help you manage your Bitmain AntMiner.

The toolkit currently containts two daemons that can be installed on your Bitmain AntMiner to help you manage your gear. The objectives of this project are to provide bitcoin miners with tools that will allow them to a) maximize work b) minimize overheating c) manage noise.

The two daemons are currently running on my S5 without any untoward behaviour so far - but I give no guarantees: use at your own risk.

AntRota is a shell script that automatically switches between configurations at certain times of the day. You can have as many as 24 different configurations (one for each hour of the day) but you can leave gaps. You can use different configurations to increase or decrease the clock speed and to modify the fan speed. I have a night mode with a low clock speed and reduced fan RPM - so I can get some sleep - and other daytime configurations so the miner works hardest in the morning and then backs off a little for the afternoon.

Put the congfiurations in /etc/antrota and call them cgminer.conf.HH where HH is 00 for midnight, 01 for 1AM, etc. You can generate these files using the Bitmain-provided Miner Configutation web interface - just set things up how you want them and then copy /config/cgminer.config to /etc/antrota/.

AntThrottle is also a shell script that automatically backs the clock speed off if the miner gets too hot. Modify the script to specifty the temperature threshold - if the temperatiure reaches this, AntThrottle will reduce the clock speed by 25MHz and wait 30 seconds (and keep doing this until the temperature gets below your threshold or it runs out of predefined drops).

You can use both daemons together. AntRota will set the hour by hour profile and AntThrottle will try to prevent your equipment overheating (for example, if AntRota overclocks your miner and it gets hot, AntThrottle will bring it back down again shortly afterwards).

Both scripts are installed on your miner in /usr/local/bin/ and have a SystemV daemon handler in /etc/init.d. Start them using /etc/init.d/[daemon] start. To make them automatically start on system startup create a symbolic link (cd /etc/rcS.d; ln -s ../init.d/antrota S65antrota; ln -s ../init.d/antthrottle S66antthrottle;).

Both scripts produce log files is /var/log/. You will need to manage these if you run your miner for a very long time without a reboot (restarting the daemons will start the log files anew).

You will need to ssh onto your miner to install the software and configure it: using a linux box on the same LAN, ssh antMiner.local (user root, password admin). You can copy the software from your linux box using scp antMusic.zip antMiner.local:. . If you don't have a linux box on the same LAN you will have to figure out how to ssh to your miner yourself.

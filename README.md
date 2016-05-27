# AntMusic
Tools to help you manage your Bitmain AntMiner.

The toolkit currently containts two daemons and a utility that can be installed on your Bitmain AntMiner to help you manage your gear. The objectives of this project are to provide bitcoin miners with tools that will allow them to a) maximize work b) minimize overheating c) manage noise.

The two daemons are currently running on my S5 without any untoward behaviour so far - but I give no guarantees: use at your own risk.

[i]antrota[/i] is a shell script that automatically switches between configurations at certain times of the day. You can have as many as 24 different configurations (one for each hour of the day) but you can leave gaps. You can use different configurations to increase or decrease the clock speed and to modify the fan speed. I have a night mode with a low clock speed and reduced fan RPM - so I can get some sleep - and other daytime configurations so the miner works hardest in the morning and then backs off a little for the afternoon.

Put the congfiurations in /etc/antrota and call them cgminer.conf.HH where HH is 00 for midnight, 01 for 1AM, etc. You can generate these files using the Bitmain-provided Miner Configutation web interface - just set things up how you want them and then copy /config/cgminer.config to /etc/antrota/.

AntThrottle is also a shell script that automatically reduces the clock speed if the miner gets too hot and increases it when it is running cool. Modify the script to specifty the maximum and minimum temperature thresholds. If the temperatiure reaches the maximum, AntThrottle will reduce the clock speed by 25MHz and wait 30 seconds (and keep doing this until the temperature gets below your threshold or it runs out of predefined drops). If the temperature goes below the minimum it will be increased in steps of 25MHz up to a maximum of 400MHz unless the temperature goes above the minimum.

You can use both daemons together. AntRota will set the hour by hour profile and AntThrottle will try to prevent your equipment overheating (for example, if AntRota overclocks your miner and it gets hot, AntThrottle will bring it back down again shortly afterwards).

Both scripts are installed on your miner in /usr/local/bin/ and have a SystemV daemon handler in /etc/init.d. Start them using /etc/init.d/[daemon] start. If you make any changes to either script, restart it using /etc/init.d/[daemon] stop and /etc/init.d/[daemon] start.

Both scripts produce log files is /var/log/. You will need to manage these if you run your miner for a very long time without a reboot (restarting the daemons will start the log files anew).

AntStat is a helper script that will enable you to get various statistics about your miner from the command line. It takes one argument (currently HASH, FREQ, FAN1, FAN2, TEMP or HW for hash rate in GHx, clock frequency in MHz, fan 1 RPM, fan 2 RPM, average temperature and harware error percentage).

You will need to ssh onto your miner to install the software and configure it: using a linux box on the same LAN, ssh antMiner.local (user root, password admin). You can copy the software from your linux box using scp AntMusic-master.zip antMiner.local:. . If you don't have a linux box on the same LAN you will have to figure out how to ssh to your miner yourself.

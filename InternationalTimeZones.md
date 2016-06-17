The Angstrom distro used on the S5 does not have time zone date so the date binary will always use UTC. To set the time to your local time zone and daylight saving offset, you need to set the TZ environment variable to GMT[+/-][1..12]. To ensure you have the correct value, try
`$TZ GMT+6 date` (or whatever your adjustment to GMT is)
from the command line. I don't know quite why but the offset seems to be the reverse of what you would expect. For me, here in the UK in summer time, I need to use
`$TZ GMT-1 date`
to see the correct date. The output of
`date`
is
`Fri Jun 17 09:06:54 UTC 2016`, which is UTC
but the output of
`TZ GMT-1`
is
`Fri Jun 17 10:07:29 GMT 2016`, which is BST (British Summer Time), but BST is defined as GMT+1! This means that if you are in the US, you need to add your time difference to UTC and in France, Russia and Japan, subtract it.

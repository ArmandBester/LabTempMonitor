## Enable ntp on local ntp server
$ sudo nano /etc/systemd/timesyncd.conf

*Edit the file and add:*

NTP=ntp.ufs.ac.za  * change this to some appropriate *


$ sudo timedatectl set-ntp false

$ sudo timedatectl set-ntp true

$ timedatectl status * check that the time is now correct *

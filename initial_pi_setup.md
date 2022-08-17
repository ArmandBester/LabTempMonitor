## Enable ntp on local ntp server
$ sudo nano /etc/systemd/timesyncd.conf

*Edit the file and add:*

NTP=ntp.ufs.ac.za    (*change this to some appropriate*)


$ sudo timedatectl set-ntp false

$ sudo timedatectl set-ntp true

$ timedatectl status    (*check that the time is now correct*)


## Setup a local socks proxy and configure apt to use it.

$ sudo nano /etc/apt/apt.conf.d/proxy.conf

*and add the line:*

Acquire::http::proxy "socks5h://127.0.0.1:1080";  (*adjust you proxy settings*)





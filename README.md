# LabTempMonitor

From: https://www.superhouse.tv/41-datalogging-with-mqtt-node-red-influxdb-and-grafana/

## Mosquitto

sudo apt update
sudo apt upgrade

sudo apt install mosquitto mosquitto-clients

echo "mqtt_username:mqtt_password" > pwfile

mosquitto_passwd -U pwfile

cat pwfile

sudo mv pwfile /etc/mosquitto/

sudo nano /etc/mosquitto/mosquitto.conf

'''
pi@raspberrypi:~ $ cat /etc/mosquitto/mosquitto.conf 
# Place your local configuration in /etc/mosquitto/conf.d/
#
# A full description of the configuration file is at
# /usr/share/doc/mosquitto/examples/mosquitto.conf.example
per_listener_settings true

pid_file /run/mosquitto/mosquitto.pid

persistence true
persistence_location /var/lib/mosquitto/

log_dest file /var/log/mosquitto/mosquitto.log

allow_anonymous false
password_file /etc/mosquitto/pwfile

include_dir /etc/mosquitto/conf.d
'''

## InfluxDB

https://pimylifeup.com/raspberry-pi-influxdb/

curl https://repos.influxdata.com/influxdb.key | gpg --dearmor | sudo tee /usr/share/keyrings/influxdb-archive-keyring.gpg >/dev/null

echo "deb [signed-by=/usr/share/keyrings/influxdb-archive-keyring.gpg] https://repos.influxdata.com/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdb.list

sudo apt update

sudo apt install influxdb

sudo systemctl unmask influxdb
sudo systemctl enable influxdb

sudo systemctl start influxdb

https://www.superhouse.tv/41-datalogging-with-mqtt-node-red-influxdb-and-grafana/

influx
CREATE USER admin WITH PASSWORD 'adminpassword' WITH ALL PRIVILEGES
exit

sudo nano /etc/influxdb/influxdb.conf

- Press CTRL+W to search for the section called [HTTP].

'''
auth-enabled = true
pprof-enabled = true
pprof-auth-enabled = true
ping-auth-enabled = true
'''

sudo systemctl restart influxdb

influx -username admin -password adminpassword
CREATE DATABASE sensors
exit


# Node-Red

sudo apt install build-essential git

bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

npm install node-red-contrib-influxdb

# Grafana

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

sudo apt update
sudo apt install grafana

sudo systemctl enable grafana-server

sudo systemctl start grafana-server













mosquitto_pub -u mqtt_username -P mqtt_password -h 192.168.1.30 -p 1883 -t "cmnd/DVES_F1D452_fb/POWER1" -m "ON"

mosquitto_pub -u mqtt_username -P mqtt_password -h 192.168.1.30 -p 1883 -t "cmnd/DVES_F1D452_fb/POWER1" -m "TOGGLE"

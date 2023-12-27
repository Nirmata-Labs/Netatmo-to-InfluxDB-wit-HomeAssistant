# Netatmo-to-InfluxDB-wit-HomeAssistant
Write Netatmo weather Data into a InfluxDBv2 using HomeAssistant Docker on a RaspberryPi 4


```
sudo raspi-config
sudo reboot
curl https://download.argon40.com/argon1.sh | bash
reboot
```
```
sudo apt-get update
sudo apt-get full-upgrade
sudo rpi-update
sudo reboot
sudo rpi-eeprom-update -d -a
sudo reboot
```
```
mkdir Docker/Home-Assistant
docker run -d
  --name homeassistant
  --privileged
  --restart=unless-stopped
  -e TZ=Europe/Berlin
  -v /Docker:/config
  -v /run/dbus:/run/dbus:ro
  --network=host
  ghcr.io/home-assistant/home-assistant:stable
```

```
docker stop homeassistant
docker compose up -d
docker remove homeassistant
docker remove -f homeassistant
docker run -d grafana
docker ps
```
```
docker run -d --name="influxdb" --restart always -p 8086:8086 -p 8083:8083 -v /volume1/docker/influxdb/:/var/lib/influxdb influxdb
docker run -d -p 3000:3000 --name="grafana"     -v /volume1/docker/grafana:/var/lib/grafana     grafana/grafana
 docker run -d --name=grafana -p 3000:3000 grafana/grafana
```
```  
  205  sudo find / -type f -name "configuration.yaml"
  206  cd /Docker/Home-Assistant/
  211  sudo nano configuration.yaml 
```



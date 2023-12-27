# Netatmo-to-InfluxDB-with-HomeAssistant

This repository provides instructions and configuration steps for setting up a Raspberry Pi 4 with Netatmo weather data, InfluxDBv2, and HomeAssistant Docker. The goal is to facilitate the integration of Netatmo weather data into InfluxDB, using HomeAssistant in a Docker container on a Raspberry Pi 4.

[TOC]

## Raspberry Pi Configuration

1. **Update Raspberry Pi Configuration:**
   ```bash
   sudo raspi-config
   sudo reboot
   ```

2. **Install Argon One Script:**
   ```bash
   curl https://download.argon40.com/argon1.sh | bash
   reboot
   ```

3. **Update Raspberry Pi System:**
   ```bash
   sudo apt-get update
   sudo apt-get full-upgrade
   sudo rpi-update
   sudo reboot
   sudo rpi-eeprom-update -d -a
   sudo reboot
   ```

## HomeAssistant Docker Setup

1. **Create Docker Home Assistant Directory:**
   ```bash
   mkdir Docker/Home-Assistant
   ```

2. **Run Home Assistant Docker Container:**
   ```bash
   docker run -d \
     --name homeassistant \
     --privileged \
     --restart=unless-stopped \
     -e TZ=Europe/Berlin \
     -v /Docker:/config \
     -v /run/dbus:/run/dbus:ro \
     --network=host \
     ghcr.io/home-assistant/home-assistant:stable
   ```

3. **Manage Home Assistant Docker Container:**
   ```bash
   docker stop homeassistant
   docker compose up -d
   docker remove homeassistant
   docker remove -f homeassistant
   docker run -d grafana
   docker ps
   ```

## InfluxDB and Grafana Docker Setup

1. **Run InfluxDB Docker Container:**
   ```bash
   docker run -d --name="influxdb" --restart always -p 8086:8086 -p 8083:8083 -v /volume1/docker/influxdb/:/var/lib/influxdb influxdb
   ```

2. **Run Grafana Docker Container:**
   ```bash
   docker run -d -p 3000:3000 --name="grafana" -v /volume1/docker/grafana:/var/lib/grafana grafana/grafana
   ```

   Or using an alternative command:
   ```bash
   docker run -d --name=grafana -p 3000:3000 grafana/grafana
   ```

## Home Assistant Configuration

1. **Locate Configuration File:** 
   ```bash
   sudo find / -type f -name "configuration.yaml"
   cd /Docker/Home-Assistant/
   ```

2. **Edit Configuration File:** 
   ```bash
   sudo nano configuration.yaml
   ```

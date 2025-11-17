# Troubleshooting Guide

Common issues and solutions for Powerwall3MQTT.

## Network and Connectivity

### Cannot connect to Powerwall

**Symptom:** Connection refused or timeout errors to `192.168.91.1`

**Solution:**
- Verify you're connected to the Powerwall WiFi network (SSID: `TeslaPW_*` or `TEG-*`)
- Check you have an IP in `192.168.91.0/24` range
- Test connectivity: `ping 192.168.91.1`
- Verify the Powerwall gateway is powered on
- Confirm direct WiFi connection (wired/routing will not work with firmware 25.10.1+)

### Empty data / all zeros (Multi-Powerwall systems)

**Symptom:** Logs show `sitemanagerStatus.isRunning: False`, config/status data is empty or all zeros, but firmware version is retrieved successfully

**Root cause:** You may be connected to a **follower Powerwall instead of the leader**

**Solution:**
- In multi-Powerwall systems, only the leader runs the site manager and has operational data
- Scan for all Powerwall WiFi networks: `sudo iw dev wlan0 scan | grep "SSID: TeslaPW"`
- Connect to each `TeslaPW_*` network until you find the one where `sitemanagerStatus.isRunning: true`
- The leader Powerwall's serial number should match what's shown in the Tesla app

### Authentication failed (Powerwall)

**Symptom:** HTTP 401 errors in logs

**Solution:**
- Verify password matches your gateway password
- Check the password on the Powerwall touchscreen: **Settings** → **About**
- Or check the sticker on the physical gateway device

## MQTT Issues

### Cannot connect to MQTT broker

**Symptom:** Connection refused to MQTT broker

**Solution:**
- Verify MQTT broker is running: `telnet YOUR_MQTT_HOST 1883`
- Check MQTT host and port configuration
- Verify username/password if authentication is enabled
- Ensure MQTT broker is accessible from the Powerwall WiFi network
- Check firewall rules on MQTT broker host

### Device not appearing in Home Assistant

**Symptom:** No Powerwall device in MQTT integration

**Solution:**
- Verify MQTT integration is configured in Home Assistant
- Check MQTT base topic matches HA discovery prefix (usually `homeassistant`)
- Monitor MQTT messages: **Developer Tools** → **MQTT** → Listen to `homeassistant/#`
- Check the logs for "Published discovery" messages

## API and Rate Limiting

### Rate limiting / HTTP 429 errors

**Symptom:** Logs show "Rate limited" or HTTP 429 responses

**Solution:**
- Increase polling interval to 60 seconds or higher
- The app will automatically back off when rate limited
- Wait a few minutes for the Powerwall API to recover
- Avoid polling intervals below 5 seconds

## Getting Help

When reporting issues, please include:
- Log output (enable DEBUG logging if possible)
- Firmware version from logs
- Network configuration (SSID, IP address)
- For multi-Powerwall systems: Output showing `sitemanagerStatus`

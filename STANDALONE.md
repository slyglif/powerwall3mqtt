# Standalone Deployment

Run Powerwall3MQTT independently without Home Assistant OS, using Docker Compose.

## Why Standalone?

- Run on any Docker-capable system with WiFi access to Powerwall
- Use with Home Assistant container mode (not HAOS)
- Integrate with any MQTT broker
- Deploy on dedicated monitoring devices

## Prerequisites

1. **Docker and Docker Compose** installed
2. **WiFi connection** to Powerwall WiFi network (`TeslaPW_*` or `TEG-*` SSID)
   - Must obtain IP in `192.168.91.0/24` range
   - Wired connection will not work (firmware 25.10.1+ restriction)
3. **MQTT broker** accessible from Powerwall WiFi network
4. **Gateway password** from Powerwall touchscreen or sticker

## Quick Start

1. **Clone repository:**
   ```bash
   git clone https://github.com/slyglif/powerwall3mqtt.git
   cd powerwall3mqtt
   ```

2. **Create configuration:**
   ```bash
   cp .env.example .env
   nano .env
   ```

   Required settings:
   ```bash
   TEDAPI_PASSWORD=your-powerwall-password
   MQTT_HOST=your-mqtt-broker-ip
   MQTT_PORT=1883
   ```

3. **Start service:**
   ```bash
   docker-compose up -d
   ```

4. **Verify operation:**
   ```bash
   docker-compose logs -f
   ```

## Configuration

All settings are configured via `.env` file using environment variables with the `POWERWALL3MQTT_CONFIG_` prefix.

**Required:**
- `TEDAPI_PASSWORD` - Gateway password
- `MQTT_HOST` - MQTT broker hostname/IP
- `MQTT_PORT` - MQTT broker port

**Optional:**
- `MQTT_USERNAME` / `MQTT_PASSWORD` - MQTT authentication
- `MQTT_SSL` - Enable SSL/TLS
- `TEDAPI_POLL_INTERVAL` - Polling frequency (1-300 seconds, default 30)
- `TEDAPI_REPORT_VITALS` - Per-Powerwall metrics for multi-unit systems
- `LOG_LEVEL` - Logging verbosity (DEBUG/INFO/WARNING/ERROR/CRITICAL)

See [.env.example](.env.example) for complete list with descriptions.

## Management

```bash
# Start
docker-compose up -d

# Stop
docker-compose down

# Restart
docker-compose restart

# View logs
docker-compose logs -f

# Update
git pull && docker-compose build && docker-compose up -d
```

## Troubleshooting

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues and solutions.

**Standalone-specific issues:**

- **Container keeps restarting:** Check `.env` file exists and contains required variables
- **Network mode errors:** Ensure `network_mode: host` is set in `docker-compose.yml`

## Differences from HAOS Add-on

| Feature | Standalone | HAOS Add-on |
|---------|------------|-------------|
| Configuration | `.env` file | Web UI |
| Installation | Git clone + docker-compose | Add-on store |
| MQTT Integration | Any broker | Auto-configured |
| Auto-start | Manual (systemd optional) | Built-in |
| Features | Identical | Identical |

Both versions support the same features: authentication, SSL/TLS, vitals reporting, Home Assistant auto-discovery, and all polling options.

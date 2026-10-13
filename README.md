# QuickMill Sunny ESPHome Bridge

ESPHome YAML configuration to bridge a **QuickMill Sunny** espresso machine to **Home Assistant** via BLE.

## Architecture

- **ESP32-WROOM-32** connects to the Sunny's isolated Wi-Fi (`Quickmill5D`)
- HTTP requests to the Sunny's web UI at `http://192.168.1.1`
- Data exposed to Home Assistant via the **ESPHome API** (BLE transport)
- Uses the existing HA Bluetooth Proxy (`esp32-bluetooth-proxy-8c77cc`)

## Features

### Sensors (read)
- Brew temperature (Coffee & Steam)
- Single/Double shot pre-infusion & infusion times
- Water dose time
- Filter life
- Total & partial shot counters
- Machine state & water level

### Numbers (set)
- Brew temperature (Coffee & Steam)
- Pre-infusion duration (Single & Double)
- Infusion duration (Single & Double)
- Water dose time
- Filter life

### Switches (control)
- Power on/off
- Steam boiler toggle
- Eco mode
- Standby mode
- Machine restart

## Setup

1. Flash the ESP32 with ESPHome 2026.x
2. Edit `esphome/quickmill-sunny.yaml`:
   - Set `DEIN_ESPHOME_API_KEY`
   - Set `OTA_PASSWORT`
3. Install via ESPHome Add-on in Home Assistant
4. The device will connect to `Quickmill5D` and appear in HA via BLE

## HA Dashboard

Import `dashboards/quickmill-sunny.yaml` in Home Assistant:
**Settings → Dashboards → Import**

## QuickMill Sunny API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/getConfig` | All configuration values |
| POST | `/setDose1preinf/!{value}` | Single shot pre-infusion [s] |
| POST | `/setDose1inf/!{value}` | Single shot infusion [s] |
| POST | `/setDose2preinf/!{value}` | Double shot pre-infusion [s] |
| POST | `/setDose2inf/!{value}` | Double shot infusion [s] |
| POST | `/setDoseWater/!{value}` | Water dose time [s] |
| POST | `/setpoint_Group/!{value}` | Coffee temperature setpoint [°C] |
| POST | `/setpoint_Service/!{value}` | Steam temperature setpoint [°C] |
| POST | `/setFiltroAcqua/!{value}` | Filter life [h] |
| POST | `/EnableService/!{0\|1}` | Steam boiler on/off |
| POST | `/EnableECO/!{0\|1}` | Eco mode on/off |
| POST | `/EnableStandby/!{0\|1}` | Standby on/off |
| POST | `/ON_OFF/!statePower$ON\|OFF` | Power toggle |
| POST | `/Riavvio/` | Restart machine |

## License

MIT
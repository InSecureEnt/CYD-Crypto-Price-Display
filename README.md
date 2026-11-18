# CYD-Crypto-Price-Display
2.8 CYD Crypto &amp; Weather Tracker

**CYD Crypto Price Monitor — Project Summary**

**Hardware:** ESP32-2432S028 (CYD) — 320×240 ST7789 + XPT2046 touch

**Firmware location:** 
- `cyd-crypto-ticker_firmware.bin` — main firmware - 0x10000
- `bootloader.bin` — 0x1000
- `partitions.bin` — 0x8000

**Flash command (host):**
```bash
esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 921600 \
  write_flash 0x1000 bootloader.bin 0x8000 partitions.bin 0x10000 cyd-crypto-ticker_firmware.bin
```

**Features:**
| Interaction | Action |
|-------------|--------|
| Single tap | Refresh crypto prices |
| Triple-tap (≤2s) | Toggle weather page |
| Long-press (3s) | Cycle display rotation (0→1→2→3) |
| Hold screen on boot | Clear WiFi/config → AP mode |

**Config portal (no rebuild needed):**
- First boot: AP `CYD-Ticker-Setup` → `http://192.168.4.1`
- After WiFi: `http://<device-ip>/config`
- Sets: WiFi, CoinGecko IDs/names/tickers/decimals (≤10 coins), currency, refresh/retry intervals, green/red 24h colors, **weather ZIP**, rotation

**Weather:** Open-Meteo (geocodes ZIP → lat/lon → current temp/condition/wind), graceful error display

**Serial debug:** `screen /dev/ttyUSB0 115200` — shows WiFi, API calls, config loads, weather fetch errors

**Source:** `/opt/data/CYD-Crypto-Price-Monitor/` (modified from upstream with web config + weather + rotation NVS)

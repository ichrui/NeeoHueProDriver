# NeeoHueProDriver
# Hue Bridge Pro – meta Driver for NEEO

Adapted version of the original Hue driver by **[jac459](https://github.com/jac459/NeeoHueDriver)** for the [meta](https://github.com/jac459) remote framework, extended by **ichrui** to support the new **Philips Hue Bridge Pro**.

## What was changed?

The Hue Bridge Pro differs technically from older bridge generations:

- **HTTPS only** (port 443) instead of HTTP – all bridge calls were updated accordingly
- **Self-signed certificate** – the meta process must be started with `NODE_TLS_REJECT_UNAUTHORIZED=0` (see below)
- **mDNS discovery doesn't work reliably with the Pro** – the bridge IP is therefore entered manually during setup instead of being auto-discovered
- Drivers were renamed (`Hue Pro` / `Hue Pro Groups`) so they can be installed alongside the original drivers for older bridges without conflicting

The core logic (switching lights, brightness, color picker) is unchanged from the original driver.

## Files

| File | Purpose |
|---|---|
| `philipsHuePro.json` | Individual Hue lights |
| `philipsHueProGroup.json` | Hue rooms/zones (groups) |
| `Resources/` | Color picker icons – place in the repo under `Resources/` so the image URLs in the JSON files work |

## Installation

1. Copy the files into your meta driver's `devices` folder
2. Start the meta process with the certificate exception enabled (required due to the Bridge Pro's self-signed certificate):
   ```bash
   cd /path/to/meta
   NODE_TLS_REJECT_UNAUTHORIZED=0 pm2 start meta.js --name meta
   pm2 save

# evcc-cyd

A tiny touch control panel for [EVCC](https://github.com/evcc-io/evcc) running on the **Sunton ESP32‑2432S028R “Cheap Yellow Display (CYD)”** board. It shows key EV/charger status and gives you quick mode tweaks on a low‑cost, wall/desk‑mounted screen.

> Status: early, hackable. PRs welcome.

---

## Hardware

- **Display/MCU:** Sunton **ESP32‑2432S028R** (aka “Cheap Yellow Display / CYD”)
- **Power:** 5 V via Micro‑USB (typical phone charger works)
- **Back end:** A reachable **EVCC** instance on your LAN

### Optional: 3D‑printed enclosure

Use this community enclosure designed for the Sunton ESP32‑2432S028R (CYD):

- Printables model: **Enclosure for Sunton ESP32‑2432S028R “Cheap Yellow Display”**  
  https://www.printables.com/model/685845-enclosure-for-sunton-esp32-2432s028r-cheap-yellow-

> Notes: Check the model page for the exact fasteners/inserts. Common builds use small M3 screws or heat‑set inserts depending on the variant. Print one front and one back (plus the optional stand if you want a desk setup).

---

## Getting started

### 1) Clone
```bash
git clone https://github.com/donnyvangulik/evcc-cyd.git
cd evcc-cyd
```

### 2) Build & flash

You can use **PlatformIO (VS Code)** or the **Arduino IDE**—pick one:

**PlatformIO (recommended)**
1. Open the folder in VS Code with the PlatformIO extension installed.
2. Select the ESP32 environment for the Sunton CYD (or a generic ESP32 Dev Module).
3. Click **Build** then **Upload** to flash over Micro‑USB.

**Arduino IDE**
1. Install ESP32 boards support (via Boards Manager).
2. Select an ESP32 Dev Module (or a CYD-specific board profile if you have one).
3. Open the main sketch / project and click **Upload**.

### 3) Configure network & EVCC

Create `include/config.h` (or `src/config.h`) if it doesn’t exist, for example:

```cpp
// config.h
#pragma once

// Wi‑Fi
#define WIFI_SSID       "your-ssid"
#define WIFI_PASSWORD   "your-password"

// EVCC server (use IP if mDNS isn't resolving)
#define EVCC_BASE_URL   "http://evcc.local:7070"

// Optional basic auth if you use it
#define EVCC_USER       ""
#define EVCC_PASSWORD   ""
```

Re‑build and re‑flash after editing your configuration.

### 4) Power it up

Power the CYD via Micro‑USB. On boot, it should join your Wi‑Fi and query your EVCC server.

---

## Repository layout

- `src/` – firmware sources
- `include/` – headers and local configuration (e.g., `config.h`)
- `lib/` – private libraries (if any)
- Project files for your chosen toolchain (PlatformIO or Arduino)

*(Folders may evolve—check the tree once you clone.)*

---

## Troubleshooting

- **Blank or garbled display:** double‑check you selected an ESP32 board/partition that fits and the correct display/touch drivers for your CYD variant.
- **No EVCC data:** confirm the device can reach your EVCC host, and that `EVCC_BASE_URL` (and auth, if used) are correct. Try an IP address instead of `.local` if needed.
- **Wi‑Fi issues:** ensure you’re on 2.4 GHz and credentials are correct.

---

## Acknowledgements

- [EVCC](https://github.com/evcc-io/evcc)
- The “Cheap Yellow Display” community
- 3D enclosure by the Printables author linked above

## License

See the `LICENSE` file in this repository.

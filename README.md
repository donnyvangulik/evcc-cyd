evcc-cyd

A tiny touch control panel for EVCC
 running on the Sunton ESP32-2432S028R “Cheap Yellow Display (CYD)” board. Think: glanceable EV status + quick mode tweaks on a low-cost, wall/desk-mounted screen. 
GitHub
+1

Status: early, hackable, MIT-licensed. Contributions welcome!

Features (current & planned)

Shows key EVCC status at a glance (charger state, power, etc.).

Touch UI designed for the 2.8″ CYD.

Local/LAN only; no cloud.

Lightweight firmware you can flash in minutes.

(If you’re reading this before features are complete, treat it as the starting point for the UI.)

Hardware

Display/MCU: Sunton ESP32-2432S028R (aka Cheap Yellow Display / CYD)
2.8″ 240×320 TFT (ILI9341), resistive touch (XPT2046), ESP32-WROOM-32, Micro-SD, USB-Micro for power/programming. Typical supply 5 V via USB. 
circuitpython.org
+2
esp3d.io
+2

Power: 5 V over micro-USB (a phone charger works). 
esp3d.io

Back end: A running EVCC on your network (Docker, binary, etc.). 
GitHub

Optional: 3D-printed case

Use this excellent enclosure for the Sunton ESP32-2432S028R (with optional desk stand):

STL: Enclosure for Sunton ESP32-2432S028R “Cheap Yellow Display” by @mdkendall
Printables: https://www.printables.com/model/685845-enclosure-for-sunton-esp32-2432s028r-cheap-yellow-
 
Printables

Notes from the model page (summarized):

Prints without supports; print one front and one back (two front variants: threaded inserts vs self-tap).

Hardware: 4× M3 inserts (~4 mm) if using inserts, 4× M3×6 screws (use M3×10 for two screws if you add the stand).

Designed for the ESP32-2432S028R variant with micro-USB. 
Printables

Quick start

Clone this repo:

git clone https://github.com/donnyvangulik/evcc-cyd.git


Open & build with your preferred toolchain:

PlatformIO (recommended): open the folder in VS Code with the PlatformIO extension, select the ESP32 environment, then Build → Upload.

Arduino IDE: install ESP32 board support, select an ESP32 Dev Module (or the Sunton board profile, if available), then Compile → Upload.

Configure Wi-Fi & EVCC endpoint:

Look for a src/config.h (or create one from src/config.example.h if present) and set:

// src/config.h
#pragma once
#define WIFI_SSID       "your-ssid"
#define WIFI_PASSWORD   "your-pass"

// EVCC server reachable on your LAN
#define EVCC_BASE_URL   "http://evcc.local:7070"
// Optional auth if your EVCC is protected:
#define EVCC_USER       ""
#define EVCC_PASSWORD   ""


Flash again after editing.

Power it up over micro-USB. The UI should connect to your Wi-Fi and start talking to EVCC on your network. 
GitHub

Tip: If your EVCC host doesn’t resolve via mDNS (e.g., evcc.local), use the IP address instead.

Project layout

src/ — firmware sources for the CYD (ESP32).

include/ — headers / configuration (e.g., config.h).

lib/ — private libraries (if any).

platformio.ini or .ino — depending on toolchain.

(Exact folders may evolve; check the tree once you clone.)

Troubleshooting

White screen / no touch: double-check the selected board and display/touch drivers (ILI9341/XPT2046 are standard for the CYD). 
circuitpython.org

No data from EVCC: verify EVCC is reachable from the CYD and that the base URL and (if used) credentials are correct. 
GitHub

Wi-Fi issues: try a 2.4 GHz network (ESP32 prefers it). 
circuitpython.org

Why the “Cheap Yellow Display”?

“Cheap Yellow Display” (CYD) is the community nickname for the ESP32-2432S028R board popularized by Brian Lough and others. It’s inexpensive and perfect for small UIs like this one. 
GitHub

Roadmap

More EVCC metrics (per-phase currents, PV/battery flow).

Mode switching (e.g., pv, minpv, now).

Settings page (limits, setpoints).

Theming & icons.

Acknowledgements

EVCC
 for the awesome local charging controller. 
GitHub

The CYD community & resources (see witnessmenow/ESP32-Cheap-Yellow-Display
). 
GitHub

Enclosure by @mdkendall on Printables. 
Printables

License

MIT (see LICENSE).

If you want, I can tweak the README around the exact config file names and build system once you confirm whether you’re using PlatformIO, Arduino, or ESP-IDF.

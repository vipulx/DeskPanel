# DeskPanel – ESPHome Control Panel



DeskPanel is an **ESPHome-based smart control panel** built using an **ESP32-S2 Mini (Lolin S2 Mini)**. It integrates relays, OLED display, WS2812 LED indicators, rotary encoder, IR receiver, and Home Assistant entities into a single desk-mounted control unit.

---

## ✨ Features

- **Smart Display (OLED 128x64, SSD1306)**

  - Displays time, IP address, and device states
  - Temporary custom messages from Home Assistant (`input_text`)
  - Auto screen timeout with wake-up on interaction

- **Status Lighting**

  - WS2812 LED strip (3 LEDs)
  - Binary onboard LED indicator

- **Control Hardware**

  - Rotary encoder for menu navigation
  - Push button for mode switching (Work / TV Mode)
  - Secondary button for quick display wake-up

- **Relay Switching**

  - Server, Monitor, Alexa, FireTV, and Server Power relay control
  - Supports sequential switching with delays (e.g., server boot + monitor on)

- **Home Assistant Integration**

  - Fetches time, device states (light, fan, plugs, relays)
  - Custom HA message support
  - Exposes relays, switches, and sensors to HA

- **IR Remote Support**

  - IR receiver on `GPIO14` with dump enabled

- **Wi-Fi Management**

  - Automatic fallback hotspot if Wi-Fi connection fails
  - Captive portal enabled

---

## 📐 Hardware Used



- **MCU:** Lolin S2 Mini (ESP32-S2)
- **Display:** 0.96" SSD1306 OLED (I²C)
- **LEDs:** WS2812 RGB (3 LEDs)
- **Input Controls:**
  - Rotary encoder (GPIO2, GPIO3)
  - Push button (GPIO7)
  - Secondary button (GPIO5)
- **Relays:**
  - Server (GPIO10)
  - Monitor (GPIO11)
  - Alexa (GPIO12)
  - FireTV (GPIO13)
  - Server Power Switch (GPIO6)
- **Others:**
  - Onboard LED (GPIO15)
  - IR Receiver (GPIO14)

---

## 🖥️ Display Pages

1. **Clock Page** – Large digital clock (12-hour format)
2. **Network Page** – Shows IP address
3. **Device State Page** – Shows states of Light, Fan, Plug, and Relay (from HA)

Custom message mode overrides pages temporarily.

---

## ⚙️ Controls

### 🔘 Power Button (GPIO7)

- **Single Press → Work Mode**
  - Turns **off Alexa**, turns **on Server + Monitor**
  - Server power switch pulsed for boot sequence
- **Double Press → TV Mode**
  - Displays *Switching to TV Mode*
  - Powers **Monitor + FireTV + Alexa**
  - Server power pulsed

### 🔘 Rotary Encoder

- **Clockwise / Anticlockwise:** Switch between display pages
- **Press (GPIO5):** Wakes up display (resets timeout)

---

## 🔄 Scripts

- **reset\_display\_timer** – Keeps display on while interacting, blanks after timeout
- **show\_temp\_message** – Shows a temporary HA/ESP message on OLED for 5s

---

## 📡 Home Assistant Integration

Entities fetched from HA:

- Light state: `light.esphome_bedroom_bathroom_light`
- Fan state: `fan.esphome_bedroom_bedroom_fan`
- Plug state: `light.esphome_bedroom_bedroom_light`
- Relay state: `light.esphome_bedroom_bedroom_night_light`
- OLED message: `input_text.oled_message`

Time source: Home Assistant time service.

---

## 📂 File Structure

```
.
├── deskpanel.yaml   # ESPHome configuration
├── fonts/
│   └── digital-7m.ttf
├── ARIAL.TTF        # Font file used
└── images/
    ├── cover.jpg
    └── product.jpg
```

---

## 🚀 Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/<your-username>/deskpanel.git
   cd deskpanel
   ```

2. Flash the ESP32-S2 Mini using ESPHome:

   ```bash
   esphome run deskpanel.yaml
   ```

3. Add ESPHome device to Home Assistant (it will auto-discover).

---

## 📷 Demo / Screenshots

*(Add more photos of your desk panel build and OLED display here)*

---

## 🛠️ To-Do / Improvements

-

---

## 🤝 Contributing

Contributions are welcome! Fork the repo, make your changes, and submit a PR.

---

## 📜 License

This project is open-source under the **MIT License**.

---

## 🔗 Resources

- ESPHome Docs: [https://esphome.io](https://esphome.io)
- ESP32-S2 Mini Pinout: [https://www.wemos.cc/en/latest/s2/s2\_mini.html](https://www.wemos.cc/en/latest/s2/s2_mini.html)
- SSD1306 Display Docs: [https://esphome.io/components/display/ssd1306.html](https://esphome.io/components/display/ssd1306.html)
- Rotary Encoder Docs: [https://esphome.io/components/sensor/rotary\_encoder.html](https://esphome.io/components/sensor/rotary_encoder.html)
- Home Assistant: [https://www.home-assistant.io](https://www.home-assistant.io)

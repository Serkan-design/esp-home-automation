# 🏠 ESP32 Home Automation System (Siri + Home Assistant + Cloudflare)

Control your home devices using ESP32 with full Siri voice integration via Home Assistant.
This system is self-hosted on a Linux server and securely exposed using Cloudflare.

---

## 🚀 Features

* 🍏 Siri voice control (Apple Home)
* ⚡ Real-time device control via ESP32
* 🔐 Encrypted communication (ESPHome API)
* 🌐 Remote access via Cloudflare Tunnel
* 🖥️ Self-hosted Home Assistant (Docker)
* 📡 Local-first architecture (no dependency on cloud services)

---

## 🧰 Hardware

* ESP32
* Relay module
* Light / Lamp
* WiFi network

---

## ⚙️ Software Stack

* ESPHome
* Home Assistant (Docker)
* Apple Home (HomeKit)
* Ubuntu Server
* Cloudflare Tunnel

---

## 🧠 System Architecture

ESP32 → WiFi → Home Assistant (Docker) → Cloudflare Tunnel → Apple Home (Siri)

---

## 🔌 1. ESP32 Setup (ESPHome)

Install ESPHome:

```bash
pip install esphome
```

Create config:

```bash
esphome wizard oda-lamba.yaml
```

Example configuration:

```yaml
esphome:
  name: oda-lamba

esp32:
  board: esp32dev

wifi:
  ssid: "YOUR_WIFI"
  password: "YOUR_PASSWORD"

api:
  encryption:
    key: "YOUR_API_KEY"

switch:
  - platform: gpio
    pin: 23
    name: "Room Light"
    inverted: true
```

Flash device:

```bash
esphome run oda-lamba.yaml
```

---

## 🖥️ 2. Home Assistant (Docker on Ubuntu Server)

Install Docker:

```bash
sudo apt update && sudo apt install docker.io -y
```

Run Home Assistant:

```bash
sudo docker run -d \
  --name homeassistant \
  --restart=unless-stopped \
  -p 8123:8123 \
  ghcr.io/home-assistant/home-assistant:stable
```

Access:

```
http://SERVER_IP:8123
```

---

## ☁️ 3. Cloudflare Tunnel (Remote Access)

Install Cloudflared:

```bash
sudo apt install cloudflared -y
```

Login:

```bash
cloudflared tunnel login
```

Create tunnel:

```bash
cloudflared tunnel create homeassistant
```

Route:

```bash
cloudflared tunnel route dns homeassistant yourdomain.com
```

Run:

```bash
cloudflared tunnel run homeassistant
```

---

## 🧠 4. Connect ESP32 to Home Assistant

* Go to **Settings → Devices & Services**
* Add **ESPHome Integration**
* Enter ESP device IP

---

## 🍏 5. Apple Home (Siri Integration)

* Add **HomeKit Bridge** in Home Assistant
* Scan QR code using Apple Home app

Now you can say:

👉 “Hey Siri, turn on the room light”

---

## 📸 Screenshots

### Home Assistant Dashboard

![Home Assistant](./docs/screenshots/home-assistant.png)

### Apple Home App

![Apple Home](./docs/screenshots/apple-home.png)

---

## 🔐 Security Notes

* Do NOT expose ESP devices directly to the internet
* Always use Cloudflare Tunnel instead of port forwarding
* Keep API keys and WiFi credentials private

---

## 💡 Future Improvements

* Multi-room automation
* Sensor integration (temperature, motion)
* Mobile app control panel

---

## 👨‍💻 Author

Developed by Serkan

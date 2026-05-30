# Senhus Connect for Panasonic AC

This guide is for updating Senhus Connect Panasonic AC devices built before June 2026 from older firmware to the current ESPHome firmware.

## Migration Guide

If your device has older firmware, update it over USB using ESPHome Dashboard.

You need:

- ESPHome Dashboard
- A USB cable
- Your Wi-Fi name and password

## Step 1: Add Your Wi-Fi Secrets

In ESPHome Dashboard, open **Secrets** or edit `secrets.yaml`.

Add your Wi-Fi details:

```yaml
wifi_ssid: "Your WiFi Name"
wifi_password: "Your WiFi Password"
```

Example:

```yaml
wifi_ssid: "Home WiFi"
wifi_password: "my-wifi-password"
```

These secrets stay in your own ESPHome installation. They are not uploaded to this GitHub repository.

## Step 2: Create The Device In ESPHome

In ESPHome Dashboard:

1. Click **New Device**.
2. Click **Continue**.
3. Give the device a name.
4. Choose your ESP32 board if ESPHome asks.
5. Open the YAML editor.
6. Replace the generated YAML with the config below.

Basic config:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

### Wireless Install By IP

If the old firmware is already online and supports ESPHome wireless updates, add `use_address` under `wifi`.

Replace `192.168.1.123` with the current IP address of the device.

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  use_address: 192.168.1.123
```

For USB install, do not add `use_address`.

## Step 3: Install The Firmware

1. Click **Install** in ESPHome Dashboard.
2. Choose the install method that matches your config.
3. For USB, connect the device by USB and choose the USB/serial option.
4. For wireless install, choose the wireless option and make sure the target IP address is correct.
5. Wait for the install to finish.
6. Keep the device powered while it connects to Wi-Fi.

This replaces the old firmware with the new GitHub-based ESPHome firmware.

## USB Fallback

If wireless install fails, install over USB instead.

1. Connect the device by USB.
2. Click **Install** in ESPHome Dashboard.
3. Choose the USB/serial option.
4. Wait for the flash to finish.
5. Keep the device powered while it connects to Wi-Fi.

After the first successful flash, future updates can usually be installed wirelessly from ESPHome Dashboard.

## If The Device Does Not Show Up

If the device was flashed without Wi-Fi credentials, it cannot join your network yet.

Wait about 90 seconds after boot, then look for the `SenhusConnect` Wi-Fi hotspot and enter Wi-Fi credentials through `http://192.168.4.1`.

The firmware also supports Improv over USB serial, so compatible ESPHome tools can send Wi-Fi credentials over USB.

## File Overview

| File | Purpose |
| --- | --- |
| `acr-pa.yaml` | Main ESPHome firmware config for Senhus Connect Panasonic AC migration devices. |
| `acr-pa-v2.yaml` | ESPHome firmware config for V2 hardware. |
| `README.md` | Migration instructions and release notes. |

## Release Log

### 2026-05-31

- Updated migration instructions for devices built before June 2026.
- Added USB and wireless-by-IP migration options.
- Added Wi-Fi secrets setup instructions.
- Added file overview.

### 2026-05-30

- Added public ESPHome package configs for Senhus Connect Panasonic AC.
- Added V1 and V2 firmware variants.
- Added ESPHome Dashboard import metadata.
- Added mDNS discovery support.
- Added captive portal and Improv serial provisioning support.

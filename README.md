# Senhus Connect for Panasonic AC

This guide shows how to add a Senhus Connect Panasonic AC device to ESPHome and flash it to an ESP32.

## Choose Your Device Version

There are two hardware versions.

| Version | Use this file | UART pins |
| --- | --- | --- |
| V1 | `acr-pa.yaml` | TX GPIO4, RX GPIO3 |
| V2 | `acr-pa-v2.yaml` | TX GPIO3, RX GPIO4 |

If you are not sure which version you have, check the product label or documentation from Senhus.

## Before You Start

You need:

- ESPHome Dashboard
- An ESP32 connected by USB for the first flash
- Your Wi-Fi name and password
- The correct device version, V1 or V2

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
6. Replace the generated YAML with the config for your device version.

For V1:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

For V2:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa-v2.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

## Step 3: Flash The Device

1. Connect the ESP32 by USB.
2. Click **Install** in ESPHome Dashboard.
3. Choose the USB/serial option.
4. Wait for the flash to finish.
5. Keep the device powered while it connects to Wi-Fi.

After the first successful flash, future updates can usually be installed wirelessly from ESPHome Dashboard.

## Updating From Older Firmware

If your Senhus Connect device already has older ESPHome firmware installed, you can move to this new GitHub-based setup without erasing the device.

### If The Device Is Already In ESPHome Dashboard

1. Open the existing device in ESPHome Dashboard.
2. Open its YAML editor.
3. Replace the old YAML with the matching package config.

For V1:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

For V2:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa-v2.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

4. Click **Install**.
5. Choose **Wirelessly** if ESPHome can reach the device.
6. If wireless install fails, connect the device by USB and install over USB instead.

### If The Device Is Not In ESPHome Dashboard

If the device is online but not listed in ESPHome Dashboard:

1. Create a new device in ESPHome Dashboard.
2. Use the matching V1 or V2 package config from above.
3. Click **Install**.
4. Choose a wireless/manual OTA option if ESPHome can find the device by name or IP.
5. If that does not work, install over USB.

### After Updating

After the new firmware is installed, the device will advertise itself with ESPHome discovery and dashboard import information. Future setup and adoption should be easier from ESPHome Dashboard.

The update keeps the normal ESPHome behavior: Wi-Fi credentials already stored on the device may continue to work, but adding the `wifi` section with `!secret` values is recommended so future flashes include the correct Wi-Fi credentials.

## If The Device Does Not Show Up

If the device was flashed without Wi-Fi credentials, it cannot join your network yet.

Wait about 90 seconds after boot, then look for a Wi-Fi hotspot named:

```text
SenhusConnect
```

Connect to that hotspot and open:

```text
http://192.168.4.1
```

Enter your normal Wi-Fi name and password. After the device joins your Wi-Fi, ESPHome Dashboard should be able to find it.

The firmware also supports Improv over USB serial, so compatible ESPHome tools can send Wi-Fi credentials over USB.

## Changing Wi-Fi Later

Once the device is online, it exposes these configuration controls:

- `WiFi SSID`
- `WiFi Password`
- `Save WiFi Credentials`

Enter the new Wi-Fi name and password, then press **Save WiFi Credentials**. The new credentials are stored on the device and will be used the next time it reconnects or restarts.

## ESPHome Dashboard Discovery

The firmware advertises itself with mDNS and ESPHome dashboard import information. When the device is online on the same network, ESPHome Dashboard can discover it and offer adoption.

If adoption is offered, choose the matching device version:

- V1 uses `acr-pa.yaml`
- V2 uses `acr-pa-v2.yaml`

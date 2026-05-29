# Senhus Connect ESPHome

ESPHome firmware configs for Senhus Connect devices.

## Panasonic AC

- `acr-pa.yaml`: Panasonic AC V1, UART TX on GPIO4 and RX on GPIO3.
- `acr-pa-v2.yaml`: Panasonic AC V2, UART TX on GPIO3 and RX on GPIO4.

Both variants include:

- ESPHome Dashboard adoption through `dashboard_import`
- mDNS discovery
- Captive portal fallback
- Home Assistant/Web Server controls to save new Wi-Fi credentials while the device is still online

Use the file that matches the hardware revision when flashing or adopting the device.

## Add in ESPHome Dashboard

Users do not need to download these YAML files manually. In ESPHome Dashboard, create a new device and replace the generated config with one of these package imports.

For Panasonic AC V1:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

For Panasonic AC V2:

```yaml
packages:
  senhus_pac: github://Senhus-DK/senhus-connect-esphome/acr-pa-v2.yaml@main

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

Then click **Install** and choose USB for the first flash. After the first flash, future updates can usually be installed wirelessly.

If the first flash does not include Wi-Fi credentials, wait about 90 seconds after boot and connect to the `SenhusConnect` Wi-Fi hotspot. Open `http://192.168.4.1` and enter the normal Wi-Fi credentials there.

Already-flashed devices advertise a dashboard import URL, so ESPHome Dashboard can discover them and offer adoption when they are online on the same network. They also support Improv over USB serial for Wi-Fi provisioning.

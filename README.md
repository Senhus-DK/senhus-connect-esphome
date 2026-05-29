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

# Blynk.NCP

**Blynk.NCP** is a solution that off-loads network connectivity to a **Network Co-Processor (NCP)** in a [dual-Microcontroller Unit (MCU)](https://docs.google.com/presentation/d/1aP2sQWB0J9EWj8Y1h5qeyfm2aFwaNSUKnCE-k7zxVnk/present) setup, with the application/business logic residing on the **Primary MCU**.

## When to use Blynk.NCP?

Using Blynk.NCP is recommended if one of these is true:

- You have one of the [supported dual-MCU](#supported-boards) boards and want connect it to Blynk
- You're building a new IoT product with specific requirements for the Primary MCU, so you're adding a separate connectivity module
- You want to build a new product that adds Blynk IoT features on top of your existing product (retrofitting)
- You are looking for a **ridiculously low** risks, integration efforts, and time to market

## Features

- **Blynk.Inject**: connect your devices easily using **Blynk.App** (iOS/Android) or **Blynk.Console** (Web Dashboard)
  - `BLE`-assisted device provisioning for the best end-user experience
  - `WiFiAP`-based provisioning for devices without BLE support
- Secure **Blynk.Cloud** connection that provides simple API for:
  - Data transfer with Virtual Pins, reporting Events, and accessing Metadata
  - Time, Timezone and Location
- Network Manager:
  - WiFi (up to 16 saved networks), Ethernet, Cellular
  - Advanced network connection troubleshooting
- **Blynk.Air** - automatic Over The Air firmware updates using **Blynk.Cloud** GUI and backend
  - Both NCP and MCU firmware updates
  - Local firmware upgrade using **Blynk.App** (during device activation by the end-customer)
- Persistent automations (automation scenarios that work even if the device is offline) - *soon*
  
Additional services that can be provided by the Blynk.NCP:

- Connectivity-related device state indication - requires a monochrome/RGB/addressable LED attached to the NCP
- User button - requires a momentary push button attached to the NCP
- Non-volatile storage for [Preferences](https://github.com/vshymanskyy/Preferences)
- File System storage
- Factory testing and provisioning

## Supported boards

This example project is compatible with a set of ready-to-use Dual-MCU boards:

Board                            |                 | MCU      | NCP         | Connectivity | Provisioning
:--                              | ---             | :---     | :---        | ---          | ---
[Arduino Nano RP2040 Connect][1] | `rp2040connect` | `RP2040` | `NINA-W102` | WiFi 2.4     | BLE
[Arduino Nano 33 IoT][2]         | `nano33iot`     | `SAMD21` | `NINA-W102` | WiFi 2.4     | BLE
[Arduino MKR WiFi 1010][3]       | `mkrwifi1010`   | `SAMD21` | `NINA-W102` | WiFi 2.4     | BLE
[Arduino UNO R4 WiFi][4]         | *soon*          | `RA4M1`  | `ESP32s3`   | WiFi 2.4     | BLE
[Arduino Portenta C33][5]        | *soon*          | `RA4M1`  | `ESP32c3`   | WiFi 2.4     | BLE
[TTGO T-PicoC3][6]               | *soon*          | `RP2040` | `ESP32c3`   | WiFi 2.4     | BLE
[RPi Pico][7] + [ESP8266][8]     | `pico_esp8266`  | `RP2040` | `ESP8266`   | WiFi 2.4     | WiFiAP

## Custom boards

You can also [add one of the supported connectivity modules](docs/BuildYourOwn.md) to your own board.

## Getting started

This is a **PlatformIO** project. We recommend using [**VSCode**][pio_vscode] or [**PIO CLI**][pio_cli].  

Flash the Blynk.NCP firmware:

```sh
pio run -e rp2040connect -t upload_ncp
```

> **Note:** This overwrites both the MCU and the NINA module firmware.  
You can [restore the stock NCP firmware][restore] easily.

Open `src/main.cpp` and fill in [information from your Blynk Template](https://bit.ly/BlynkInject):

```cpp
#define BLYNK_TEMPLATE_ID           "TMPxxxxxx"
#define BLYNK_TEMPLATE_NAME         "MyDevice"
```

Build and flash the example project, run the serial monitor:

```sh
pio run -e rp2040connect -t upload
pio device monitor
```

## Use the **Blynk mobile app** (iOS/Android) to configure your new device

Ensure that the Blynk App is installed on your smartphone and scan this QR code:

<img alt="Add New Device QR" src="./docs/Images/AddNewDeviceQR.png" width="250" />

Alternatively: open the `Blynk App` -> click `Add New Device` -> select `Find Devices Nearby`

## Disclaimer

> The community edition of **Blynk.NCP** is available for personal use and evaluation.  
If you're interested in using **Blynk.NCP** for commercial applications, feel free to [contact Blynk][blynk_sales]. Thank you!


[blynk_sales]: https://blynk.io/en/contact-us-business
[pio_vscode]: https://docs.platformio.org/en/stable/integration/ide/vscode.html#ide-vscode
[pio_cli]: https://docs.platformio.org/en/stable/core/index.html
[restore]: ./docs/RestoreFirmware.md

[1]: https://store.arduino.cc/products/arduino-nano-rp2040-connect
[2]: https://store.arduino.cc/products/arduino-nano-33-iot
[3]: https://store.arduino.cc/products/arduino-mkr-wifi-1010
[4]: https://store-usa.arduino.cc/pages/unor4
[5]: https://www.arduino.cc/pro/hardware-product-portenta-c33
[6]: https://www.lilygo.cc/products/lilygo%C2%AE-t-picoc3-esp32-c3-rp2040-1-14-inch-lcd-st7789v
[7]: https://www.raspberrypi.com/products/raspberry-pi-pico
[8]: https://www.waveshare.com/pico-esp8266.htm

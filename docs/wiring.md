# Wiring

> **Button pins depend on the board.** The tables below include every supported board family. The firmware image for your board already contains the correct pin map.

## Components

| Item | Notes |
| :--- | :--- |
| ESP32 board | WROOM-32, S3, or C3. See the pin table below. |
| 2 momentary buttons | Tactile switches, bar-end clickers, or paddle shifters. |
| USB cable | Data-capable cable for flashing and setup. |
| 5 V supply | USB power is normally sufficient. |

No external resistors are needed: the firmware enables the ESP32's internal pull-ups.

## Button pins

| Board | Shift Up | Shift Down |
| :--- | :--- | :--- |
| ESP32-WROOM-32 / classic DevKit | GPIO 18 | GPIO 5 |
| Waveshare ESP32-S3 Zero | GPIO 4 | GPIO 5 |
| LOLIN C3 Mini | GPIO 7 | GPIO 5 |

Connect one side of each button to the listed GPIO and the other side to `GND`. A press pulls the pin low.

## Onboard status LED

| Board | LED pin | Type |
| :--- | :--- | :--- |
| ESP32-WROOM-32 / DevKit | GPIO 2 | Single colour, active HIGH |
| LOLIN C3 Mini | GPIO 7 | Shares Shift Up; firmware disables this LED |
| Waveshare ESP32-S3 Zero | GPIO 21 (`WS_RGB`) | WS2812 RGB |

LED states:

| State | Single colour | RGB |
| :--- | :--- | :--- |
| No desktop app connected | Slow blink, 900 ms on / 900 ms off | Red slow blink |
| App connected, trainer not connected | Repeated double flash | Blue double flash |
| App and trainer connected | Solid on | Solid green |

The desktop app counts as connected over Wi-Fi TCP, an open native USB CDC session, or recent command traffic on a USB-to-UART bridge. USB power alone does not count. On S3 boards, enable **USB CDC On Boot** if you want USB serial to act as the app connection; otherwise `Serial` uses UART0.

## Quick WROOM wiring

```text
      ESP32-WROOM           Buttons
      +---------+
      | GPIO 18 |-----------[ Shift Up ]----+
      |         |                           |
      | GPIO  5 |-----------[ Shift Down ]--+
      |         |                           |
      |    GND  |---------------------------+---- GND
      +---------+
```

## Board-specific cautions

**WROOM / DevKit v1:** avoid strapping pins GPIO 0, 2, 12, and 15 for buttons. GPIO 4 was unreliable on some boards, so Shift Up stays on GPIO 18.

**S3 boards:** GPIO 4 and GPIO 5 are safe choices. Console traffic is normally on GPIO 43/44.

**C3 boards:** avoid GPIO 2, 8, and 9 (strapping), GPIO 18/19 (USB data), and GPIO 20/21 (UART0). On the LOLIN C3 Mini the onboard LED shares GPIO 7 with Shift Up, so the firmware disables the LED to keep the button working. Use an external LED on a free pin if you need status indication on that board.

## Optional hardware

An SSD1306 128x64 I2C OLED was evaluated but is **not implemented** in official firmware. If added in a future version, the intended connections would be VCC to 3.3 V, GND to GND, SDA to GPIO 21, and SCL to GPIO 22 on WROOM.

An external status LED can be connected on WROOM GPIO 2 through a 330 Ω resistor, anode to GPIO and cathode to GND. Use the LED pin and polarity for your board from the table above on other boards.

## Verification before flashing

1. Check that no bare wires touch adjacent pins or the board shield.
2. With a multimeter, measure each button pin to GND: open circuit when released, near 0 Ω when pressed.
3. After flashing, open a serial monitor at 115200 baud and press each button. Gear change messages should appear. Pressing both within 50 ms should toggle the front ring when 2x front shifting is enabled.

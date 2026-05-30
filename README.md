# Touchless IR Sensor Water Tap
 
Embedded firmware for a contactless water tap built on an ESP32, using an MH-B IR proximity sensor module for hand detection and a relay-switched solenoid valve for water flow control. Developed in Arduino IDE with real-time status monitoring over UART serial.
 
## Hardware used
 
- ESP32 (dual-core, 240 MHz)
- MH-B IR obstacle/proximity sensor module (LM393 comparator, digital output)
- Single-channel relay module
- 12V normally-closed solenoid valve
- Arduino IDE serial monitor (UART, 115200 baud) for debugging
## What it does
 
- MH-B IR sensor continuously checks for hand presence — the onboard LM393 comparator outputs a clean digital LOW when a hand reflects IR back, HIGH when clear
- ESP32 reads the sensor on a GPIO pin and drives the relay accordingly
- Hand detected → relay energises → solenoid valve opens → water flows
- Hand removed → relay de-energises → solenoid closes → water stops
- Valve open/close events printed to serial monitor over UART for real-time debugging
## Key firmware work
 
- GPIO configuration for digital sensor input (INPUT_PULLUP) and relay output on ESP32
- Software debounce logic to prevent relay chatter at the edge of detection range — required consecutive LOW reads before triggering the valve
- Relay timing control to prevent solenoid chatter on marginal detections
- Detection range tuned via the onboard potentiometer to ~5–8 cm for reliable hand detection
## What I learned
 
The MH-B gives a digital output — the comparator does the threshold comparison in hardware, so the firmware just reads HIGH or LOW. The real challenge was making detection reliable across different lighting conditions, since sunlight and fluorescent lights both emit IR and caused false triggers. Combining hardware threshold tuning (potentiometer) with software debouncing solved it. Monitoring valve state over UART helped quickly distinguish whether false triggers were hardware noise or a firmware logic issue.
 
## Tools
 
`ESP32` `Arduino IDE` `Embedded C/C++` `GPIO` `UART` `MH-B IR sensor` `LM393` `Relay control` `Solenoid valve`

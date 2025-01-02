# Programming an ESP-12F (ESP8266) with an ESP32 WROOM

This is my attemp at programming an ESP-12F using ESP32 model (Cause I'm too lazy to buy anything else... and I don't have spare money. *~~So shut up and cry more.~~*

I'm not a professional, so any contribution is wellcome.

This README explains how to program an ESP-12F (ESP8266) Wi-Fi module using an ESP32 WROOM *(30-pin)* development board as a USB-to-serial adapter and programmer. This method is useful when you don't have a dedicated USB-to-serial converter for the ESP8266.

## Prerequisites

*   ESP-12F (ESP8266) Wi-Fi module
*   ESP32 WROOM (30-pin) development board
*   Jumper wires
*   Breadboard (recommended)
*   Arduino IDE or PlatformIO (VS Code extension)
*   USB cable for connecting the ESP32 to your computer

## Wiring Diagram

 **1. DURING UPLOAD**

Connect the ESP32 and ESP-12F as follows:
```
ESP32 EN <------> ESP32 GND

ESP32	     ESP-12F

TX0/2 <-------------> TX 
RX0/2 <-------------> RX
GND------------------> GND 
3.3V <--------------------> VCC 
3.3V <--------------------> EN
GND <--(During Upload)--> GPIO0
GPIO15 <--------------------> GND

**(OPTIONAL)**
RST <-------(BUTTON)--------> GND 
```
![image](https://github.com/user-attachments/assets/af29f4ff-1c0f-4714-8169-a5147d299ec2)

**2. DURING RUNNING**
```
GND  <--------------------> GND 
3.3V <--------------------> VCC 
3.3V <--------------------> EN 
```
## Software Setup 
### Arduino IDE 
1. Install the ESP8266 board package in the Arduino IDE: 
* Go to File > Preferences. 
 * Add `http://arduino.esp8266.com/stable/package_esp8266com_index.json` to **"Additional Boards Manager URLs"**. 
* Go to **Tools** > **Board** > **Boards Manager** and install **"esp8266 by ESP8266 Community"**. 
* Select the correct board: **Tools** > **Board** > **NodeMCU 1.0 (ESP-12E Module)** or Generic ESP8266 Module 
2. Select the correct port: Tools > Port > (The port your ESP32 is connected to) 
### PlatformIO (VS Code) 
1. Install the PlatformIO extension in VS Code. 
2. Create a new PlatformIO project.
* Make sure you choose the board to be **ESP 8266 E12F** 
## Uploading the Code 
1. Connect the ESP32 to your computer via USB. 
2. Open your ESP8266 code in the Arduino IDE or PlatformIO. 
3. In the IDE/PIO, start the upload process. 
4. **(DEPENDS) Manual Reset:** If you got stuck at "Uploading stub...". As soon as you see "Uploading stub..." in the console output, briefly connect the RST pin of the ESP-12F to GND (or using your pushbutton in the wiring diagram) and then release it. 
The timing is critical. 
5. If the upload is successful, you'll see a message indicating the upload progress and completion. 
6. Disconnect GPIO0 from GND after the upload. 


## Test
```c
int LED =2;

void  setup() {
pinMode(LED, OUTPUT); 
}

void  loop() {
digitalWrite(LED, LOW); 
delay(1000); 
digitalWrite(LED, HIGH);
delay(1000);
}
```

Upload those code and wait for disaster to come.
## Troubleshooting 
* **"Failed to connect to ESP8266: Timed out waiting for packet header" or "Invalid head of packet":** Double-check all wiring, especially TX/RX and GPIO0. Ensure a stable power supply and practice the manual reset timing. 
* **Invalid head of packet (0x20) Chip is ESP8266 in Secure Download Mode**
Ensure all connections between the ESP32 (programmer) and ESP-12E are correct and secure, especially the crucial TX/RX swap and the GPIO0 connection for bootloader mode.

 * **Other errors:** Consult the error message for specific guidance. Search online forums or communities for solutions. 
 ## Further Resources 
 * [ESP8266 WIKI github](https://github.com/esp8266/esp8266-wiki) 
 * [PlatformIO Documentation](https://docs.platformio.org/) 

* This README provides a guide to programming an ESP-12F using an ESP32. Remember to consult the troubleshooting section if you encounter any problems.




[![CLA assistant](https://cla-assistant.io/readme/badge/meshtastic/Repeater)](https://cla-assistant.io/meshtastic/Repeater)

# Meshtastic-repeater

A simple repeater node firmware for Meshtastic 

LoRa CubeCell nodes by Heltec Automation: https://github.com/HelTecAutomation/ASR650x-Arduino/

## Notes

Intended for use with the platform.io IDE. Depends on the NanoPB Lib and Base64 Lib (see platformio.ini). See the provided platformio.ini for built-in environments. Default is cubecell_board.

> Serial output speed: 115200.

Packets will be repeated only once per packet ID, to prevent flooding.

Keep in mind that re-sending packets will cause the initial sender to assume that the packet is "received" or at least in the mesh.
If no other meshtastic node is in range of either the node or the repeater, the message will still be shown as received.

Will work with most packets meeting the radio settings, but the serial output is based on the assumption that the node receives meshtastic packets.
Minimum size for none-Meshtastic packets is 14 bytes.

> ⚠️ The Repeater is not working for “medium range” setting due to the tight timings. It's best for "very long range" and "long range", but is working for "short range", too.

## Settings

`#define SILENT` to stop serial output.

`#define NOBLINK` to disable red blinking from the RGB LED during the sending of a packet (can be quite long at speed setting 3).

`define NO_OLED` to turn off messages on the OLED. Supported Boards for OLED mode are HTCC-AB02 and HTCC-AB02S (cubecell_board_Plus and cubecell_gps).

### Meshtastic Channel Settings

*Edit the configuration block in `config.h`*

`#define REGION  RegionCode_EU865` 
Defines your region (to EU865). For US, use RegionCode_US, for CN use RegionCode_CN etc. See config.h for more supported regions.

`#define TX_MAX_POWER     14` 
Sets output power to 14 dB. This value will also be used, wenn output power is set to Zero in your RegionCode (0 = max. power). TX_MAX_POWER will be ignored, when higher than RegionCode maximum

`char MeshtasticLink[] = "https://www.meshtastic.org/d/#CgsYAyIBAYABAYgBAQ";`  (Example String for Channel "Default")
Specificy your own Meshtastic channel url.

# WiFi Probe Request Sniff With LED Status

This example starts and stops ESP32 Marauder probe request sniffing with the hardware button and uses the RGB LED for status feedback.

The script enables the ESP32 Marauder `SavePCAP` setting before starting `sniffprobe`, so captured probe requests can be written to the SD card as `probe_N.pcap`.

## Status Indicator

| LED state          | Meaning                                                                                               |
| ------------------ | ----------------------------------------------------------------------------------------------------- |
| Dim amber          | Ready and waiting for the first button press.                                                         |
| Bright amber       | Enabling Marauder PCAP output.                                                                        |
| Dim red            | Stopping any previous Marauder scan before starting a clean probe sniff.                              |
| Pulsing violet     | Probe request sniffing is running. The pulse updates once per loop while no packet activity is shown. |
| Bright green pulse | Probe request activity was reported by `ESP32M_GET_RECV_PACKETS()`. The display also advances a dot.  |
| Red                | Stop request received and the script is stopping the ESP32Marauder scan/sniffing command.             |
| Steady dim green   | Complete and waiting for the final button press before reset.                                         |
| Off                | The device is resetting or the script is not running on hardware with LED support.                    |

## Usage

1. Copy `autorun.ds` onto the SD card.
2. Plug in the device and wait for the dim amber LED.
3. Short press the hardware button to start probe request sniffing.
4. Long press (until the red light) the hardware button to stop capture.
5. Short press the hardware button once more to reset when the LED is steady dim green.

## Notes

The Marauder `sniffprobe` command starts the Probe Request Sniff function. The local Marauder wiki documents the GUI workflow in `ESP32Marauder.wiki/Probe-Request-Sniff.md`; this USB Army Knife firmware tree exposes the matching CLI command as `sniffprobe` in `lib/ESP32Marauder/esp32_marauder/CommandLine.h`.

Do not add blank lines to the script or keep them CRLF terminated (Windows default). This firmware's bundled DuckyScript parser treats an empty LF terminated raw line as end-of-file, so a blank line edited on Linux stops the script.

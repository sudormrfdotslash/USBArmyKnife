# WiFi Deauth And Crypto Capture With LED Status

This variant keeps the original screen prompts and adds LED status feedback for devices that have an RGB LED.

The script also enables the ESP32 Marauder `SavePCAP` setting before scanning so EAPOL/PMKID captures can be written to the SD card as `eapol_N.pcap`.

## Status Indicator

| LED state              | Meaning                                                                                                         |
| ---------------------- | --------------------------------------------------------------------------------------------------------------- |
| Dim amber              | Ready and waiting for the first button press.                                                                   |
| Bright amber           | Enabling PCAP output.                                                                                           |
| Blinking amber         | Scanning for access points. The scan phase still lasts 20 seconds.                                              |
| Brief green after scan | AP scan completed and the script is moving into deauth/sniff mode.                                              |
| Pulsing blue           | Deauth/sniff mode is running. The pulse updates once per loop while no packet activity is reported.             |
| Bright green pulse     | Packet activity was reported by `ESP32M_GET_RECV_PACKETS()`. The display also advances the packet activity dot. |
| Red                    | Stop request received and the script is stopping the ESP32Marauder scan/sniffing command.                       |
| Steady dim green       | Complete and waiting for the final button press before reset.                                                   |
| Off                    | The device is resetting or the script is not running on hardware with LED support.                              |

## notes

Do not add blank lines to the script or keep them CRLF terminated (Windows default). This firmware's bundled DuckyScript parser treats an empty LF terminated raw line as end-of-file, so a blank line edited on Linux stops the script.

## Capture Files

The ESP32 Marauder `sniffpmkid` command displays PMKID/EAPOL frames as they are captured. On this firmware tree, PCAP writing is controlled by the Marauder `SavePCAP` setting. This script enables that setting and the EAPOL scan path opens files named `eapol_0.pcap`, `eapol_1.pcap`, and so on.

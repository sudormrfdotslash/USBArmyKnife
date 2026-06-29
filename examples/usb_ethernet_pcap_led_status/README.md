# Example - PCAP USB Ethernet Traffic With LED Status

This variant keeps the original USB Ethernet/NCM PCAP capture behavior and adds LED status feedback for devices that have an RGB LED.

## Status Indicator

| LED state        | Meaning                                                |
| ---------------- | ------------------------------------------------------ |
| Bright amber     | The script is changing `usbDeviceType` to NCM.         |
| Off              | The device is resetting after the USB mode change.     |
| Bright blue      | USB NCM PCAP capture is starting.                      |
| Pulsing blue     | PCAP capture is running. Each pulse is one second.     |
| Red              | PCAP capture is stopping.                              |
| Steady dim green | Capture complete. The PCAP is written to the SD card.  |

## Set up

1. Copy `autorun.ds` onto the SD card.
2. Plug in the device. If needed, the script changes the USB mode to USB Ethernet/NCM and resets the device.
3. After the reset, unplug and plug the device in again to run the capture.

## Usage

1. Wait until the LED turns steady dim green and the screen shows `PCAP Stopped`.
2. View the SD card. You should see a file called `usbncm_0.pcap`.

## Notes

Do not add blank lines to the script or keep them CRLF terminated (Windows default). This firmware's bundled DuckyScript parser treats an empty LF terminated raw line as end-of-file, so a blank line edited on Linux stops the script.

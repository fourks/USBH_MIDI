# USBH_MIDI v0.3.1

USB-MIDI class driver for Arduino [USB Host Shield 2.0 Library][UHS2]

USBH_MIDI is USB-MIDI class driver for Arduino USB Host Shield 2.0 Library.  
USBH_MIDI is included in [USB Host Shield 2.0 Library][UHS2]. You don't need install separatery.

Project site is [here][GHP].

### for single device
> File->Examples->USBH_MIDI->USB_MIDI_converter

### for multiple device (with USB hub)
> File->Examples->USBH_MIDI->USB_MIDI_converter_multi

### for bidirectional conversion
> File->Examples->USBH_MIDI->bidrectional_converter

## API

- `uint8_t RecvData(uint8_t *outBuf)`
  Receive MIDI message (3 bytes)  
  return value is MIDI message length(0-3)

- `uint8_t RecvData(uint16_t *bytes_rcvd, uint8_t *dataptr)`
  Receive raw USB-MIDI Event Packets (each 4 bytes, upto 64 bytes)  
  `dataptr` must allocate 64bytes buffer.  
  return value is 0:Success, non-zero:Error(MAX3421E HRSLT) and bytes_rcvd is received USB packet length.  
  note: USB packet length is not necessarily the length of the MIDI message.

- `uint8_t SendData(uint8_t *dataptr, uint8_t nCable=0)`
  Send MIDI message. You can set CableNumber(default=0).  
  return value is 0:Success, non-zero:Error(MAX3421E HRSLT)

- `uint8_t SendRawData(uint16_t bytes_send, uint8_t *dataptr)`
  Send raw data. You can send any data to MIDI. (no compliant USB-MIDI event packet)  
  return value is 0:Success, non-zero:Error(MAX3421E HRSLT)

- `uint8_t SendSysEx(uint8_t *dataptr, unsigned int datasize, uint8_t nCable=0)`
  Send SysEx MIDI message. You can set CableNumber(default=0).  
  return value is 0:Success, non-zero:Error(MAX3421E HRSLT)  
  note: You must set first byte:0xf0 and last byte:0xf7

## ChangeLog
2016.04.26 (0.3.1)
* Change the type of the variables from byte to uint8_t.

2016.04.24 (0.3.0)
* Limited support for System Exclusive message on bidirectional_converter example.
* Add MidiSysEx Class for System Exclusive packet data management.

2016.04.09 (0.2.2)
* Improve SysExSend() performance.
* Add SendRawData()
* Update debug messages

2016.03.21 (0.2.1)
* Join the USB Host Shield 2.0 Library.
* Adjust indentation

2015.09.06 (0.2.0)
* Compatible with USB Host Shield 2.0 Library 1.0.0 or lator.
* Compatible with Arduino IDE 1.6.0 or lator.
* Fix for less than 64 bytes USB packet devices
* SysEx message was broken since felis/USB_Host_Shield_2.0@45df706

2014.07.06 (0.1.0)
* Merge IOP_ArduinoMIDI branch into master
* Change class name to USBH_MIDI
* Rename the function RcvData to RecvData (Old name is still available)
* Fix examples for Arduino MIDI Library 4.2 compatibility
* Add SendSysEx()
* Add new example (eVY1_sample)

2014.03.23
* Fix examples for Arduino MIDI Library 4.0 compatibility and Leonardo

2013.12.20
* Fix multiple MIDI message problem.
* Add new example (USBH_MIDI_dump)

2013.11.05
* Removed all unnecessary includes. (latest UHS2 compatibility)
* Rename all example extensions to .ino

2013.08.28
* Fix MIDI Channel issue.

2013.08.18  
* RcvData() Return type is changed to uint8_t.
* Fix examples.

2012.06.22  
* Support MIDI out and loosen device check

2012.04.21  
* First release


## License

Copyright &copy; 2012-2015 Yuuichi Akagawa

Licensed under the [GNU General Public License v2.0][GPL2]

[GPL2]: http://www.gnu.org/licenses/gpl2.html
[wiki]: https://github.com/YuuichiAkagawa/USBH_MIDI/wiki
[UHS2]: https://github.com/felis/USB_Host_Shield_2.0
[GHP]: http://yuuichiakagawa.github.io/USBH_MIDI/

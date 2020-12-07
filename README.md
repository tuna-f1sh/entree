![Canape logo](./img/Canapé_Silk.png)

# Canapé USB-C CAN Interface

Canapé - gets CAN the party started!

The Canapé is a USB-C CAN interface. It is a variant of the open source [candleLight](https://github.com/HubertD/candleLight) platform and its many spawns. Not only does it add USB-C, it brings new features and USB-PD for powering devices under test.

## Features

* Compatiable with:
    * gs_usb firmware [candleLight_fw](https://github.com/candle-usb/candleLight_fw); Linux mainline native support.
    * [PCAN cantact](https://github.com/moonglow/pcan_cantact); (Windows) PCAN software support.
    * [slcan cantact](https://github.com/normaldotcom/cantact-fw); Linux CAN over USART/CDC.
* USB-C connection for use with modern hardware.
* USB-PD negotiation for powering devices rather than using USB communication interface. Up-to 20 V/1 A can be requested and supplied to a device.
* Switched control of 120 Ω termination resistor.
* Switched control of DFU mode and TagConnect 6-pin ISP for use as a development tool.
* USB-PD profile and device setup using switched internal CAN IDs.
* USART test points for SLCAN without USB.
* Two signal connector choices.
* Small form factor: 55 x 18.5 mm.
* Silkscreen art 🎨!

# Usage

## Hardware Connection

The primary CAN connection is a [Molex Picoblade _53261-0471_](https://www.digikey.ch/products/en?keywords=WM7622CT-ND).

The connector was selected because they are commonly used on Drones and so Picoblade to 0.1" header cables can also be easily obtained:

* [1 Bit Sqaured Black Magic 0.1" female cable](https://1bitsquared.com/products/black-magic-01in-pin-header-serial-cable).
* [Pixhawk/PX4/APM to 0.1" female cable](https://www.aliexpress.com/item/32705569941.html?spm=a2g0o.detail.0.0.43ec1ae2et4g6z&gps-id=pcDetailBottomMoreThisSeller&scm=1007.13339.169870.0&scm_id=1007.13339.169870.0&scm-url=1007.13339.169870.0&pvid=21c4d945-32e3-41ea-9cdc-e7fb39809427&_t=gps-id:pcDetailBottomMoreThisSeller,scm-url:1007.13339.169870.0,pvid:21c4d945-32e3-41ea-9cdc-e7fb39809427,tpp_buckets:668%230%23131923%2399_668%23808%233772%23408_668%23888%233325%2319_668%232846%238107%2321_668%232717%237561%23332_668%231000022185%231000066059%230_668%233468%2315615%23624)

Alternatively, one can obtain [pre-crimped female cable assemblies _15134-0402_](https://www.digikey.ch/product-detail/en/molex/0151340402/WM15258-ND/6198148) or [female 4-pin housing _51021-04_](https://www.digikey.ch/product-detail/en/molex/0510210400/WM1722-ND/242844) for custom cabling.

A secondary unfitted [_JST SM04B_](https://www.digikey.ch/products/en?keywords=455-1804-1-ND) (otherwise known as Qwiic/STEMMA) footprint is available on the bottom of the board if one wishes to use those [commonly available cables](https://www.adafruit.com/category/619) instead. JST pre-crimped part is _A04SR04SR30K152A_.

### Wiring Example

Below is a wiring example showing the Canapé Picoblade and JST pinout. A Black Magic 0.1" female header cable is connected to the Picoblade and standard STEMMA QT connected to the secondary JST header. **Note both cable colouring is non-standard due to optimal board layout**.

![Canape wiring diagram](./img/canape.png)

## Software

TODO

## DIP Switches

TODO

## USB Power Delivery (USB-PD)

TODO

## Firmware

TODO

# Credits

The open source CAN community is large and this project adds to that in the true spirit of open source. The [canable](canable.io) devices (of which I have many!) started me on my journey into CAN hardware and software development. Canapé fixes areas I felt could be improved upon and brought up-to date.

Please find links below to projects that have supported the development of the open source CAN ecosystem.

* [canable.io](canable.io)
* [CANtact](https://wiki.linklayer.com/index.php/CANtact)
* [candleLight](https://github.com/HubertD/candleLight)
* [candleLight_fw](https://github.com/candle-usb/candleLight_fw)
* [SocketCAN user space utilities](https://github.com/linux-can/can-utils)
* [Linux slcan module](https://github.com/torvalds/linux/blob/master/drivers/net/can/slcan.c)
* [Linux gs_usb module](https://github.com/torvalds/linux/blob/master/drivers/net/can/usb/gs_usb.c)
* [python-can Python module](https://python-can.readthedocs.io/en/master/)

Should get you started down the rabbit hole!

---

[JBR Engineering Research Ltd](https://jbrengineering.co.uk)

![Canape logo](./img/canape_logo.png)

# Canapé USB-C CAN Interface

Canapé - gets CAN the party started!

The Canapé is a USB-C CAN interface. It is a variant of the open source [candleLight](https://github.com/HubertD/candleLight) platform and its many spawns. Not only does it add USB-C, it brings new features and CAN/USB controlled USB-PD for powering devices under test.

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

# Purchase

An initial production assembly should be ready by the end of Janurary. I will sell them on Tindie and the [JBR Engineering shop](https://shop.jbrengineering.co.uk).

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

A [Vagrant](https://www.vagrantup.com/) virtual machine environment is provided in the ./linux-vm folder for those on non-Linux hosts or who want a pre-configured environment. Install Vagrant and VirtualBox and then setup the machine from within the ./linux-vm folder with the `vagrant up` command.

### Linux SocketCAN

Canapé comes with _candleLight_ firmware which is intended for use with a Linux host. Most Linux distributions include the gs_usb driver and can kernel modules by default so getting started is very easy.

#### Create CAN network interface [[ref]](https://elinux.org/Bringing_CAN_interface_up)

```
sudo ip link set can0 type can bitrate BIT_RATE # where BIT_RATE is the CAN bus speed in b/s
sudo ip link set up can0
```

#### CLI

Install `can-utils` using one's package manager and then various command line tools are available.

```
cansend can0 999#DEADBEEF   # Send a frame to 0x999 with payload 0xdeadbeef
candump can0                # Show all traffic received by can0
canbusload can0 500000      # Calculate bus loading percentage on can0
cansniffer can0             # Display top-style view of can traffic
cangen can0 -D 11223344DEADBEEF -L 8    # Generate fixed-data CAN messages
```

See the [can-utils README](https://github.com/linux-can/can-utils/blob/master/README.md) for more.

#### Cangaroo GUI

The Cangaroo GUI can be compiled for Linux hosts. See [Cangaroo](https://github.com/normaldotcom/cangaroo/).

### Windows

To use the default _candleLight_ firmware on Windows, one can use [Cangaroo](https://github.com/normaldotcom/cangaroo/): [Pre-compiled Win32 binary](https://www.dropbox.com/s/dyh9gvt572v8nhn/cangaroo-win32-0363ce7.zip?dl=0).

The _PCAN_cantact_ firmware can be used with the [PCAN software suit](https://www.peak-system.com/Software.68.0.html?&L=1) and [Python](#python) modules.

Alternatively, to use [SocketCAN](#linux-socketcan) one can use the pre-configured virtual machine explained at the start of the [Software section](#software).

### Python

The [python-can](https://python-can.readthedocs.io/en/master/#) module supports _SocketCAN_ (candleLight), _slcan_ and _PCAN_ devices so options for all hosts are covered - see the [configuration page](https://python-can.readthedocs.io/en/master/configuration.html).

Paired with the [cantools](https://pypi.org/project/cantools/) module, one has access to powerful CLI tools and scripting for CAN bus operations including use with database definition files.

Both modules are pre-installed in the Vagrant virtual machine.

## DIP Switches

The 4 bit DIP switch sets unique runtime settings when in the 'ON' position; for normal usage as a CAN bus probe these would be 'OFF'.

| Switch | Decimal | Set Action                                                    |
|--------|---------|---------------------------------------------------------------|
| 1      | 1       | Force bootloader for DFU.                                     |
| 2      | 2       | Enable Canapé internal configuration CAN IDs.                 |
| 3      | 4       | Enable VBUS -> VBS always not just when USB-PD profile valid. |
| 4      | 8       | Enable 120 ohm CAN_H/CAN_L termination resistor               |

**NOTE** both DFU and 'Enable VBUS' will require power cycling the device for the change to be reflected.

## USB Power Delivery (USB-PD)

The on-board USB-C controller (STUSB4500) is configured for 5 V / 1A power delivery by default (PDO 2). One can configure the controller using the below CAN bus commands when using the [**candleLight_fw**](https://github.com/tuna-f1sh/candleLight_fw) fork and with the [internal CAN IDs switch](#dip-switches) set.

These commands are scrapped from the recieved gs_usb Tx commands and will not be forwarded to the CAN bus when the switch is set. Ensure the DLC is 8 bytes, the ID is correct and byte seven is the Canapé key '0xAF'.

The commands are also scrapped from the `can_recieved` callback but for this to work a USB connection must be enumerated and CAN bus setup in order for the CAN perphieral to be enabled with the correct bit-timing. In the future I may save the previous bit-timing to flash in order to enable this without USB connection.


| ID    | Cmd          | 0    | 1          | 2          | 3         | 4         | 5         | 6         | 7    | Action                                                                  |
|-------|--------------|------|------------|------------|-----------|-----------|-----------|-----------|------|-------------------------------------------------------------------------|
| 0x010 | VBUS EN      | 0x01 | NVM (bool) | SET (bool) | 0x00      | 0x00      | 0x00      | 0x00      | 0xAF | Set VBUS always enable (NVM) or try to enable VBUS by setting profile 1 |
| 0x010 | Set PDO      | 0x02 | NVM (bool) | PROFILE    | VOLTAGE_L | VOLTAGE_H | CURRENT_L | CURRENT_H | 0xAF | Set power delivery profile number (1-3) voltage (mV) and current (mA)   |
| 0x010 | Set Profiles | 0x03 | NVM (bool) | PROFILES   | 0x00      | 0x00      | 0x00      | 0x00      | 0xAF | Set number of profile in use (1-3)                                      |
| 0x010 | Set VBUS     | 0x04 | VOLTAGE_L  | VOLTAGE_H  | 0x00      | 0x00      | 0x00      | 0x00      | 0xAF | Request voltage on VBUS (volatile)                                      |
| 0x010 | Get RDO      | 0x05 | 0x00       | 0x00       | 0x00      | 0x00      | 0x00      | 0x00      | 0xAF | Get enumerated profile number                                           |

### Usage Notes

* NVM flag will write to the NVM rather than volatile register. If a write is required, the **STUSB4500 will be soft reset** in order to re-enumerate the USB-PD profiles. The LEDs will flash rapidly 20 times when a NVM flash occurs. The volatile settings will also trigger a soft reset in order to re-enumerate. **A soft reset will mean the CAN network will need re-creating on the host**.
* The NVM VBUS enable is the only concrete way to force VBUS; the volatile method attempts to enumerate a 5 V power delivery profile but this may not work with non-compliant devices.
* When profile 2 is enumerated, the orange 'PD-OK' will illuminate. This can be changed to profile 3 with the solder link on the underside of the board.
* Refer to the [STUSB4500 programming guide](https://www.st.com/resource/en/user_manual/dm00664189-the-stusb4500-software-programing-guide-stmicroelectronics.pdf) for more information.
* **Excerise caution** configuring these and ideally use a USB-PD checker/multimeter to verify your configuration prior to powering a device!

## Firmware

* [**candleLight_fw Canapé fork**](https://github.com/tuna-f1sh/candleLight_fw) - [[BIN DOWNLOAD]](./bin/canape_fw.bin): Default firmware shipping with Canapé. Works with [Linux SocketCAN](#linux-socketcan) and the [Cangaroo](#cangaroo-gui) GUI. Includes support for configuration of the on-board STUSB4500 USB-C controller and DFU without setting DIP switch.
* [**PCAN CANtact**](https://github.com/tuna-f1sh/pcan_cantact/tree/hsi48) - [[BIN DOWNLOAD]](./bin/pcan_canape_hw.bin): Open source PCAN compatible firmware; works like a PCAN USB adaptor with the PCAN software suite and python-can module. Does not include USB-PD configuration or DFU.
* [**cantact_slcan**](https://github.com/normaldotcom/cantact-fw): slcand is a USART CAN daemon for Linux, which emulates a CAN network socket over USART. The pre-cursor of the candleLight_fw and gs_usb driver, it offers no real advantage since it is still over USB as a CDC. I've found it to drop frames at common bus rates and so do not recommend it. USART pins are exposed however if one wishes to play with slcan over physical USART. A virtual network interface can be created: `sudo slcand -o -s8 -t hw -S 3000000 /dev/ttyS0` and then used like a [SocketCAN](#linux-socketcan) interface.

### Update

Enable the DFU [DIP switch](#dip-switches) and then issue the following command with [`dfu-util`](http://dfu-util.sourceforge.net/):

```
sudo dfu-util -d 0483:df11 -c 1 -i 0 -a 0 -s 0x08000000 -D $FIRMWARE_FILE.bin
```

Where `$FIRMWARE_FILE.bin` is the firmware file to be updated. Binaires are stored in the './bin' folder of this repository, so to flash:

```
sudo dfu-util -d 0483:df11 -c 1 -i 0 -a 0 -s 0x08000000 -D ./bin/canape_fw.bin # candleLight_fw
sudo dfu-util -d 0483:df11 -c 1 -i 0 -a 0 -s 0x08000000 -D ./bin/pcan_canape_hw.bin # pcan_cantact
```

There is also a [Web DFU tool](https://devanlai.github.io/webdfu/dfu-util/), which does not require `dfu-util`. The only requirement is the Chrome browser. Use these settings:

* Vendor ID: **0x0483**
* Transfer Size: **2048**

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

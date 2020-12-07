# CAN Connection

The primary CAN connection is a [Molex Picoblade 53261-0471](https://www.digikey.ch/products/en?keywords=WM7622CT-ND).

The connector was selected because they are commonly used on Drones and so Picoblade to 0.1" header cables can also be easily obtained:

* [1 Bit Sqaured Black Magic 0.1" female cable](https://1bitsquared.com/products/black-magic-01in-pin-header-serial-cable).
* [Pixhawk/PX4/APM to 0.1" female cable](https://www.aliexpress.com/item/32705569941.html?spm=a2g0o.detail.0.0.43ec1ae2et4g6z&gps-id=pcDetailBottomMoreThisSeller&scm=1007.13339.169870.0&scm_id=1007.13339.169870.0&scm-url=1007.13339.169870.0&pvid=21c4d945-32e3-41ea-9cdc-e7fb39809427&_t=gps-id:pcDetailBottomMoreThisSeller,scm-url:1007.13339.169870.0,pvid:21c4d945-32e3-41ea-9cdc-e7fb39809427,tpp_buckets:668%230%23131923%2399_668%23808%233772%23408_668%23888%233325%2319_668%232846%238107%2321_668%232717%237561%23332_668%231000022185%231000066059%230_668%233468%2315615%23624)

Alternatively, one can obtain [pre-crimped female cable assemblies 15134-0402](https://www.digikey.ch/product-detail/en/molex/0151340402/WM15258-ND/6198148) or [female 4-pin housing 51021-04](https://www.digikey.ch/product-detail/en/molex/0510210400/WM1722-ND/242844) for custom cabling.

A secondary un-fitted [JST SM04B](https://www.digikey.ch/products/en?keywords=455-1804-1-ND) (otherwise known as Qwiic/STEMMA) footprint is available on the bottom of the board if one wishes to use those [commonly available cables](https://www.adafruit.com/category/619) instead (JST pre-crimped part is A04SR04SR30K152A).

## Wiring Example

Below is a wiring example showing the Canape Picoblade and JST pinout. A Black Magic 0.1" female header cable is connected to the Picoblade and standard STEMMA QT connected to the secondary JST header. **Note both cable colouring is non-standard due to optimal board layout**.

![Canape wiring diagram](./exports/canape.png)

# Tinsel cheer

This was a quick hack to bring some CheerLights colour into our "website HQ" in the final days of long website replacement project.

## Hardware

I used whatever was available at the time which happened to be a [Particle Photon](https://store.particle.io/collections/photon) and a string of 50 WS2801 RGB LEDs encased in 12mm diffused packages. I don't remember where the LEDs came from but you can get similar ones from [Adafruit](https://www.adafruit.com/products/322), [4Tronix](http://4tronix.co.uk/store/index.php?rt=product/product&product_id=214), [AliExpress](http://www.aliexpress.com/item/50pcs-12mm-IP65-Waterproof-WS2801-RGB-LED-Pixels-Modules-with-WS2801-IC-Addressable-Color/663520530.html), etc.

If I was to buy components to build this I'd get some WS2811/WS2812/WS2812B based LEDs as they require one less pin, have smaller interconnecting wires and are easier to drive.

Connections are as follows:

Photon pin | LED String
-----------|-----------
A3         | Data
A5         | Clock
Vin        | +Ve
Gnd        | -Ve

There's a large capacitor between Vin and Gnd to prevent and large current inrush from damaging the LEDs, i think it was a 2200uF 6.3v electrolytic.

**_Do not_ try and power the Photon and LEDs from USB, the power requirements for all LEDs is something in the order of 3-4Amps!** LED strings like these tend to have power connections at both ends so you can connect the Photon at one end (the end with Data In) and a suitably rated 5v power supply at the other end to power both the LED string and Photon from the same supply.

## Software

Getting a reliable WS2801 driver that compiles in Particle's Web IDE was a challenge. A [gist from technobly on github](https://gist.github.com/technobly/8339548) did the trick and was modified to add the ThingSpeak library to talk to github and "walk" the latest colour down the string of 50 LEDs.

There is an additional "colour" supported by this code called `xmas` which changes the LED string colours into alternating red, green, blue and yellow to resemble a classic set of Christmas lights.
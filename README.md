# MyMultisensors

This is a simple, cheap and low power sensor which can be used, for example, with your favorite battery powered node, for counting power meters blinking led pulses. 

I've decided to not use the well known LM393 module with photodiode because the combo has some power consumption (0.4mA for the comparator only + rest of the circuit, even if no pulses). 

I also thought there is not always the possibility to have an external power supply, when power counters are outdoor for instance.
But sure, the advantage to use a comparator is we get a nice digital voltage level for the signal to the node.

So I got the idea to use a mosfet with a photoresistor and just a few resistors, which i think should be enough :) 

Lot of docs about photoresistors on the internet, but quickly, the photoresistor operation is very simple, and allow us to be low power though: 
- In darkness, in datasheet you can see it's rated for 200k to >1M, in practice, in darkness (i've checked mine), it's in >1Mohms range.
- In light conditions, it falls to 20k for instance.

And i've used it like this :
- the P-mosfet is enabled when the photoresistor is pulled down, detecting a pulse (remember approx 20k, depends on the light intensity). The Source pin of the mosfet being VCC , this is what we get on its Drain pin which is also the Led indicator and Signal pin of the module
- when there is no pulses, the photores is >1M, and we get "1" logic level to the gate of the P-mosfet. So, nothing on signal pin.

The pros:
- the way the mosfet is connected allows a good reliable voltage level for the PULSE signal pin 
- we can also expect a good voltage range of operation, for battery powered device this may be useful
- the resistors combined with the photoresistor consumes just a very few uA depending on their values

I've quickly tested it with a signal generator and was able to detect up to 100Hz. Which should be enough for lot of power meters i think..
An example, for 50Hz frequency blinking led :
- 50 pulses/sec so 50*3600 pulses/hour gives us 180000 pulses/hour
- says at this rate, you're consuming 20kw/h, wow! Then we would get 9000 pulses/kw on the power meter side..

I've done two pcb versions that you can order here in case you want to play with it:
- SMD for those like me who're fond of this.. : https://PCBs.io/share/z5bXQ
- Through hole for those who are thinking i'm boring with my SMD : https://PCBs.io/share/zvVP1


SMD version :

<img src="https://raw.githubusercontent.com/scalz/MyPulseSensor/master/Img/pulse_sensor.png" alt="pulse sensor smd"> 

Through hole version :

<img src="https://raw.githubusercontent.com/scalz/MyPulseSensor/master/Img/MyMultisensors_bottom.jpg" alt="pulse sensor through hole"> 

PCB :
<img src="https://raw.githubusercontent.com/scalz/MyPulseSensor/master/Img/v1_parts.jpg" alt="pulse sensor pcb"> 

Assembled, Top led view :
<img src="https://raw.githubusercontent.com/scalz/MyPulseSensor/master/Img/v1_assembled_ledindicator_view.jpg" alt="pulse sensor top view">

Assembled, Bottom photoresistor view :
<img src="https://raw.githubusercontent.com/scalz/MyPulseSensor/master/Img/v1_assembled_photores_view.jpg" alt="pulse sensor bottom view">

###General specs
------

<img src="https://raw.githubusercontent.com/scalz/MyPulseSensor/master/Img/schematic.png" alt="schematic"> 

|Specs|  |
|---|---|---|
| PCB Size | diam. 18mm |


|Pinout|  |
|---|---|---|
| VCC | Connect to VCC of your board|
| GND |  Connect to GND|
| PULSE | Connect to an IRQ pin on your board|
| SMD Jumper | Shunt the jumper by soldering, if you need the led indicator (will use a bit more power, tweak the resistor|


To use the board, that's easy:
- Follow the above pinout
- If you add the optional onboard led, that will consumes more power of course. Tweak its resistor, or you can disable it thx to the jumper.
- Of course, you need the sensor well aligned in front of the blinking led. The main goal is to have a good dark/light detection.

I don't really need it, or maybe in future, because where I live there are others alternatives like a grid protocol providing lots of informations, but that was quick and fun to do!

Enjoy :)


###Known issues
------ 


###Donations
------

I'm trying to make opensource projects. I do this for free and sharing spirit. I don't do ads etc..
But if you think information here is worth of some money, or want to reward me, feel free to send any amount through paypal.

[![](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=PWVDL2P64FDVU)  

Or you can also order pcb here :
I will earn a little percentage that will allow me to order proto pcb and share more fun design.

Or pay me a protein smoothie if you see me! oh well, a beer is ok too :)

### Contributors
------
Always special thanks to:
- Mysensors Team for its great work

###Links, reference and license
------
- https://www.openhardware.io/view/352/MyPulse-Sensor


Copyright Scalz (2017). released under the CERN Open Hardware Licence v1.2

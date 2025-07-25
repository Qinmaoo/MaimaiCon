# MaimaiCon - V1
DIY Full-size Maimai controller

## Disclaimer
This is my first ever DIY project, i'm well aware that many aspects can be made even better.
This is also only a first version of the project, I'm planning on building a second one which will fix some issues.

## Credits
Huge thanks to @whowechina for the mai-pico firmware and PCB files, without them the project would have been much more of a pain.
Many thanks to Konakwa for the help in discord DM, and being here to answer my (several) questions.
Finally, since this is a grouped project, half the credit goes to Darexell who managed some soldering and hardware aspects.

## Components

### Structure
- Main frame: 1 80x80x2 cm wooden plank, with a 52cm diameter circle cut out in the middle, and a 4mm deep, 58x58cm square engraving on one side. Since engraving isn't the easiest to do, glueing shut 2 separate planks (one with a circular hole, one with a square hole) of appropriate thickness will do the job just fine.
- A ton of wooden cleats for the structure, I used about about 6 1m-long 26x26mm cleats.
- 58x58cm, 5mm thick octogonal glass panel. Square glass works but it's more of a pain to hide the button cables. Since the hole is 58x58, picking a very slightly smaller glass panel (57.9x57.9 for example) might be a good thing to make sure it fits correctly.
- 12mm screws, and some 20mm ones
- A lot of flat angle brackets, and 2 hinges. If you can find 20 degrees brackets, those are more stable than hinges.

### Electronics
- 8x Rabbit buttons, ordered off Taobao. I personally printed the separators, but you can simply buy them from the same seller, depending on your budget.
- 1 pcb and all the related components from whowechina's mai-pico repository. Since we're doing a scaled-up version, the buttons are different, so follow the guide without taking into consideration the mechanical switches and button pcb; however make sure to read the part concerning "optical buttons". (TLDR: some 0603 resistors, one rpi pico, 9 3-pin JSTs, 2 2-pin JSTs, 3 MPR121s, some regular dupont pins and an optional usb-c 16pin port). I haven't looked into making the LEDs work yet, but i figure a random LED strip will do the job just rigt.
- ITO film for the touch zones. I got mine cut by Konakwa since he owns a cutting machine, but you can cut them with scissors by hand I guess? I advise against laser cutting the film, since it melts some parts of the plastic and ends up kinda bad.
- A lot of cables, the longer the better. If you can manage to find very long 3pin/2pin JST cables for the buttons, and very long female dupont cables for the touch, go for it, as it saves the hassle of making them yourself.
- One 43" tv. I ordered mine off amazon, anything works as long as it has decent input lag and is at least 60hz/1080p.

### Tools
- 1~2cm diameter bell drill
- Electric screwdriver
- Cable stripper always helps


## Assembly

### Main wooden frame
There are two main approaches:
- Either find a service to cut a circle, then engrave a square on the solid 2cm thick frame
- If engraving is hard, buy one 5mm thick frame and cut out the entire square in the middle, then buy one 15mm thick frame and cut out the entire circle in the middle, then glue both parts together. This approach is of course more fragile, but it should be alright as long as you let the glue set correctly. This is the approach i used.

Once that's done, mesure out the space for the 8 buttons and screw them on. Drill holes using the bell drill, in such a way that they get covered by the separators (be careful to make them not on top of the glass). The buttons' wires will go through those holes, so none are actually apparent.

(side note: if you have a square panel, the 45° separators will be pretty much in the same spot as the glass, so you can't really drill large holes there. Either make the wires go through the adjacent buttons, or drill holes further away at the cost of overall appearance (though they can get covered by some decoration).

### Glass panel
First step is to glue the ITO film on the backside of the glass panel.

Try to print out the pattern of the touch zones on paper so you can line up the glass correctly. This step is a pain to do since if you mess up, the result will be way uglier. Take it slow and it should be alright!

If everything goes to plan, you should have a circular pattern plus 34 small extrusions on the border of the glass. I would advise removing the protective layer only once everything is in place. 

### Front panel assembly
One both the glass and the main frame are done, you can assemble both! Carefully slide the glass in the square engravement. To secure it, i advise both gluing it (be careful not to put too much weight on the film) and putting some kind of screwed-in structure half on the wood and half on the glass.

### PCB Soldering
!! **Don't forget to short down the <name> pin on the MPR121s** !!
Solder the rpi pico, resistors, usbc port, dupont pins and JST female pins to the board. You can solder the MPR121s on the pcb directly, however I find it better to plug it to the pcb using dupont cables in order to have a cleaner cable management, and also to be more future proof if the component breaks. The "touch" zone should be cleared with nothing soldered to it.

I recommend screwing the PCB on one of the angles of the main frame's backside. The further away the MPR121s are from the TV the better. I screwed mine vertically so the USBc port went out from the side.

### Touch zone wiring
Start putting down the dupont cables on the MPR121s. Since there's a total of 36 MPR electrodes for only 34 zones, leave two electrodes unplugged. I advise grouping every dupont cable coming from the same MPR together, to have a cleaner cable management.

For each zone, measure out the length of the cable (with a small margin to play it safe), shorten the cable to the appropriate length and strip the tip of the cable. Use a multimeter to test each ITO zone from center to extrusion: for some, you might need to make the wire go further along the connector to get a good response.

Using insulating tape, tape every wire to its corresponding extrusion. If you needed to make the wire go further, use regular clear tape to make it stick, and make sure there's no contact with other zones.

### Button wiring
Using long 3pin JST male>male cables, connect the buttons' female jst port to the PCB BT1~8 ports. Do the same for the 2pin service/coin/test/select buttons too if you need to. Make sure to get the wires through the holes you drilled earlier, then cover them up using the separators.

### Firmware config
Since I'm using the V1.1 firmware on V1.0 pcb, I have some small issues regarding the buttons. There shouldn't be any issue if you start the project right now.

The very boring part is remapping every single touch zone on the firmware using the `touch` command on the serial terminal. Once that's done, the electronic part is done!

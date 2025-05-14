# CSL-light-hardware


## I. Objectives 
### LED module operating modes with a pcb plate

#### MODE 1 - Sequence of pulses
The user can define on the computer the frequency and amplitude of a sequence of pulses.


#### MODE 2 - Analog control 
The user can send an analog signal to control the LED. The analog signal can be designed using eg. a signal generator. 

#### MODE 3 - Manual control
The user can set the LED level using a potentiometer.

## II. Usage


### I. Access mode 
- **To access Mode 1**: set interruptor to 1 ("serial" shows up on the screen) and switch the flip to PWM.
- **To access Mode 2**: set interruptor to 1 ("serial" shows up on the screen) and switch the flip to analog.
- **To access Mode 3**: set interruptor to 0 ("manual" shows up on the screen).


### II. Connection 
- Insert the LED jacks into the corresponding holes
- Insert the generator jacks into the corresponding holes
- Insert the jacks to feed the analog signals into the corresponding input holes

<p align="center">
<a> <img src="./Images/final_module.png" width="500"></a>
</p>

### III. Using the LEDControl_interrupt_screen_ascii code

First, open the LEDControl_interrupt_screen_ascii.cpp code in Arduino.ide.
To run the program, you must first have the SSD1306Ascii library installed on Arduino.

[Explains how to control light sources with Arduino and Python, and generate a trigger signal to synchronize a camera](https://github.com/SonyCSLParis/CSL-Lights)


Test the control command: 
- type: #d[3,0,0,1,0,2,0,255]:xxxx.  
  It is a command to generate on and off output on pin 3 or 6.
  The pin stays on for 1 seconds with a period of 2 seconds, at intensity 255. 
  It is later on embeded in a Pyton code for clarity. 
  You should see a character sequence appear. 
- Then type #b[100,0]:xxxx to start the experiment. 
  You should see the LEDs blink (frequency 0.5Hz). 
- To stop the blinking, type #e:xxxx


## III. Manufacture

### I. Kicad

[Kicad Folder](https://github.com/Julie-Mauguit/CSL-light-hardware/tree/main/Kicad%20pcb)

#### A. Complete electronic circuit

Complete Circuit on Kicad : 

<p align="center">
<a> <img src="./Images/Kicad_Complete_Circuit.png" width="1200"></a>
</p>

LED 1 and 2 : 

<p align="center">
<a> <img src="./Images/LED1_LED2.png" width="1200"></a>
</p>


PWM Control : 

<p align="center">
<a> <img src="./Images/PWM_Control.png" width="1200"></a>
</p>


Analog Control : 

<p align="center">
<a> <img src="./Images/Analog_Control.png" width="1200"></a>
</p>

Serial or Manual Mode : 

<p align="center">
<a> <img src="./Images/Serial_Manual.png" width="1200"></a>
</p>

#### B. Component roles
- **Top connectors (J5, J7, J6, J8, J10)** :
  These are screw terminal blocks used to connect LEDs, power, or other peripherals.
- **Relays (RECOM1, RECOM2, etc.)** :
Their role is to adjust the LED light output to prevent damage. They therefore act as power regulators.
- **MOSFETs (BS170)** :
These are used to invert the signal. In fact, the RECOM inverts the input signal, it is inverted a first time before it processes it, in order to obtain the initially desired signal at the output. This can be useful if the LEDs require active low control (they light up when the signal is LOW).
- **Potentiometers (RV1, RV2)** :
These allow for a manual mode to adjust LED intensity via an analog input.
- **Double Switch (SW_DPDT_x2)** :
Two switches are used to select between analog or PWM control for each LED.
- **A Switch On-Off (Jumper_2_Open)** :
It allows switching between Serial and Manual modes.

#### C. Impression

It lasts about 30 minutes.

<p align="center">
<a> <img src="./Images/complete_circuit_pcb.png" width="500"></a>
</p>


### II. Welding

#### A. Shield Arduino
First, you need to solder the branches of the Arduino.

#### B. Components that you solder directly onto the PCB board
- Resistors
- MOSFET transistors
- RECOM
- Terminal blocks
- Vias

#### C. Components that you don't solder directly onto the PCB board
- The 2 potentiometers
- The OLED screen
- The 2 switches
- The on-off switch

<p align="center">
  <strong>After welding</strong><br>
<a> <img src="./Images/after_welding.jpg" width="500"></a>
</p>

#### D. Jack sockets
You have to solder cables with the female jack sockets.

<p align="center">
<a> <img src="./Images/jack_socket.png" width="500"></a>
</p>

For the black and red cables of the male jack, you must solder them to the generator, LED, and signal cables.
Before soldering, prepare some heat-shrink tubing to prevent loose connections.

#### E. List of components

On GOTRRONIC : 

- **RECOM** : (x2)
  - Web link: https://www.gotronic.fr/art-convertisseur-r-78e3-3-0-5-29589.htm
  - Code : 14977
  - Price : 4,6€

- **Switch On-Off**: (x1)
  - Web link : https://www.gotronic.fr/art-inter-secteur-unipolaire-47432.htm
  - Code : 07059
  - Price : 0.90€

- **OLED Screen** : (x1)
  - Web link : https://www.gotronic.fr/art-module-afficheur-oled-0-96-tf052-28511.htm
  - Code : 36038
  - Price : 9,5€

- **Potentiometers** : (x2)
  - Web link : https://www.gotronic.fr/art-potentiometre-logarithmique-10k-937-3000.htm
  - Code : 04519
  - Price : 2,60€

 - **Double switch** : (x2)
    - Web link : https://www.gotronic.fr/art-inverseur-bipolaire-8012b-4181.htm
    - Code : 07014
    - Price : 2,80€
      
- **Resistors 820 ohms** : (x2)
    - Web link : https://www.gotronic.fr/art-resistance-carbone-1w-820-8486-2748.htm
    - Code :  04235
    - Price : 0,10€
      
- **2.5mm pitch terminal block** : (x6)
    - Web link : https://www.gotronic.fr/art-bornier-sc02-2-54-15468.htm
    - Code : 48930
    - Price : 0.80€
      
 - **3.5 mm male jack** : (x6)
    - Web link : https://www.gotronic.fr/art-cordon-jack-vers-fils-denudes-sterf-37803.htm
    - Code : 48239
    - Price : 0,95€
  
 - **3.5mm female socket** : (x6)
     - Web link : https://www.gotronic.fr/art-embase-femelle-cg203-4814.htm
     - Code : 08461
     - Price : 0,50€

 - **Transistor MOSFET BS170** : (x2)
     - Web link : https://www.gotronic.fr/art-transistor-bs170-1569.htm
     - Code : 02440
     - Price : 0.30€

- **Uno Arduino** : (x1)
    - Web link : https://www.gotronic.fr/art-arduino-uno-a000066-12420.htm
    - Code : 25950
    - Price : 23.90€

- **9-pin Arduino connector** : (x3)
    - Web link : https://www.gotronic.fr/art-connecteur-fh1x9-35491.htm
    - Code : 49007
    - Price : 0.80€
      
- **14-pin Arduino connector** : (x1)
    - Web link : https://www.gotronic.fr/art-connecteur-fh1x14-35646.htm
    - Code : 49011
    - Price : 1€
      
- **LED** : (x2)
    - Web link: https://www.gotronic.fr/art-led-5-mm-led5bt-21009.htm
    - Code :  03039
    - Price : 0.30€

### III. Assembly

#### A. Box printing

[Solidworks box](https://github.com/Julie-Mauguit/CSL-light-hardware/tree/main/Solidworks%20bo%C3%AEte)

Printing the box takes approximately 1 hour and 20 minutes.
Printing the box lid takes approximately 30 minutes.
Printing the small panel with the instructions takes approximately 13 minutes.


#### B. Plastic inserts

You will need to make three 3.7mm diameter, 3mm deep plastic inserts with 6mm long M3 screws to secure the Arduino to the enclosure lid. 
Then, make 3mm diameter, 3mm deep plastic inserts with 8mm long M3 screws to close the enclosure.

#### C. Finalization

Screw the components into the box in this order:
- Female jack sockets
- OLED display with 10mm long M2 screws and nuts
- The two switches
- The on-off switch
- The two potentiometers

<p align="center">
  <strong>After assembly</strong><br>
<a> <img src="./Images/after_assembly.jpeg" width="500"></a>
<a> <img src="./Images/after_assembly_1.jpeg" width="500"></a>
</p>

### IV. Code

[Code Arduino/LEDControl_interrupt_screen_ascii](https://github.com/Julie-Mauguit/CSL-light-hardware/tree/main/Code%20Arduino/LEDControl_interrupt_screen_ascii)

The code has been adapted to suit the circuit. 
In this configuration, pins 3 and 6 are used for PWM inputs, while pins A0 and A1 are used for analog inputs.

[Explains how to control light sources with Arduino and Python, and generate a trigger signal to synchronize a camera](https://github.com/SonyCSLParis/CSL-Lights)


### License

Copyright (C) 2025 

Author(s):
Julie Maugit - Polytech Sorbonne
Thierry Legou - CNRS/Aix-Marseille Université
Peter Hanappe - Sony Computer Science Laboratories Paris
Aliénor Lahlou - Sony Computer Science Laboratories Paris

You can redistribute it and/or modify  it under the terms of the GNU General Public License as published by   the Free Software Foundation, either version 3 of the License, or   (at your option) any later version.  This project is distributed in the hope that it will be useful, but  WITHOUT ANY WARRANTY; without even the implied warranty of   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU  General Public License for more details.  You should have received a copy of the GNU General Public License  along with this program.  If not, see  <http://www.gnu.org/licenses/>.

This work was supported by the European Innovation Council Pathfinder Open DREAM (grant no. 101046451)



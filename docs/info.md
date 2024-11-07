<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This design is targetted to be used as
1. Ring oscillator
2. Clock divider 
3. Digitally controlled oscillator
   
1. Ring oscillator
Five inverters are used in chain. By shorting out0 pin to in0 and clk, the design can be configured as a ring oscillator
Frequency = 1/(5*inverter cell delay)

2. Clock divider network
Dff chain is used to introduce clock division.
By using combination between in1, in2, in3 below we can different division at out1
fs - frequency of the clock signal

in1 in2 in3  output frequency (out0)
0   0   0    fs/128
0   0   1    fs/64
0   1   0    fs/32
0   1   1    fs/16
1   0   0    fs/8
1   0   1    fs/4
1   1   0    fs/2

3. Digitally controlled oscillator (DCO)
- Short in0, clk0, out0, we get the ring oscillator. The signal can be tapped at out0
- The clock divider network introduce frequency variations in multiples of 2
- in1 in2 in3 combinations can fork out different frequencies at out0 as below 
 with fr being the frequency of the ring oscillator (free running frequency)

  in1 in2 in3  out0 (output frequency)
   0   0   0    fr/128
   0   0   1    fr/64
   0   1   0    fr/32
   0   1   1    fr/16
   1   0   0    fr/8
   1   0   1    fr/4
   1   1   0    fr/2
   1   1   1    fr
   
## How to test
Pin description
 1. clk - clock input, input the clock signal to this pin if the chip is to be used as a clock divider, out1 is the output of the clock divider. Short it to in0 and out0 if used as a Oscillator
 2. in0 - Short it with clk pin and out0 if used as a ring oscillator
 3. in1 - LSB of the binary input (DCO input or clock divider select)
 4. in2 - second binary input  (DCO input or clock divider select) 
 5. in3 - MSB of the binary input (DCO input or clock divider select )
    
## External hardware
No external hardware required as such

List external hardware used in your project (e.g. PMOD, LED display, etc), if any

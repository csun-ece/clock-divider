# Clock and Sequential logic
**California State University, Northridge**  
**Department of Electrical and Computer Engineering**  

## Objective

After completing this assignment, students will be able to:
- Create clock divider to generate different clock frequencies
- Create structural top level design
- Create regular and priority encoders

## Requirements

- Vivado 2019.1
- Git

## Introduction
This lab is a continuation of lab 3. In this lab we will create a clock divider
to convert the sysclk to slower frequencies. We will also create a structural top
level design to combine all counter created in lab 3 into one design. The top design
will interface to outside by accepting inputs from switches and buttons and feed the
counter outputs into the board LEDs. 

## General requirements:
- Clock divider will convert the sysclk to 1 Hz, 8 Hz and 16 Hz frequencies.
    - The sysclk for Zybo is 125 MHz and for Zedboard is 100 MHz.
- Use button 0 for reset. All counters shall be reset upon press of button 0.
- Use button 1 for pause. Upon pressing the pause button the current value of the counter shall be preserved, but no new value should be shown until the release of the button. 
    - Buttons 1 shall have priority over button 2 and button 3.
- Use button 2 for feeding 8 Hz clock into counters. Buttons 2 shall have 
priority over button 3.
- Use button 3 for feeding 16 Hz clock into counters.
- When all switches are off (e.g "0000") no LED shall be ON.
- When switches are in the "0001" configuration LEDs shall reflect the output of shift right ring counter.
- When switches are in the "0010" configuration LEDs shall reflect the output of shift left ring counter.
- When switches are in the "0100" configuration LEDs shall reflect the output of binary counter.
- When switches are in the "1000" configuration LEDs shall reflect the output of johnson counter.
- The ports in `top.vhd` should map correctly to the XDC constraint file provided here [Zybo-Z7-Master.xdc](./constrs/Zybo-Z7-Master.xdc)

The following is an example of ports matching the XDS I/O names:
``` vhdl
entity top is
    Port ( sysclk : in STD_LOGIC;
           sw : in STD_LOGIC_VECTOR (3 downto 0);
           btn: in STD_LOGIC_VECTOR (3 downto 0);
           led : out STD_LOGIC_VECTOR (3 downto 0));
end top;
```
- Testbench and report utilization after the implementation should be provided in the final report.
- The design must pass all the design flow steps including synthesize, implementation and bit stream generate, 

## Tasks

:point_right: **Task 1**: (35 points)  
Design a clock divider to convert the sysclk to 1 Hz, 8 Hz and 16 Hz frequencies.
It is recommended to use GENERIC option in the clock divider entity such that frequency of the base clock can be configured during the instantiation of the clock divider.
Create a testbench to verify your design. Record your clock divider waveform in the report.

:point_right: **Task 2**: (35 points)  
Create a structural design and name is `top.vhd`. This file should instantiate all the counters created in lab 3 and select each of them based on the selected switch shown in the table below:

| switch config | selected counter         |
|:-------------:|:------------------------:|
| 0000          | None                     |
| 0001          | shift right ring counter |
| 0010          | shift left ring counter  |
| 0100          | binary counter           |
| 1000          | johnson counter          |

When no button is pressed the counters should run at 1 Hz frequency.

All counters should be reset when button 0 is pressed.

The selected counter should pause when button 1 is pressed.
Pressing buttons 2 and 3 should not have any effect when button 1 is pressed.

The counters should run at 8 Hz when button 2 is pressed.
Pressing buttons 3 should not have any effect when button 2 is pressed.

The counters should run at 16 Hz when button 3 is pressed.

Create a testbench to verify your design.
The waveform of the top design should be recorded in the final report.

:point_right: **Task 3**: (10 points)  

In Vivado Flow Navigator open RTL ANALYSIS > Open Elaborated Design > Schematic.
Take a screenshot from the schematic and report it in the final report.

:point_right: **Task 4**: (10 points)  

In Vivado Flow Navigator open IMPLEMENTATION > Open Implementation Design > Schematic.
Take a screenshot from the schematic and report it in the final report.

:point_right: **Task 5**: (10 points)  

In Vivado Flow Navigator open IMPLEMENTATION > Open Implementation Design > Report utilization.
Take a screenshot from the schematic and report it in the final report.

:point_right: **Extra credit**: (10 points)  

Generate a bit steam, program your device, and make a video demo of your design 
running on the hardware.  

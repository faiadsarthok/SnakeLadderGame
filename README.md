# Digital Logic Design: Hardware Snake & Ladder Game

## Team Members

* Shazzad Ahmed Chowdhury
* Faiad Faisal Sarthok
* Fahim Rezwan Shifat
* Ahnaf Sakif
* Mahib Abtahi
* Abdullah Jubayer
* Hasib Ahmed Anik

## Overview

This repository contains the schematic and PCB design files for a fully functional, hardware-level Snake & Ladder game. Developed for the Digital Electronics (EEE 4307) and Digital Logic Design (EEE-4308) courses at the Islamic University of Technology (IUT), this project utilizes fundamental digital logic components to manage game states, RNG dice generation, and player progression without the use of microcontrollers.

## Hardware Architecture

* **Display Board:** A 16-block LED matrix utilizes an active-low, common anode configuration. Dedicated colors track game states: Red for Player 1, Blue for Player 2, Green for ladders, and Yellow for snakes.
* **Player Position Decoding:** Dual decoders equipped with protective resistors map current binary positions directly to the physical LED matrix.
* **Ladder & Snake Routing:** The system utilizes IC74154 (4x16 decoders) alongside IC7483 adders and subtractors to dynamically calculate and route ladder ascents and snake descents.
* **Game Logic Processing:** A dedicated module compares interim player positions with board hazards. If a ladder and a snake overlap, the hardware logic strictly prioritizes the ladder movement.
* **RNG Dice Generation:** A 555 timer generates clock pulses (regulated by the formula $1.44/{C^{*}(R1+2R2)}$) which feed into two D flip-flops, outputting randomized 1, 2, or 3 signals to a 7-segment display.
* **Turn Management:** A J-K flip-flop toggles the active state between Player 1 and Player 2 upon each dice roll.
* **State Memory & Reset:** Dual shift registers and a 2x4 demultiplexer retain historical player data, while a SW-SPDT-MOM switch acts as a hard physical reset for the board.
* **Victory Conditions:** A comparator monitors for the 15th block. Upon reaching it, an X-NOR gate triggers an orange victory LED and an audible buzzer.

## Key Logic Features

* **Start-on-One Validation:** Players are restricted from leaving block zero until a 1 is rolled.
* **Wait-Until-Win:** Prevents players from overshooting the final block; if the rolled value exceeds the remaining distance, the player forfeits the movement.
* **Single-Action Play:** A SW-DPST-MOM switch unifies the dice roll and turn-toggle into a single user action.
* **Boundary Protection:** Hardcoded logic prevents ladder endpoints from exceeding board limits and stops snake tails from dropping into negative values.

## PCB & Schematic Specifications

* **Environment:** Proteus Design Suite.
* **Dimensions:** Modular board designs, including 180mm x 100mm and 120mm x 100mm standard layouts.
* **Routing Standards:** Designed with Thru-Hole via types (V80), DEFAULT/T40/T50 trace styles, 10-th/20-th pad clearances, and auto-routed optimization.

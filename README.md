# 6502-bootloader
Simple bootloader that configures a UART (6551 ACIA chip) to receive 6502 instructions and load them into RAM, ready to be executed by the CPU

### Notes
The 6502 asm is parameterised as best as possible, so change the base memory address for each peripheral/RAM/ROM to suit your system. 

### Usage
- Program an EEPROM chip with the bootloader in this repo.
- Power up and reset the 6502 system.
- vasm (http://sun.hasenbraten.de/vasm/) is used to assemble the 6502 asm, and a raw binary is generated. This binary can simply be pushed over UART (`cat a.out > /dev/ttyUSB0` for example...)
- The 6502 computer will poll the UART receive bit in the 6551's status register, and will read the incoming data byte and load it in the specified base RAM address, and will continue doing this in a loop whilst inrementing its index counter each time a byte is received. 
- The result will be that the user's program is now present in RAM, and when the 6502 receives an `!` character, the program counter will be moved over to the base RAM address and the code will be executed.

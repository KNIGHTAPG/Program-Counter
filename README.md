# Program-Counter using verilog and vhdl

Program Counter is a very important part of any microprocessor or microcontroller. Its job is to store the address of the next instruction to be executed. It is basically a combination of an up counter and PIPO register. For general instruction, PC simply increase the count by 1 after every instruction gets executed. For Branch instructions the PC directly loads the address of the next instruction to be executed. These are the 2 modes of operation of a PC. These 2 modes are selected using 2 control signals i.e increment & load.

We have designed a 4-bit program counter capable of counting from 0000 to 1111 in binary, (0 to F) in hexadecimal, thereby enabling the execution of basic programs in digital systems

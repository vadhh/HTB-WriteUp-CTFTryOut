![image](https://github.com/user-attachments/assets/93800b67-9184-4e83-aee7-c684c26a447a) 
## Category  : Hardware                                                                    
## Tittle    : It's Oops PM
![image](https://github.com/user-attachments/assets/334f65ae-811c-4e80-8da3-6b5fd88b5f95)
## Objective : Find and exploit a backdoor.
## Assets: 4 .vhdl file and schematic image

## Method of Solve
The first step is to understand the system. The schematic shows data coming from an INPUT. This data has two possible paths:
- Path A (Normal): INPUT -> CRYPTO -> MUX -> OUTPUT. The data is encrypted.
- Path B (Backdoor): INPUT -> LOGIC -> MUX -> OUTPUT. The data bypasses encryption.
![schematic](https://github.com/user-attachments/assets/4a4ed378-91d7-4f4c-8b92-c2a3239328cc)
The key component is the MUX, which acts as a switch, selecting between Path A and Path B. 
The schematic shows that the KEY block controls this MUX. 
The story confirms the goal: a "specific input" triggers this backdoor.

## Code Analysis of backdoor.vhdl:
Entity Declaration: The entity backdoor defines a hardware block. It takes a 16-bit input named D and produces a 1-bit output named B.

D is the 16-bit INPUT from the main schematic.
B is the selector signal for the MUX. A '1' will activate the backdoor path, while a '0' will keep the normal encrypted path active.
The Trigger Logic: Inside the architecture, the logic is clear.

A constant named pattern is hardcoded with the value 1111111111101001.
The code continuously compares the input D with this pattern.
If they match, the output B becomes '1'. This flips the MUX switch.
If they don't match, B is '0'.
![image](https://github.com/user-attachments/assets/30dc8f2c-9ece-417c-b25f-16b57f41ab93)

# quadcopter drone control using puffin 
Puffin board works with any FC hardware that runs PX4 or ArduPilot firmware.
## Connect Puffin to FC (flight controller) 
The **ONLY** connection between puffin and FC is via **serial port**, aka **UART** port aka **TELEM** port on the FC.  
see the picture below, connect TX and RX on FC to RX and TX on puffin. Connect the GND is also recommened. 
<img width="729" height="480" alt="Screenshot 2025-07-21 at 2 47 08 PM" src="https://github.com/user-attachments/assets/bb47ea41-10c8-4ddf-bf1a-aff8c0c8550f" />  
Connect RX from FC to pin 19 (TX1) on puffin, TX from FC to pin 21 (RX1) on puffin. Connect GND to GND.  
<img width="1008" height="415" alt="Screenshot 2025-07-21 at 2 52 06 PM" src="https://github.com/user-attachments/assets/e423e572-3cb2-4020-81dc-42600205f354" />
Making sure puffin has a **power supply** either from the battery or from FC. then you are all set!  

# This is for RC car 
## Understand how it works 
A typical RC car includes a radio receiver, an ESC (Electronic Speed Controller), and a steering servo. The ESC and servo are usually connected directly to the receiver. Puffin replaces the radio receiver in this setup.<br>
Before using Puffin, ensure that your RC car has a standalone ESC, steering servo, and RF receiver. Some RC cars use an all-in-one unit that combines the receiver and ESC — in such cases, Puffin is not compatible.
## Hardware setup 
Open your RC car, take out the Radio receiver and connect ESC and servo to the corresponding pins on Puffin, then you are all set ! <br>
<img width="749" height="521" alt="Screenshot 2025-07-21 at 6 43 31 PM" src="https://github.com/user-attachments/assets/bc9dd6e5-251d-4c19-89c7-327da851eecd" /> <br>
<img width="1008" height="415" alt="Screenshot 2025-07-21 at 2 52 06 PM" src="https://github.com/user-attachments/assets/29599d76-b217-445c-bbbb-59fd2e96062d" /><br>
Connect Servo to Pin 1 3 5, namely GND, VCC, PWM2, and connect ESC to Pin 2 4 6, namely GND VCC PWM1. That's it all !  
## Control Software 
Download the zip file 4g_rc_car.zip. unzip the file. In the folder you will see a html file called "Puffin_RC_model.html", double click on it. <br>
Type in your ID no. and click on "connect", you should be able to see live video streaming and you can control the car using the buttons on the control panel. <br>
<img width="1348" height="632" alt="Screenshot 2025-07-21 at 6 57 59 PM" src="https://github.com/user-attachments/assets/8a2fe7af-9916-410c-bc53-56961cacbb9e" /><br>
## Modify speed /steer settings 
Open the source code of Puffin_RC_model.html. The section below defines the speed and steer settings of the car. You can fine tune it by changing the the numbers or use **chatGPT** to help change the parameters<br>
<pre>let axis0 = -(gamepad.axes[0]+0.30);
                    steering_cmd = Math.round((1 - axis0) * 90);

                    document.getElementById('joystickValue').textContent = `Steering: ${axis0.toFixed(2)}`;
                    if (reverse) {
                        throttle_cmd = 100 - Math.round(gamepad.buttons[7].value * 100);
                    } else {
                        throttle_cmd = Math.round(gamepad.buttons[7].value * 100 + 100);
                    }
                    document.getElementById('throttleValue').textContent = `Throttle: ${throttle_cmd}`;
                    let speed = Math.round(gamepad.buttons[7].value * 100 * 0.18);
                    document.getElementById('speedValue').textContent = `Speed: ${speed} M/S`;
                    send_pwm_command(1, steering_cmd) 
                    send_pwm_command(6, throttle_cmd)  </pre>

# This is for RC car 
## Understand how it works 
A typical RC car includes a radio receiver, an ESC (Electronic Speed Controller), and a steering servo. The ESC and servo are usually connected directly to the receiver. Puffin replaces the radio receiver in this setup.<br>
Before using Puffin, ensure that your RC car has a standalone ESC, steering servo, and RF receiver. Some RC cars use an all-in-one unit that combines the receiver and ESC — in such cases, Puffin is not compatible.
## Hardware setup 
Open your RC car, take out the Radio receiver and connect ESC and servo to the corresponding pins on Puffin, then you are all set ! 
<br>
<img width="793" height="528" alt="Screenshot 2025-08-25 at 3 12 42 PM" src="https://github.com/user-attachments/assets/0e9ea3c9-1373-4968-b2ea-af4411f6d9be" />
<img width="1008" height="415" alt="Screenshot 2025-07-21 at 2 52 06 PM" src="https://github.com/user-attachments/assets/29599d76-b217-445c-bbbb-59fd2e96062d" /><br>
Connect Servo to Pin 2 4 6, namely GND, VCC, PWM1, and connect ESC to Pin 1 3 5, namely GND VCC PWM2. That's it all !  
## Control Software 
Download the zip file RC_cars_intl.zip. unzip the file. In the folder you will see a html file called "Puffin_RC_model.html", double click on it. <br>
Type in your ID no. and click on "connect", you should be able to see live video streaming and you can control the car using the buttons on the control panel. <br>
<img width="1348" height="632" alt="Screenshot 2025-07-21 at 6 57 59 PM" src="https://github.com/user-attachments/assets/8a2fe7af-9916-410c-bc53-56961cacbb9e" /><br>
## Different Control Software
You can modify the source code of "Puffin_RC_model.html" or use a different control software <br>
For examle you can use the "puffin_RC_model_keyboard_wasd_2ESC_4PWM" [here](https://github.com/WIRELESSX-HK/Puffin_KS/blob/main/RC_cars/puffin_RC_model_keyboard_wasd_2ESC_4PWM.html)<br>
put "puffin_RC_model_keyboard_wasd_2ESC_4PWM.html" file in the unzipped folder (previous step), double click on it. See the picture below, in this new control software you can use w a s d to control steering and forward/backward. <br>
On the top left corner <br>
### ⚙️ Neutral Offset Configuration (Important for ESC)

When using the Puffin board to control your RC car or vehicle, setting the **Neutral Offset** is **critical** for correct ESC behavior.

#### 🔍 What is Neutral Offset?

The **Neutral Offset** is the PWM threshold value that tells the ESC when the vehicle should be **idle**, **move forward**, or **reverse**.

- If the PWM value is **above** the neutral offset, the car moves **forward**.
- If it's **below**, the car goes **in reverse**.
- At the exact offset, the car remains **stationary**.

Different ESCs have different neutral points — some start responding at **110**, others at **130** or even higher.

### 📊 Typical Neutral Offset Values

| ESC Type           | Approximate Neutral Offset |
|--------------------|----------------------------|
| Generic ESC (Type A) | 110                        |
| Generic ESC (Type B) | 130                        |

### 🧪 How to Test & Calibrate

1. **Lift the wheels off the ground** to avoid accidental movement.
2. Power on your system.
3. Slowly increase the PWM value from 100 upwards.
4. Note the point at which the wheels begin to move forward.
5. Set this value as your `neutral_offset` parameter in your configuration.

### 💡 Tips

- Incorrect neutral offset may cause your car to move unintentionally when idle.
- You can include this value in your software or configuration file (e.g., YAML or JSON) for consistent behavior on every startup.
- Always test in a safe environment before driving on the ground.

<img width="1293" height="647" alt="Screenshot 2025-10-09 at 5 01 36 PM" src="https://github.com/user-attachments/assets/3aee3582-5c57-4d42-b4cc-0d4837400545" /><br>


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

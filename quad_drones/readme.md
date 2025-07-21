# quadcopter drone control using puffin 
Puffin board works with any FC hardware that runs PX4 or ArduPilot firmware.
## Connect Puffin to FC (flight controller) 
The **ONLY** connection between puffin and FC is via **serial port**, aka **UART** port aka **TELEM** port on the FC.  
see the picture below, connect TX and RX on FC to RX and TX on puffin. Connect the GND is also recommened. 
<img width="729" height="480" alt="Screenshot 2025-07-21 at 2 47 08 PM" src="https://github.com/user-attachments/assets/bb47ea41-10c8-4ddf-bf1a-aff8c0c8550f" />  
Connect RX from FC to pin 19 (TX1) on puffin, TX from FC to pin 21 (RX1) on puffin. Connect GND to GND.  
<img width="1008" height="415" alt="Screenshot 2025-07-21 at 2 52 06 PM" src="https://github.com/user-attachments/assets/e423e572-3cb2-4020-81dc-42600205f354" />
Making sure puffin has a **power supply** either from the battery or from FC. Then you are all set!  
## Baud rate 
Making sure the baud rate of your FC UART is 115200
## Control software 
### Download control software 
You need to download a zip file containing control software. the control software is web based  
download puffin-4g-drone-webapp-v01.zip on your local laptop 
### Use Control software 
In the folder, choose index.html,double click and you will see the control panel  
you need to connect a game joystick to your PC to control the drone. 
Type in your ID no. on the top left corner of the control panel and click on start you should be able to see live video streaming  
<img width="1286" height="587" alt="Screenshot 2025-07-21 at 3 20 04 PM" src="https://github.com/user-attachments/assets/f49d9a2d-0f00-4f1d-8bf2-511f7dcd3228" />
### Joy stick support 
We support Xbox-style controllers by default. To use other types of controllers, you’ll need to modify the index.html source code. The section below defines how joysticks are handled. You can use **ChatGPT** to assist with customizing the code
<pre>var previousButtons = [];  // 
var game = 0;
    window.addEventListener("gamepadconnected", function(e) {
      document.getElementById("xboxstatus").innerText = "gamepad connected: " + e.gamepad.id;
      requestAnimationFrame(updateStatus);
    });
    window.addEventListener("gamepaddisconnected", function(e) {
      document.getElementById("xboxstatus").innerText = "gamepad disconnected";
      previousButtons = [];  
    });

    function executeCommand(command) {
      console.log(command + " command running");
    }
    function updateStatus() {
      var gamepads = navigator.getGamepads();
      if (gamepads[0]) {
        var gp = gamepads[0];
        var buttonsStatus = "";
        for (var i = 0; i < gp.buttons.length; i++) {
          buttonsStatus += "button" + i + "-" + (gp.buttons[i].pressed ? "1" : "0");
        
          if (gp.buttons[i].pressed && (previousButtons[i] === false || previousButtons[i] === undefined)) 
		  {
            if (i === 0) {executeCommand("arm");arm_command();} 
			else if (i === 1) {executeCommand("disarm");disarm_command();} 
			else if (i === 2) {executeCommand("Alt");ALT_command();}
			else if (i === 4) {if ( game === 1){game=0;}else {game=1;}}
			else if (i === 3) {executeCommand("pos");POS_command();}
			else if (i === 5) {executeCommand("return");RTL_command();}
			//else if (i === 6) {executeCommand("自动");AUTO_command();}
          }
		  if ( game === 1){
		  executeCommand("GAME");GAME_command();
			}
          previousButtons[i] = gp.buttons[i].pressed;
        }
        document.getElementById("xboxstatus").innerHTML = "status：<br/>" + buttonsStatus + "<br/>" +
          "YAW:" + gp.axes[0].toFixed(2) +"<br/>"+
          "THR:" + gp.axes[1].toFixed(2) +"<br/>"+
          "ROLL:" + gp.axes[2].toFixed(2) +"<br/>"+
          "PITCH:" + gp.axes[3].toFixed(2);
		  
		 //
    
       // 
      yaw = Math.round(gp.axes[0] * 300+1500);
		  thr = Math.round(-gp.axes[1] *400+1500);  // 
		  roll = Math.round(gp.axes[2] * 300+1500);
		  pit = Math.round(gp.axes[3] * 300+1500); 
    }
	 setTimeout(updateStatus, 100); // 
    }</pre>



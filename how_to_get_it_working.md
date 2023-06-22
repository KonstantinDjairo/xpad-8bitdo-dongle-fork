FROM https://www.reddit.com/r/Fedora/comments/zmvkdj/8bitdo_ultimate_bluetooth_controller_working_in/

-----

I've bought this new controller from 8BitDo and wished to use on linux, to my sadness the controller didn't work out of the box, neither by cable, the 2.4G dongle or bluetooth.  


So I've tried a number of solutions and this one from u/GodOfEmus over in the 8bitdo community was the one to work for me:  


1. Create a new file /etc/udev/rules.d/99-8bitdo-xinput.rules
2. Paste this udev rule in there, then save and exit the file: 
  
  ```bash
    ACTION=="add", ATTRS{idVendor}=="2dc8", ATTRS{idProduct}=="3106", RUN+="/sbin/modprobe xpad", RUN+="/bin/sh -c 'echo 2dc8 3106 > /sys/bus/usb/drivers/xpad/new_id'"
  ```
3. Run the following command in a terminal: `sudo udevadm control --reload`
4. Unplug and replug the controller if it was already plugged in, it might take a second if you have the bluetooth version

It will basically "cheat" the OS to see the controller as an generic xbox device, so sadly no bluetooth nor gyro control if you care about that, but the rumbling is working for me.  


Link to the original post: [https://www.reddit.com/r/8bitdo/comments/ykdsmv/ultimate\_24\_ghz\_model\_right\_analog\_not\_working\_in/](https://www.reddit.com/r/8bitdo/comments/ykdsmv/ultimate_24_ghz_model_right_analog_not_working_in/)  


And link to the comment of u/GodOfEmus with the solution: [https://www.reddit.com/r/8bitdo/comments/ykdsmv/comment/iv48s4k/?utm\_source=share&utm\_medium=web2x&context=3](https://www.reddit.com/r/8bitdo/comments/ykdsmv/comment/iv48s4k/?utm_source=share&utm_medium=web2x&context=3)  


Sharing this solution here to spread the word in our community

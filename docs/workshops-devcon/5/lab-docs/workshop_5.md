# Workshop 5: Creating a new gesture

In this workshop, you create a new gesture. Gestures enable Intu to take specific actions, such as make sounds, use SMS, send emails, call the Text to Speech service, wait, update status, turn the volume up or down, and so on.

**Before you begin:** You must have a Mac or Windows laptop.

Pick up one of each of the following items in the room:

* Raspberry Pi with a power cable
* Speaker
* Microphone
* Camera
* 32 GB or larger SD card

The following items are set up for you to use in the room:

* Monitor with an HDMI connection
* Keyboard and mouse with USB connections

Complete the following tasks:

1. [Setting up your Raspberry Pi](#setting-up-your-raspberry-pi)
2. [Setting up the Raspberry Pi build](#setting-up-the-raspberry-pi-build)

## Setting up your Raspberry Pi

1. Load your new SD card with the required files.
  1. [Open NOOBS](https://www.raspberrypi.org/downloads/noobs/).
  2. Under NOOBS offline and network install, click **Download ZIP**, save the package, and extract the files in a local directory. Let's call this directory your NOOBS directory.
  3. Navigate to the NOOBS directory, open `readme.txt`, complete the instructions to format your SD card.
  4. After your SD card is formatted, drag all the files in your NOOBS directory and drop them onto the SD card. Now your SD card has all the necessary files.
  5. Safely remove the SD card, and insert it into your Raspberry Pi.
2. Install the Raspbian operating system.
  1. Connect the following items to your Raspberry Pi:
    * Power source. The following image shows where to plug the power cable into the Raspberry Pi.
![Alt text](images/pi_charger.png?raw=true "Optional Title")
    * External keyboard via USB.
    * Monitor. After you connect a monitor, a window that shows a **Wifi networks (w)** icon is displayed.
The following image shows the USB port where the keyboard is connected and the HDMI port where the monitor is connected on the Raspberry Pi.
![Alt text](images/external_monitor_keyboard_to_pi.png?raw=true "Optional Title")
To complete substes 2 - 6, you'll use the external monitor and keyboard.
  2. On the window displayed on your monitor, click **Wifi networks (w)**, select your network, and specify your password. If you see a blank screen on your monitor and nothing happens, return to step 3 above and reformat your SD card.
  3. You're using your Raspberry Pi and SD card for the very first time, so you need to install an OS. Select **Raspbian**.
  4. At the bottom of the window is a language panel for your keyboard. Select **English (US)**.
  5. Click the **Install** icon in the top left part of the window. When the confirmation prompt is displayed, select **Yes**. The installation process lasts 30 - 40 minutes. If the installation process stalls at 0%, unplug the power source from your Raspberry Pi, plug the power source in again, and begin at substep 2 again.
3. Connect your Raspberry Pi to your laptop.
  1. Ensure you're still connected to the network. If you're still connected to the network, a blue wifi icon is displayed beside the Bluetooth icon on the top right corner of the window. If you're disconnected, the icon is two red crosses. To reconnect, click the two red crosses icon, select your network, and specify your password. This process might reboot your system.
  2. Click on the **Terminal** window on the top left of the toolbar.
  3. Specify `ipconfig` to get your IP address, and press Enter.
  4. Locate the wlan0 section. Your IP address is in the **inet addr** field.
  5. Test whether you can connect to your Raspberry Pi via SSH. Open a terminal window on your laptop, and run `ssh pi@*ip_address*`, where *ip_adddress* is the IP address you got in Step 3, such as `ssh pi@10.0.1.2`.
  6. At the password prompt, specify the default password `raspberry`.

If you can't connect to your Raspberry Pi, reboot it by running `sudo reboot`.

4. Disconnect the external monitor and the keyboard from the Raspberry Pi, return to your laptop, and ensure your Raspberry Pi and laptop are connected to the same network.

## Setting up the Raspberry Pi build

1. Reboot the Raspberry Pi from your laptop.
  1. Open a terminal window on your laptop, and connect to your Raspberry Pi via SSH by issuing the `ssh pi@*ip_address*` command, where *ip_adddress* is the IP address your IP address, such as `ssh pi@10.0.1.2`.
  2. At the password prompt, specify the default password `raspberry`.
  3. Reboot your Raspberry Pi by issuing the `sudo reboot` command.
1. [Download Anaconda 2.7 for Linux 32 bit](https://www.continuum.io/downloads). **Important**: Make sure you download the correct version.
2. Navigate to the directory where you downloaded the Anaconda package, and copy the package to the Raspberry Pi by issuing the following command:
```
scp Anaconda3-4.2.0-Linux-x86.sh pi@{ip}:~/
```
3. Connect to your Raspberry Pi via SSH by issuing `ssh pi@*ip_address*`, where *ip_address* is the IP address you got in the previous task.
4. Install Anaconda by completing the following steps:
  1. Issue `bash Anaconda3-4.2.0-Linux-x86.sh`.
  2. Complete the displayed steps. When you get to the license, press **Enter** until you reach the end, and specify **Yes** to approve the license.
  3. Press **Enter** to install Anaconda in the default location. Installation might take some time. If the following message is issued, ignore it:
```
Anaconda3-4.2.0-Linux-x86.sh: line 484: /home/pi/anaconda3/pkgs/python-3.5.2-0/bin/python: cannot execute binary file: Exec format error
ERROR:
cannot execute native linux-32 binary, output from 'uname -a' is:
Linux raspberrypi 4.4.21-v7+ #911 SMP Thu Sep 15 14:22:38 BST 2016 armv7l GNU/Linux
```
5. Run `sudo apt-get install python-pip cmake`. If the command fails, run `sudo apt-get update`, and run `sudo apt-get install python-pip cmake` again.
6. Run `sudo pip install qibuild`.
7. Install the **wiringPi** library.
  1. Navigate to your home directory `/home/pi` and run `git clone git://git.drogon.net/wiringPi`.
  2. Navigate into the wiringPi directory by issuing `cd wiringPi/`.
  3. Run `./build`. A list of compiled classes is displayed, and the "All Done" message is at the end.
8. On your laptop, open the [Self SDK repository](https://github.ibm.com/watson-labs-austin/self-sdk).
9. Click **Clone or download**, and select **Download Zip**.
10. Return to the terminal window for your Pi. In the Pi's home directory, `/home/pi`, create a directory called self. Run `mkdir self`.
11. Navigate to the new self directory.
12. On your laptop, navigate to the directory where you downloaded the Self SDK, and copy the SDK package to the self directory on your Raspberry Pi by running `scp self-sdk-develop.zip pi@{ip}:~/self/`.
13. When you're prompted for the Pi's password, specify `raspberry`.
14. On the Raspberry Pi, open the self directory, and run `unzip self-sdk-develop.zip`.
15. Navigate to the self-sdk-develop directory by running `cd self-sdk-develop`.
16. Mark the build script as executable by running `chmod +x scripts/build_raspi.sh`.
17. Determine which command to run:
  * If this is your first time going through this process, run `scripts/build_raspi.sh raspi`.
  * If you've been through this process previously, run `scripts/clean.sh`.
18. In the self-sdk-develop directory, navigate to raspi by running `cd bin/raspi`.
19. Run the following commands:
  * `export LD_LIBRARY_PATH=~/self/self-sdk-develop/bin/raspi`
  * `export WIRINGPI_GPIOMEM=1`
20. Run self by running `./self_instance –c 0 –f 0`.
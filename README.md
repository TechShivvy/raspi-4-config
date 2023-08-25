# Raspberry Pi 4 Configuration Guide

For any queries or uncertainties, please refer to the [Official Raspberry Pi documentation](https://www.raspberrypi.com/documentation/). This comprehensive resource can assist you in addressing any doubts you might have during the setup process.

## Components for Pi Setup

- **SD Card**: Essential for installing the Pi operating system.
- **SD Card Reader**: Required if your laptop lacks an inbuilt SD card reader.
- **Micro HDMI to HDMI Cable**: Required if you want to connect your Pi to an HDMI TV or display, or any other appropriate converter or cable from micro HDMI to an output port.
- **Ethernet Cable**: Required if you want to establish LAN connections.
- **Type C Power Adapter for Pi**: Necessary to provide power to the Pi. A 5V power supply is suitable as well. Various power methods are available; you can explore more options in this resource: [Raspberry Pi Power Methods](https://www.makeuseof.com/raspberry-pi-power-methods/).
- **Keyboard and Mouse**: Required for initial setup and configuration. If using a TV, ensure the USB dongle is connected to the Pi's USB port for input. If accessing via laptop, a separate keyboard and mouse are not necessary, as you can use the laptop's built-in keyboard and touchpad/mouse.

## Setup and Configuration of Raspberry Pi 4

### With Display (HDMI TV)

1. Follow the official Raspberry Pi setup guide: [Raspberry Pi Setting Up](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/0). However, during the installation process, opt for the 64-bit version instead of the recommended 32-bit version to take full advantage of your hardware capabilities.

### Without Display (Headless)

1. For an alternative headless setup guide, you can refer to this resource: [Raspberry Pi Headless Setup Guide](https://www.tomshardware.com/reviews/raspberry-pi-headless-setup-how-to,6028.html) or [Official Documentation for Headless](https://www.raspberrypi.com/documentation/computers/configuration.html#setting-up-a-headless-raspberry-pi). However, note that **using a display is often simpler**.

## Finding Pi's IP Address

There are several methods to find the IP address of your Pi based on your connection:

**When Connected to the Same Network:**

1. **Connected via Network**:
   - If your Pi is connected to the network, either through Wi-Fi or Ethernet, and your mobile/laptop is on the same network, you can find its IP address using various methods:
     - Access your router's admin page to locate the connected devices section.
     - Utilize an application like "Fing" on your mobile device to scan for devices within your network.
     - Employ commands such as `nmap` in a Linux environment to discover devices on the network.

2. **Using mDNS (Bonjour)**:
   - When your laptop and Pi are part of the same network, or if the Pi is connected via Ethernet to your laptop, you can employ mDNS (Multicast DNS) to effortlessly find the Pi's IP address.
   - Launch the command prompt or terminal on your laptop and execute the following command:
     
     ```
     ping raspberrypi.local -4
     ```
     If you've changed the hostname of your Pi, replace `raspberrypi` with the updated name.
     
     Note: Keep in mind that mDNS might not work reliably if you have multiple Raspberry Pi devices on the network, as the .local address might not uniquely identify each device.
   - When the Pi is active and connected to the network, this command will send a ping request to the mDNS address and receive a reply containing the IP address of the Pi.

**When You Have Direct Access to the Pi:**

3. **Direct Access to Pi**:
   - If you possess direct access to your Pi, whether through SSH or a display connection, you can determine the IP address by executing the following command on the Pi's command line:
     
     To discover the IP addresses linked to all network interfaces:
     ```
     hostname -I
     ```

     To obtain detailed information about the network interfaces, including IP addresses:
     ```
     ifconfig
     ```

   - After executing these commands, make a note of the IP addresses (inet) linked to the available network interfaces (such as `eth0` for Ethernet and `wlan0` for Wi-Fi).

Remember that some methods might be more suitable depending on your network setup and the tools available to you.

## Few more configurations

### Enable VNC and SSH
Use any of the below methods:
 - GUI Method: Click on the Pi icon (top left) -> Preferences -> Raspberry Pi Configuration -> Interfaces -> Enable SSH and VNC.
 - Command Line Method: Run the following command in the terminal:
   
   ```bash
   sudo raspi-config
   ```
Then, select "Interface Options," navigate to SSH and VNC options, and enable them as needed. This will allow you to configure and enable SSH and VNC access to your Pi.

### Headless Display Resolution Configuration
If Pi is headless, set a fixed resolution:
- Pi icon (top left) -> Preferences -> Raspberry Pi Configuration -> Display.
- Set the desired resolution to ensure correct VNC display.

### Sharing Laptop's Internet Connection over Ethernet

If you want to share the internet connection from your laptop to the Pi via Ethernet:

1. Open Control Panel -> Network and Internet -> Network and Sharing Center.
2. Choose "Change adapter settings."
3. Right-click on the source of your internet connection, open Properties.
4. Go to the "Sharing" tab and enable "Allow other network users to connect through this computer's internet connection."
5. Choose your Pi's Ethernet connection from the dropdown menu.

## Accessing Pi

If you're only using one Pi on your network, the default hostname `raspberrypi.local` can be used to connect, but this will fail as you add more devices, so it's worth going with the IP address. By using the respective IP addresses (`wlan0` or `eth0`), you can conveniently connect to your Pi using either VNC or SSH based on your needs and preferences. (Refer to the section "Finding Pi's IP Address" for details on obtaining the IP address.)

### Access via VNC (remote graphical desktop access)

#### Wireless (Wi-Fi) Connection:

- **VNC**:
  - For portable access, use VNC.
  - Access VNC using the Wi-Fi IP address (`wlan0` IP) or simply use `raspberrypi.local`.
  - Open VNC Viewer, add a new connection using the obtained IP or `raspberrypi.local` (by default), and enter username and password.

#### Wired (Ethernet) Connection:

- **VNC**:
  - Access VNC using the Ethernet IP (`eth0` IP) or `raspberrypi.local`.
  - Access using VNC Viewer as explained above.

### Access via SSH (terminal access)

#### Wireless (Wi-Fi) Connection:

- **SSH**:
  - Access SSH using the Wi-Fi IP address (`wlan0` IP) or use `raspberrypi.local`.
  - Open PowerShell/Terminal and enter the following commands:

      For connecting via IP address:
      ```bash
      ssh <username>@<ip>
      ```
      
      For connecting using the default hostname "raspberrypi.local":
      ```bash
      ssh <username>@raspberrypi.local
      ```
      
      For connecting using a custom hostname:
      ```bash
      ssh <username>@<hostname>.local
      ```

Replace `<username>` with your actual username and `<ip>` or `<hostname>` with the appropriate IP address or hostname of your Pi.

#### Wired (Ethernet) Connection:

- **SSH**:
  - Access SSH using the Ethernet IP (`eth0` IP) or `raspberrypi.local`.
  - Access using SSH as explained above.

## Transferring Files To/From Pi

### Copy from Pi to System

Use the `scp` command to copy files from Pi to your system:

```bash
scp -r <username>@<ip>:/home/<username>/<path to file or folder> C:\Users\<name>\<path to download location>
```

### Copy to Pi from System

Use the `scp` command to copy files from your system to Pi:

```bash
scp -r <full path to file or folder> <username>@<ip>:/home/<username>/<path to copy location>
```

**Note:** Replace `<username>`, `<ip>`, `<name>`, and paths with appropriate values.

## QoL Tips

1. **Proper Shutdown and Restart**:
   - To avoid data corruption and file loss, use the following commands in the Pi terminal:
     - For a proper shutdown:
       
       ```
       sudo poweroff
       ```
     - For a restart:
       
       ```
       sudo reboot
       ```
   - These commands ensure that your Pi goes through a controlled shutdown and restart process.

2. **Double-Check Connection and IP**:
   - If you encounter connection errors, verify that you are using the correct IP address based on your chosen connection method (Wi-Fi or Ethernet).
   - Ensure that the chosen connection (Wi-Fi or Ethernet) is active and properly configured.

3. **IP Address Management**:
   - Keep in mind that every time you connect your Pi to a new network source (Wi-Fi, Ethernet, etc.), the IP address might change due to DHCP.
   - To avoid confusion, make a habit of checking and noting down the IP address each time you connect to a new network.

4. **Setting a Static IP**:
   - If you want a consistent IP address for your Pi, consider setting a static IP. You can follow the instructions from this guide: [Setting a Static IP on Raspberry Pi](https://phoenixnap.com/kb/raspberry-pi-static-ip).
   - The GUI method is user-friendly and doesn't involve manually editing system configuration files.

5. **Triple Check Key Information**:
   - Before connecting remotely to your Pi, triple-check the following:
     - IP address (based on Wi-Fi or Ethernet).
     - Username (default is usually `pi` or the one you've set during configuration).
     - Password (the one you've set during configuration).

6. **Regular File Backups**:
   - Pi's SD cards can be vulnerable to corruption, which might lead to data loss. To mitigate this risk, regularly back up your important files and data to an external storage device, cloud storage, or another computer. This way, even if the SD card becomes corrupted, you'll still have a copy of your valuable data.

7. **Always Be Prepared**:
   - It's a good practice to have a microSD card reader and an Ethernet cable readily available. These tools can come in handy if you need to troubleshoot or make changes to your Raspberry Pi setup on the go. An Ethernet cable can provide a fast and reliable connection, especially when you're in a new place where Wi-Fi might not be readily available.

By following these tips, you can ensure a smoother experience while working with your Pi and minimize potential connectivity issues.

## Common Issues and Fixes

1. **Managing SSH Host Key Changes**:
   - If you encounter an SSH error like the one below when trying to connect to your Raspberry Pi:

     ```
     @@@@@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @@@@@
     IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
     ...
     ECDSA host key for raspberrypi.local has changed and you have requested strict checking.
     Host key verification failed.
     ```

     This error can occur when the host key of your Raspberry Pi changes due to reasons such as reinstallation or IP changes. To resolve this issue and re-establish trust with the host, run the following command in your local terminal:

     ```
     ssh-keygen -R <ip>
     ```

     Replace `<ip>` with the IP address of your Raspberry Pi or its hostname (e.g., raspberrypi.local). This command removes the outdated key from your known_hosts file, allowing you to connect without the verification error.

2. **Maximized Window Does Not Fill Desktop in Headless Mode**:
    - Open the `config.txt` file using the command: `sudo nano /boot/config.txt`
    - Look for the lines containing `framebuffer_width` and `framebuffer_height`. If they are commented (with a `#` at the beginning), remove the `#` to uncomment them. If they are not present, add the following lines:
        ```
        framebuffer_width=1920
        framebuffer_height=1080
        ```
        You can adjust the values (1920 and 1080) according to your desired resolution.
    - Save the file and reboot Pi.

     If this solution doesn't work for you, you can also experiment with other options mentioned in this [GitHub issue thread](https://github.com/raspberrypi/Raspberry-Pi-OS-64bit/issues/225), such as setting `hdmi_group`, `hdmi_mode`, or `hdmi_cvt` values to tailor the resolution to your needs.

3. **'Cannot Currently Show the Desktop' Error**:

Encountering the 'Cannot Currently Show the Desktop' error can be frustrating, and while a definitive fix might be elusive, there are a few strategies you can try. Most solutions you'll find online involve adjusting settings in the `/boot/config.txt` file. Although no one-size-fits-all solution exists, here are a couple of steps that might help:

1. **Uncomment `hdmi_safe=1`**:
   - Open the `/boot/config.txt` file by using the command: `sudo nano /boot/config.txt`.
   - Look for the line containing `hdmi_safe=1`. If it's commented out (preceded by a `#`), remove the `#` to uncomment it. If this line is not present, add it.
   - Save the file and reboot your Raspberry Pi.

2. **Exploring Other Options**:
   - Other solutions involve experimenting with different combinations of `hdmi_flags`, `hdmi_group`, `hdmi_mode`, and `hdmi_cvt` settings in the `config.txt` file.
   - You can try different values and configurations to see if they resolve the issue. It might require a bit of trial and error.

3. **Further Exploration**:
   - The 'Cannot Currently Show the Desktop' error is quite specific, and solutions might depend on the exact circumstances.
   - If the above solutions don't work, it's worth searching online forums, websites, and platforms like YouTube for additional strategies that have worked for others.


## Conclusion

This guide serves as a valuable resource for successfully harnessing the capabilities of your Raspberry Pi 4, empowering you to explore and engage with its features effectively.

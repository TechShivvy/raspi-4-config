# Raspberry Pi Configuration Guide

## Components for Raspberry Pi Setup

- **SD Card**: Essential for installing the Raspberry Pi operating system.
- **SD Card Reader**: Required if your laptop lacks an inbuilt SD card reader.
- **Micro HDMI to HDMI Cable**: Required if you want to connect your Raspberry Pi to an HDMI TV or display, or any other appropriate converter or cable from micro HDMI to an output port.
- **Ethernet Cable**: Required if you want to establish LAN connections.
- **Power Adapter for Pi**: Necessary to provide power to the Raspberry Pi. A 5V power supply is suitable as well.
- **Keyboard and Mouse**: Required for initial setup and configuration. If using a TV, ensure the USB dongle is connected to the Pi's USB port for input. If accessing via laptop, a separate keyboard and mouse are not necessary, as you can use the laptop's built-in keyboard and touchpad/mouse.

## Setup and Configuration of Raspberry Pi 4

### With Display (HDMI TV)

1. Follow the official Raspberry Pi setup guide: [Raspberry Pi Setting Up](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/0).

### Without Display (Headless)

1. Follow the initial steps of the official setup guide without connecting to a display.
2. For an alternative headless setup guide, you can refer to this resource: [Raspberry Pi Headless Setup Guide](https://www.tomshardware.com/reviews/raspberry-pi-headless-setup-how-to,6028.html). However, note that using a display is often simpler.

## Finding Raspberry Pi's IP Address

There are several methods to find the IP address of your Raspberry Pi based on your connection:

1. **Connected to Router**:
   - If your Raspberry Pi is connected to the router using Ethernet, you can find its IP address using various methods:
     - Check your router's admin page to locate the connected devices section.
     - Use an app like "Fing" on your mobile device to scan for devices on your network.
     - Utilize commands like `nmap` in Linux to discover devices on your network.

2. **Wi-Fi or Ethernet Connection**:
   - When connected via Wi-Fi or Ethernet to your laptop, you can find the IP address by running the command `hostname -I` or `ifconfig` on the Raspberry Pi's command line.
   - Note down the IP addresses(inet) associated with the `eth0` (Ethernet) and `wlan0` (Wi-Fi) interfaces.

## Few more configurations

### Enable VNC and SSH
Use any of the below methods:
 - GUI Method: Click on the Raspberry Pi icon (top left) -> Preferences -> Raspberry Pi Configuration -> Interfaces -> Enable SSH and VNC.
 - Command Line Method: Run `sudo raspi-config`, select "Interface Options," and enable SSH and VNC.

### Headless Display Resolution Configuration
If Pi is headless, set a fixed resolution:
- Raspberry Pi icon (top left) -> Preferences -> Raspberry Pi Configuration -> Display.
- Set the desired resolution to ensure correct VNC display.

### Sharing Laptop's Internet Connection over Ethernet

If you want to share the internet connection from your laptop to the Raspberry Pi via Ethernet:

1. Open Control Panel -> Network and Internet -> Network and Sharing Center.
2. Choose "Change adapter settings."
3. Right-click on the source of your internet connection, open Properties.
4. Go to the "Sharing" tab and enable "Allow other network users to connect through this computer's internet connection."
5. Choose your Raspberry Pi's Ethernet connection from the dropdown menu.

## Accessing Raspberry Pi

By using the respective IP addresses (`wlan0` or `eth0`), you can conveniently connect to your Raspberry Pi using either VNC or SSH based on your needs and preferences. (Refer to the section "Finding Raspberry Pi's IP Address" for details on obtaining the IP address.)

### Access via VNC (remote graphical desktop access)

#### Wireless (Wi-Fi) Connection:

- **VNC**:
  - For portable access, use VNC.
  - Access VNC using the Wi-Fi IP address (`wlan0` IP).
  - Open VNC Viewer, add a new connection using the obtained IP, and enter username and password.

#### Wired (Ethernet) Connection:

- **VNC**:
  - Access VNC using the Ethernet IP (`eth0` IP).
  - Access using VNC Viewer as explained above.

### Access via SSH (terminal access)

#### Wireless (Wi-Fi) Connection:

- **SSH**:
  - Access SSH using the Wi-Fi IP address (`wlan0` IP).
  - Open PowerShell/Terminal and enter: `ssh <username>@<ip>`.

#### Wired (Ethernet) Connection:

- **SSH**:
  - Access SSH using the Ethernet IP (`eth0` IP).
  - Access using SSH as explained above.

## Transferring Files To/From Raspberry Pi

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
   - Avoid abruptly pulling out the power supply from the Raspberry Pi.
   - Always use the commands `sudo poweroff` for a proper shutdown and `sudo reboot` for a restart in the Raspberry Pi terminal.

2. **Double-Check Connection and IP**:
   - If you encounter connection errors, verify that you are using the correct IP address based on your chosen connection method (Wi-Fi or Ethernet).
   - Ensure that the chosen connection (Wi-Fi or Ethernet) is active and properly configured.

3. **IP Address Management**:
   - Keep in mind that every time you connect your Raspberry Pi to a new network source (Wi-Fi, Ethernet, etc.), the IP address might change due to DHCP.
   - To avoid confusion, make a habit of checking and noting down the IP address each time you connect to a new network.

4. **Setting a Static IP**:
   - If you want a consistent IP address for your Raspberry Pi, consider setting a static IP. You can follow the instructions from this guide: [Setting a Static IP on Raspberry Pi](https://phoenixnap.com/kb/raspberry-pi-static-ip).
   - The GUI method is user-friendly and doesn't involve manually editing system configuration files.

5. **Triple Check Key Information**:
   - Before connecting remotely to your Raspberry Pi, triple-check the following:
     - IP address (based on Wi-Fi or Ethernet).
     - Username (default is usually `pi` / one you've set during configuration).
     - Password (the one you've set during configuration).

By following these tips, you can ensure a smoother experience while working with your Raspberry Pi and minimize potential connectivity issues.


## Conclusion

This guide serves as a valuable resource for successfully harnessing the capabilities of your Raspberry Pi 4, empowering you to explore and engage with its features effectively.

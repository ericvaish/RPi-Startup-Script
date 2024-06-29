# RPi-Startup-Script

If you want a script to run as soon as the Raspberry Pi boots, you can use the `/etc/rc.local` file. This file is executed by the system during the final stage of the boot process. Here’s how you can add your script to `rc.local`:

1. Open the `rc.local` file with a text editor:

   ```sh
   sudo nano /etc/rc.local
   ```

2. Before the `exit 0` line, add the command you want to run. For example, to run `python3 /home/pi/myscript.py`:

   ```sh
   #!/bin/sh -e
   # rc.local

   # Print the IP address
   _IP=$(hostname -I) || true
   if [ "$_IP" ]; then
     printf "My IP address is %s\n" "$_IP"
   fi

   # The below line is used to turn on Raspberrypi Hotspot on boot.
   #sudo nmcli device wifi hotspot ssid SSID_NAME password PASSWORD_HERE ifname wlan0
   # If you want, you can run your own script on startup by mentioning the location below.
   python3 /home/pi/myscript.py


   exit 0
   ```

3. Save the file and exit the editor (in Nano, press `CTRL + X`, then `Y`, and `Enter`).

4. Ensure the `rc.local` file is executable:

   ```sh
   sudo chmod +x /etc/rc.local
   ```

After making these changes, your script should run automatically on startup. You can reboot your Raspberry Pi to test if it works:

```sh
sudo reboot
```

When the system starts up again, your script should execute. This method ensures that your script runs as soon as the Raspberry Pi boots.

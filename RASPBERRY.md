# Reset lost admin password for Raspberry Pi

Raspberry Pis are great, but sometimes their ability to keep running in the background can lead to forgotten root passwords. I've had more than one time where I was sure I knew the root password, only to learn that I had forgotten.

Luckily, Raspberry Pi has a "feature" that most Linux machines don't: very easily removable primary storage.

To reset your password:

- Power down and pull the SD card out from your Pi and put it into your computer.
- Open the file **'cmdline.txt'** and add **'init=/bin/sh'** to the end. This will cause the machine to boot to single user mode.
- Put the SD card back in the Pi and boot.
- When the prompt comes up, type **'su'** to log in as root (no password needed).
- Type **"passwd pi"** and then follow the prompts to enter a new password.
- Shut the machine down, then pull the card again and put the **cmdline.txt** file back the way it was by removing the **'init=/bin/sh'** bit.

The cmdline.txt should look something like this:

**dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait init=/bin/sh**

It's worth noting that with this process being as easy as it is, to consider than a malicious person with physical access to your Raspberry Pi could do this as easily as you can.



# ROOT ACCOUNT PROMPTING FOR PASSWORD:

If the root account is prompting for a password (not common) you can, back on your computer, open the /etc/shadow file and replace the root password in there with an asterisk. This will change the password to be blank.



# ERROR WHEN CHANGING THE PASSWORD:

Note: Sometimes the password won't be able to be changed because the Pi will boot in a read-only mode. You'll get an error that you can't change the password. To fix this, remount the drive in read-write mode:

**mount -o remount,rw /**

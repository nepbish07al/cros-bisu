**CHEAT SHEET FOR ChromeOS installation**

Recommended to read this guide before you start:

https://github.com/sebanc/brunch
#!/bin/bash
sudo apt update && sudo apt -y install pv cgpt tar unzip

#sudo add-apt-repository universe
lsblk -e7
  echo 'lists out the disks information'
echo 'for full disk installation/ installing in the pendrive, go to the folder where you have your extracted file, open it in the terminal and enter this command, replace disk with the disk name e.g: sda6 get disk info by going into gparted/disk application :' 
#sudo bash chromeos-install.sh -src chromeos_filename.bin -dst /dev/disk


mkdir -p ~/tmpmount

sudo mount /dev/part ~/tmpmount

sudo bash chromeos-install.sh -src chromeos_filename.bin -dst ~/tmpmount/chromeos.img -s size
 echo 'here replace size with your disk size info, but keep the number slightly less than the available one: for eg: if your disk size is 75GB then you can type "64"'

#copy the menu entry which will be inside ******

sudo cp /etc/grub.d/40_custom /etc/grub.d/99_brunch

sudo nano /etc/grub.d/99_brunch

sudo update-grub

sudo umount ~/tmpmount

#chromeOS will be now installed

after booting:

The Brunch Configuration Menu can be accessed directly from Grub using the "ChromeOS (settings)" boot option or while logged into ChromeOS using the sudo edit-brunch-config command in the crosh shell.

To access the crosh shell, press Ctrl + Alt + T

echo 'Updating your chromeOS'

Open the Crosh Shell with Crtl + Alt + T and enter shell at the prompt

#Replace brunch_archive.tar.gz and recovery.bin with the file's actual filename

sudo chromeos-update -f ~/Downloads/brunch_archive.tar.gz

Reboot then,

sudo chromeos-update -r ~/Downloads/recovery.bin
 
Or,

sudo chromeos-update -r ~/Downloads/recovery.bin -f ~/Downloads/brunch_archive.tar.gz


Restart ChromeOS after the update finishes

For linux install failure:
This has been successful for fixing the Crostini Linux install failure in ChromeOS 90 and 91:

1. Set this flag to “disabled” - chrome://flags#crostini-use-dlc
2. Reboot your PC
3. Press Ctrl-Alt-T to open crosh
4. Type vmc destroy termina and press enter
5. Try setting up Linux again from the Settings menu

This fix works for ChromeOS 90 and 91, but may not work for ChromeOS 92. If you are having Linux issues with 92 I would suggest installing an older release, setting up Crostini, then update into 92 afterwards.

#for mic fix
Open the crosh shell (ctrl + alt + t) and enter shell at the prompt. 
sudo mkdir -p /var/brunch/bootscripts
Download the file attached to this post
sudo cp ~/Downloads/amixer_mic_fix.sh /var/brunch/bootscripts

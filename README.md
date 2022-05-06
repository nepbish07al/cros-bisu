**CHEAT SHEET FOR ChromeOS installation**

Recommended to read this guide before you start:

https://github.com/sebanc/brunch

>sudo apt update && sudo apt -y install pv cgpt tar unzip

>sudo add-apt-repository universe
>lsblk -e7
 -lists out the disks information

**For full disk installation/ installing in the pendrive**

Go to the folder where you have your extracted file, open it in the terminal and enter this command:
_replace **"disk"** with the disk name **e.g: sda6** 

I hope you have known name of your disk  :' _

>sudo bash chromeos-install.sh -src chromeos_filename.bin -dst /dev/**disk**

**FOR DUAL BOOTING**

>mkdir -p ~/tmpmount

>sudo mount /dev/part ~/tmpmount

replace **part** with the name of your disk where you want to install chromeOS

usage: Supoose you want to install it in **sda7** then your command will be like this:
>sudo mount /dev/**sda6** ~/tmpmount

>sudo bash chromeos-install.sh -src chromeos_filename.bin -dst ~/tmpmount/chromeos.img -s size

Here replace **size** with your disk size info, but keep the number slightly less than the available one: for eg: if your disk size is 75GB then put size little lower than that

example:
>sudo bash chromeos-install.sh -src chromeos_filename.bin -dst ~/tmpmount/chromeos.img -s **64**

Copy both of the menu entry which will be inside ******

Editing thr grub bootloader to add ChromeOS as a option, type the following commands respectively
>sudo cp /etc/grub.d/40_custom /etc/grub.d/99_brunch

>sudo nano /etc/grub.d/99_brunch

>sudo update-grub

>sudo umount ~/tmpmount

#chromeOS will be now installed

**After booting:**

The Brunch Configuration Menu can be accessed directly from Grub using the "ChromeOS (settings)" boot option or while logged into ChromeOS using the following command in crosh shell:

>sudo edit-brunch-config 

To access the crosh shell, press **Ctrl + Alt + T** in chrome browser

**Updating your chromeOS**

Open the Crosh Shell with Crtl + Alt + T and enter shell at the prompt

Download the latest version of brunch and corresponding version of ChromeOS

Rename brunch file as **brunch_archive.tar.gz** and chromeOS bin fine as **recovery.bin**

Copy those renamed file into Downloads if it is not there

type this command:
>sudo chromeos-update -r ~/Downloads/recovery.bin -f ~/Downloads/brunch_archive.tar.gz

>sudo chromeos-update -f ~/Downloads/brunch_archive.tar.gz

Restart ChromeOS after the update finishes

**For linux install failure**

This has been successful for fixing the Crostini Linux install failure in ChromeOS 90 and 91:

1. Set this flag to “disabled” - chrome://flags#crostini-use-dlc
2. Reboot your PC
3. Press Ctrl-Alt-T to open crosh
4. Type vmc destroy termina and press enter
5. Try setting up Linux again from the Settings menu

**For mic fix**

Open the crosh shell (ctrl + alt + t) and enter shell at the prompt.
 
>sudo mkdir -p /var/brunch/bootscripts

Download the file attached to this post

>sudo cp ~/Downloads/amixer_mic_fix.sh /var/brunch/bootscripts

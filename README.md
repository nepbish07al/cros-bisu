<h1> CHEAT SHEET of ChromeOS installation for linux user (debian based) </h1>

This is Not a detailed guide , I actually made this because i felt lazy to go to original repo and read

Detailed guide can be found here: [Orginal repo](https://github.com/sebanc/brunch)

1. Download recovery bin: [cros.tech](cros.tech)

2. Download the **Brunch** file: [latest-release](https://github.com/sebanc/brunch/releases/latest)

**Open the terminal and begin the process:**

`sudo apt update && sudo apt -y install pv cgpt tar unzip`

`sudo add-apt-repository universe`

`lsblk -e7`

 lists out the disks information

**Rename chromeosXXXX(sth).bin file to recovery.bin**

while still being in that folder, right click on any free space to open **menu**, you will see one option which says: **open in terminal**
Do that

**DO NOTE** in the command: _replace_ **"disk"** with the disk name **e.g: sda6** 

I hope you have known name of your disk from above `lsblk -e7` command

`sudo bash chromeos-install.sh -src recovery.bin -dst /dev/**disk**`



**FOR DUAL BOOTING**

`mkdir -p ~/tmpmount`

**DO NOTE** in the command: replace **part** with the name of your disk where you want to install chromeOS

`sudo mount /dev/part ~/tmpmount`

HINT: Supoose you want to install it in **sda7** then your command will be like this:

`sudo mount /dev/**sda6** ~/tmpmount`

>**DO NOTE:** in the command here replace **size** with your disk size info, but keep the number slightly less than the available one: 

for eg: if your disk size is 75GB then put size little lower than that

`sudo bash chromeos-install.sh -src recovery.bin -dst ~/tmpmount/chromeos.img -s size`

example:
>sudo bash chromeos-install.sh -src chromeos_filename.bin -dst ~/tmpmount/chromeos.img -s **64**`

Copy both of the menu entry which will be inside ****** 

To copy anything from terminal always use **Ctrl + shift + C**  If you do **Ctrl + C** in the terminal, it ends the current process of the terminal

**Editing the grub bootloader to add ChromeOS as a option**

type the following commands respectively

`sudo cp /etc/grub.d/40_custom /etc/grub.d/99_brunch`

`sudo nano /etc/grub.d/99_brunch`
 
 HINT: press **Ctrl + O** to save the file and press Enter and press **Ctrl + X** to exit
 
`sudo update-grub` 

`sudo umount ~/tmpmount`

#chromeOS will be now installed


**After booting:**

The Brunch Configuration Menu can be accessed directly from Grub using the "ChromeOS (settings)" boot option or while logged into ChromeOS using the following command in crosh shell:

`sudo edit-brunch-config `

To access the crosh shell, press **Ctrl + Alt + T** in chrome browser

**Updating your chromeOS**

Open the Crosh Shell with Crtl + Alt + T and enter shell at the prompt

Download the latest version of brunch and corresponding version of ChromeOS

Rename brunch file as **brunch_archive.tar.gz** and chromeOS bin fine as **recovery.bin**

Copy those renamed file into Downloads if it is not there

type this command:

`sudo chromeos-update -r ~/Downloads/recovery.bin -f ~/Downloads/brunch_archive.tar.gz`

`sudo chromeos-update -f ~/Downloads/brunch_archive.tar.gz`

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

Download the file attached to this post and type the following code in terminal

`sudo mkdir -p /var/brunch/bootscripts`

>sudo cp ~/Downloads/amixer_mic_fix.sh /var/brunch/bootscripts

# eportfolio-aircrack
This is the repository for my e-Portfolio for the software engineering course 2021/2022. The topic of this presentation is the exploitation of insecure Wifi networks by using [aircrack-ng](https://www.aircrack-ng.org/)
## Setup and requirements
The most important component for performing this attack is a wlan adapter which is able to switch into monitor mode. I'll be using the [Fritzbox wlan stick](https://avm.de/produkte/fritzwlan/fritzwlan-stick-ac-860/) eventhough there are better alternatives for this purpose. 
In addition to that the aircrack toolsuite needs to be installed on your machine. You can do this by following the installation steps from the [official website](https://www.aircrack-ng.org/install.html) or by setting up a virutal machine (my recommendation) which already has all the tools needed and even more handy stuff :) If you need any help during the setup feel free to contact me.  
### Installation using a VM
I use virtual box to run my virtual machine. You can follow the steps from the [official website](https://www.virtualbox.org/wiki/Downloads) to install it. After installing virtualbox you need to download the ISO of the desired operating system. I'll be using [Kali Linux](https://www.kali.org/get-kali/) but other pentesting systems like [Black Arch](https://blackarch.org/downloads.html#ova-download) also work. In addition to that you probably need to install the virtual box [extension pack](https://download.virtualbox.org/virtualbox/6.0.24/Oracle_VM_VirtualBox_Extension_Pack-6.0.24.vbox-extpack) because virtual box can only tunnel USB 1.0 ports by default.
### Installation without VM
After installing aircrack on your machine, you also need to download the [RockYou wordlist](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) which will be used to decrypt the captured handshake. 
## Procedure of the attack

# eportfolio-aircrack
This is the repository for my e-Portfolio for the software engineering course 2021/2022. The topic of this presentation is the exploitation of insecure Wifi networks by using [aircrack-ng](https://www.aircrack-ng.org/). The learnings from this e-Portfolio may only be used on your own networks or networks which explicitly gave you their permission. 
## Setup and requirements
The most important component for performing this attack is a wlan adapter which is able to switch into monitor mode. I'll be using the [Fritzbox wlan stick](https://avm.de/produkte/fritzwlan/fritzwlan-stick-ac-860/) eventhough there are better alternatives for this purpose. 
In addition to that the aircrack toolsuite needs to be installed on your machine. You can do this by following the installation steps from the [official website](https://www.aircrack-ng.org/install.html) or by setting up a virutal machine (my recommendation) which already has all the tools needed and even more handy stuff :) If you need any help during the setup feel free to contact me.  
### Installation using a VM
I use virtual box to run my virtual machine. You can follow the steps from the [official website](https://www.virtualbox.org/wiki/Downloads) to install it. After installing virtualbox you need to download the ISO of the desired operating system. I'll be using [Kali Linux](https://www.kali.org/get-kali/) but other pentesting systems like [Black Arch](https://blackarch.org/downloads.html#ova-download) also work. In addition to that you probably need to install the virtual box [extension pack](https://download.virtualbox.org/virtualbox/6.0.24/Oracle_VM_VirtualBox_Extension_Pack-6.0.24.vbox-extpack) because virtual box can only tunnel USB 1.0 ports by default.
### Installation without VM
After installing aircrack on your machine, you also need to download the [RockYou wordlist](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) which will be used to decrypt the captured handshake. 
## Procedure of the attack
Before starting the attack we have to make sure that our system has access to the wlan stick. We can do this by using the following command.
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/dfb3d33a211d6d7e8340a8ece59a27d010079258/resources/iwconfig.PNG)<br>
We should see our wlan adapter (wlan0) which is in managed mode at the moment. In order to use it for performing the attack we have to change its mode to monitored by using the following command.
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/dfb3d33a211d6d7e8340a8ece59a27d010079258/resources/startMonitorMode.PNG)<br>
After doing this we can use iwconfig again to confirm that the mode changed successfully.
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/dfb3d33a211d6d7e8340a8ece59a27d010079258/resources/iwconfig2.PNG)<br>
Subsequently we can get information about nearby networks by running:
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/1db478798a93447818621f0a61cb4ce770974d57/resources/nearbyNetworks%20(1)-1.png)<br>
The command will give details about every nearby network but I "censored" them due to privacy reasons. Our target network will be "Chakratherapie Rapperich". We need its BSSID and chanel. 
After getting this information, we want to deauthenticate any connected clients. 
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/a8b05bb7b56dbe88dfae1beac603658a0beaf855/resources/deAuth-1.png)</br>
This command by itself can be used as a denial of service attack because it will keep on deauthenticating clients from the network. But we use it because we want the clients to reconnect to the network. That way we can capture the 4-way-handshake which is exchanged when connecting to a network. While running the command above, we also want to listen for the handshake in another terminal.
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/c1ce45a45cc679b60cd2eca07aa69d8629982352/resources/handshakeCapture-1.png)</br>
After capturing a handshake, it is shown in the red box.
The last step is decrypting the captured handshake with the help of a wordlist. One can also decrypt it by using brute force tools like [hashcat](https://hashcat.net/hashcat/). Both of this methods will not work for strong passwords or networks which use different authentification methods. In case of a strong password you will have to try other ways to get the password, like setting up an [evil twin](https://en.wikipedia.org/wiki/Evil_twin_(wireless_networks)) which will not be covered in this e-Portfolio. 
Nevertheless, most routers will probably use weak passwords because most people are not aware of network security. We can try to decrypt the captured handshake by using the rockyou wordlist. This is done by running the following command:
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/aa8c7e6688639533420d9baa6312a8720f2848a7/resources/decryptHandshake-1.png) </br>
And that's it we successfully recovered our routers password. After receiving the password we want to change our wlan adapter to managed mode because we may want to use it as a common adapter again. This is done by running:
<br> ![](https://github.com/tsch4k0mo/eportfolio-aircrack/blob/aa8c7e6688639533420d9baa6312a8720f2848a7/resources/returToManaged.PNG) </br>

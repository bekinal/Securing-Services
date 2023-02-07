<h1>Securing Services</h1>

<h2>Description</h2>
Project consists of making existing installed services more secure. This is accomplished by backing up the Samba configuration file and using port configuration.
<br />


<h2>Utilities Used</h2>

- <b>VirtualBox</b>
- <b>Debian Environment</b>
- <b>Terminal</b>

<h2>Files</h2>

- <b>putty.zip</b>
- <b>WinSCP-5.19.5-Setup</b>

<h2>SSH Hardening:</h2>
SSH will be enahnced and secured by setting connection limitations and port configuration. This project is completed assuming that a VirtualBox machine is used for both Debian and Windows environments; as well as a bridged connection established between the two.
<br />
<br />
On the root user, the SSH service start/status commands are used to verify that SSH is running on the system:<br/>
<img src="https://imagizer.imageshack.com/img922/3113/30wksm.png"
<br />
<br />
The putty.exe file is then opened on the Windows machine:<br/>
<img src="https://imagizer.imageshack.com/img924/296/sNjPQg.png"
<br />
<br />
The IP address is checked in the Debian environment:<br/>
<img src="https://imagizer.imageshack.com/img923/4087/xCQFu4.png"
<br />
<br />
Putty is then started, and the IP for the Debian machine is entered. Port 22 is used:<br/>
<img src="https://imagizer.imageshack.com/img922/8648/iJje2P.png"
<br />
<br />
Yes is selected in this next window:<br/>
<img src="https://imagizer.imageshack.com/img923/5912/tomBGk.png"
<br />
<br />
Credentials for the Debian user are entered:<br/>
<img src="https://imagizer.imageshack.com/img923/2092/ViYwPS.png"
<br />
<br />
After confirming connection to the Debian machine using SSH, the window is closed:<br/>
<img src="https://imagizer.imageshack.com/img923/844/xt1wZO.png"
<br />
<br />
The SSHD config file is opened for editing:<br/>
<img src="https://imagizer.imageshack.com/img923/958/3EV3bq.png"
<br />
<br />
The port is uncommented and changed to 4567 for testing purposes:<br/>
<img src="https://imagizer.imageshack.com/img924/1305/MOXJAA.png"
<br />
<br />
SSH is then restarted and verified as running:<br/>
<img src="https://imagizer.imageshack.com/img922/7269/Thqn49.png"
<br />
<br />
Putty is opened again, this time connecting to the Debian machine through port 4567:<br/>
<img src="https://imagizer.imageshack.com/img923/7646/MczaCY.png"
<br />
<br />
Providing an incorrect username/password 6 times will create an error message:<br/>
<img src="https://imagizer.imageshack.com/img924/594/3hGCz8.png"
<br />
<br />
The SSHD config is opened again in Debain:<br/>
<img src="https://imagizer.imageshack.com/img923/1751/CRbkTl.png"
<br />
<br />
The following line is altered to only allow 3 login attempts before locking the system:<br/>
<img src="https://imagizer.imageshack.com/img922/4367/pVHneH.png"
<br />
<br />
The SSH service is restarted once again:<br/>
<img src="https://imagizer.imageshack.com/img923/4986/Murq8a.png"
<br />
<br />
Using putty again, an incorrect password is entered 3 times. The error message verifies that the changes made are working:<br/>
<img src="https://imagizer.imageshack.com/img924/3999/dtnmGz.png"
<br />
<br />
The config file is opened once more, and default settings are restored:<br/>
<img src="https://imagizer.imageshack.com/img924/640/BTyyQK.png"
<br />
<br />

<h2>WinSCP Obfuscation:</h2>
The port number for the FTP connection will be changed, then connected using WinSCP
<br/>
<br/>
The WinSCP installation is opened in windows:<br/>
<img src="https://imagizer.imageshack.com/img923/6815/eruNQr.png"
<br />
<br />
The vsftpd service is started on the Debian machine:<br/>
<img src="https://imagizer.imageshack.com/img923/3091/3t9YM1.png"
<br />
<br />
In WinSCP, the Debian's IP is entered using port number 21. The login credentials are entered:<br/>
<img src="https://imagizer.imageshack.com/img924/8932/3iyvs0.png"
<br />
<br />
The vsftpd config file is opened for editing:<br/>
<img src="https://imagizer.imageshack.com/img924/7782/PrtmKa.png"
<br />
<br />
The following line is added under listen=NO: listen_port=222:<br/>
<img src="https://imagizer.imageshack.com/img923/4876/F7VZgc.png"
<br />
<br />
The vsftpd service is restarted once more:<br/>
<img src="https://imagizer.imageshack.com/img922/4376/NfX9WQ.png"
<br />
<br />
A new connection is established using port 222:<br/>
<img src="https://imagizer.imageshack.com/img922/7928/jkwBKi.png"
<br />
<br />
The config file is set back to default:<br/>
<img src="https://imagizer.imageshack.com/img922/5449/lbIXLF.png"
<br />
<br />

<h2>Samba Hardening:</h2>
The Samaba configuration file will be backed up. The smb.conf file is opened for editing:<br/>
<img src="https://imagizer.imageshack.com/img924/130/JpllFC.png"
<br/>
<br/>
At the bottom, the guest ok option is set to no. This will prevent anyone from connecting to the share without first providing their credentials:<br/>
<img src="https://imagizer.imageshack.com/img924/743/dGms50.png"
<br/>
<br/>
The smbd service is restarted:<br/>
<img src="https://imagizer.imageshack.com/img923/8295/um8wuP.png"
<br/>
<br/>
In file explorer, the Debian path is entered in the search bar. It can be noted that network credentials are now required:<br/>
<img src="https://imagizer.imageshack.com/img924/5177/m2noz6.png"
<br/>
<br/>
It can also be noted that the user now has read/write access, and can create folders within the directory:<br/>
<img src="https://imagizer.imageshack.com/img924/4765/2bF9ah.png"
<br/>
<br/>
In the config file, read only is set to yes to prevent users from creating files/folders within the directory:<br/>
<img src="https://imagizer.imageshack.com/img924/8365/4MRBt8.png"
<br/>
<br/>
Smbd is restarted once more for the changes to take effect:<br/>
<img src="https://imagizer.imageshack.com/img923/5626/ngVa5P.png"
<br/>
<br/>
Attempting to create a folder now will prompt an Access Deny message:<br/>
<img src="https://imagizer.imageshack.com/img924/6439/bDdbkz.png"
<br/>
<br/>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

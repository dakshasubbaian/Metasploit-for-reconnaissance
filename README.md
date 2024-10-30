### Date:
# Ex-5: Metasploit-for-reconnaissance
## Metasploit
Metasploit for reconnaissance in pentesting

## AIM:

To get introduced to Metasploit Framework and to  perform reconnaissance  in pentesting .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
Find out the ip address of the attackers system
### OUTPUT:
</br>
![1)](https://github.com/user-attachments/assets/9e5560b3-a1b1-4b73-bf6c-a85fcadc2300)


Invoke msfconsole:
</br>
![2)](https://github.com/user-attachments/assets/f624d39a-c3d0-40cf-abcf-4a087e255bc1)




Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
</br>
![3)](https://github.com/user-attachments/assets/75a38085-c0b0-468a-9812-0c09bf50f4f5)



## Port Scanning:
Following command is executed for scanning the systems on our local area network with a TCP scan (-sT) looking for open ports between 1 and 1000 (-p1-1000).
msf >  nmap -sT 192.168.1810/24 -p1-1000
### OUTPUT:
</br>

![4)](https://github.com/user-attachments/assets/d734a267-8f29-4ec0-8588-09f1876b276f)


Step_4:
use the db-nmap command to scan and save the results into Metasploit's postgresql attached database. In that way, you can use those results in the exploitation stage later.

scan the targets with the command db_nmap as follows.
msf > db_nmap 192.168.181.0/24
### OUTPUT:
</br>

![5)](https://github.com/user-attachments/assets/8af6805d-a9a2-4c00-a49d-f66f5d5ac568)



Metasploit has a multitude of scanning modules built in. If we open another terminal, we can navigate to Metasploit's auxiliary modules and list all the scanner modules.
cd /usr/share /metasploit-framework/modules/auxiliary
kali > ls -l
### OUTPUT:
</br>

![6)](https://github.com/user-attachments/assets/2a8c0b01-2813-4793-86d2-f2e9f57d1c83)


Search is a powerful command in Metasploit that you can use to find what you want to locate. 
msf >search name:Microsoft type:exploit

The info command provides information regarding a module or platform,
### OUTPUT:
</br>

![7)](https://github.com/user-attachments/assets/08e08311-a4eb-4ef6-8e0c-7bf7168f5a05)



Before beginning, set up the Metasploit database by starting the PostgreSQL server and initialize msfconsole database as follows:
systemctl start postgresql
msfdb init
## MYSQL ENUMERATION:
Find the IP address of the Metasploitable machine first. Then, use the db_nmap command in msfconsole with Nmap flags to scan the MySQL database at 3306 port.
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>
</br>

![8)](https://github.com/user-attachments/assets/4bc1caf6-0dd0-46dd-bbc0-ca81fae05558)


Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.
search type:auxiliary mysql
</br>

![9)](https://github.com/user-attachments/assets/73277d01-ee64-407a-bc04-5e6056d772ad)


use the auxiliary/scanner/mysql/mysql_version module by typing the module name or associated number to scan MySQL version details.
use 11 Or: use auxiliary/scanner/mysql/mysql_version
</br>
![10)](https://github.com/user-attachments/assets/b8d5e0af-f1ab-4a2f-bd27-f42c084d8b27)



Use the set rhosts command to set the parameter and run the module, as follows:
</br>

![11)](https://github.com/user-attachments/assets/60c01d56-1ad9-47a5-ac9c-2bb661cd824f)



After scanning, you can also brute force MySQL root account via Metasploit's auxiliary(scanner/mysql/mysql_login) module.
</br>

![12)](https://github.com/user-attachments/assets/de30a650-4652-46a2-a089-5eaaf51040a9)


set the PASS_FILE parameter to the wordlist path available inside /usr/share/wordlists:
set PASS_FILE /usr/share/wordlistss/rockyou.txt
Then, specify the IP address of the target machine with the RHOSTS command.
set RHOSTS <metasploitable-ip-address>
Set BLANK_PASSWORDS to true in case there is no password set for the root account.
set BLANK_PASSWORDS true
</br>

![13)](https://github.com/user-attachments/assets/e0a89744-f37f-416f-b7d3-7d6644af92ab)


## RESULT:
The Metasploit framework for reconnaissance is  examined successfully.

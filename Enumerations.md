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


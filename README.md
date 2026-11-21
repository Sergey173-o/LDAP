Научиться настраивать LDAP-сервер и подключать к нему LDAP-клиентов;

## Проверить конфигурацию и запустить сервер

```bash
root@nfsc:~/ldap-lab-centos# 
  vagrant up ipa --provider=virtualbox --no-provision &&
  vagrant ssh ipa -c 'cat /etc/centos-release && hostname -f'
Vagrantfile validated successfully.
Bringing machine 'ipa' up with 'virtualbox' provider...
==> ipa: Box 'otus/centos-stream9' could not be found. Attempting to find and install...
    ipa: Box Provider: virtualbox
    ipa: Box Version: >= 0
==> ipa: Box file was not detected as metadata. Adding it directly...
==> ipa: Adding box 'otus/centos-stream9' (v0) for provider: virtualbox (amd64)
    ipa: Downloading: https://cloud.centos.org/centos/9-stream/x86_64/images/CentOS-Stream-Vagrant-VirtualBox-9-latest.x86_64.vagrant-virtualbox.box
==> ipa: Successfully added box 'otus/centos-stream9' (v0) for 'virtualbox (amd64)'!
==> ipa: Importing base box 'otus/centos-stream9'...
==> ipa: Matching MAC address for NAT networking...
==> ipa: Setting the name of the VM: otus-ldap-centos-ipa
==> ipa: Fixed port collision for 22 => 2222. Now on port 2203.
==> ipa: Clearing any previously set network interfaces...
==> ipa: Preparing network interfaces based on configuration...
    ipa: Adapter 1: nat
    ipa: Adapter 2: intnet
==> ipa: Forwarding ports...
    ipa: 22 (guest) => 2203 (host) (adapter 1)
==> ipa: Running 'pre-boot' VM customizations...
==> ipa: Booting VM...
==> ipa: Waiting for machine to boot. This may take a few minutes...
    ipa: SSH address: 127.0.0.1:2203
    ipa: SSH username: vagrant
    ipa: SSH auth method: private key
    ipa: Warning: Connection reset. Retrying...
    ipa:
    ipa: Vagrant insecure key detected. Vagrant will automatically replace
    ipa: this with a newly generated keypair for better security.
    ipa:
    ipa: Inserting generated public key within guest...
    ipa: Removing insecure key from the guest if it's present...
    ipa: Key inserted! Disconnecting and reconnecting using new SSH key...
==> ipa: Machine booted and ready!
==> ipa: Checking for guest additions in VM...
    ipa: No guest additions were detected on the base box for this VM! Guest
    ipa: additions are required for forwarded ports, shared folders, host only
    ipa: networking, and more. If SSH fails on this machine, please install
    ipa: the guest additions and repackage the box to continue.
    ipa:
    ipa: This is not an error message; everything may continue to work properly,
    ipa: in which case you may ignore this message.
==> ipa: Setting hostname...
==> ipa: Configuring and enabling network interfaces...
==> ipa: Machine not provisioned because `--no-provision` is specified.
CentOS Stream release 9
ipa.otus.lan
root@nfsc:~/ldap-lab-centos#

```



## Установить FreeIPA
TdYGihY!dfsd33cx
TdYGihY!2232d33ds
```bash
read -rsp 'Пароль FreeIPA admin: ' IPA_ADMIN_PASSWORD; echo
read -rsp 'Пароль Directory Manager: ' IPA_DS_PASSWORD; echo
export IPA_ADMIN_PASSWORD IPA_DS_PASSWORD
vagrant provision ipa


root@nfsc:~/ldap-lab-centos# cd ~/ldap-lab-centos
vagrant up ipa --provider=virtualbox --no-provision &&
  vagrant ssh ipa -c 'hostname -f; uptime'
Bringing machine 'ipa' up with 'virtualbox' provider...
==> ipa: Machine not provisioned because `--no-provision` is specified.
ipa.otus.lan
 13:47:45 up 13 min,  1 user,  load average: 1.71, 2.39, 1.73
root@nfsc:~/ldap-lab-centos# vagrant provision ipa &&
  vagrant ssh ipa -c 'sudo -n ipactl status'
==> ipa: Running provisioner: ansible...
    ipa: Running ansible-playbook...

PLAY [Установить сервер FreeIPA] ***********************************************

TASK [Gathering Facts] *********************************************************
ok: [ipa]

TASK [Найти файлы репозиториев] ************************************************
ok: [ipa]

TASK [Использовать прямой репозиторий BaseOS] **********************************
ok: [ipa] => (item={'path': '/etc/yum.repos.d/centos-addons.repo', 'mode': '0644', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 0, 'gid': 0, 'size': 4245, 'inode': 25166330, 'dev': 2052, 'nlink': 1, 'atime': 1780675495.0, 'mtime': 1780675495.0, 'ctime': 1794197470.7903557, 'gr_name': 'root', 'pw_name': 'root', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': True, 'xoth': False, 'isuid': False, 'isgid': False})
changed: [ipa] => (item={'path': '/etc/yum.repos.d/centos.repo', 'mode': '0644', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 0, 'gid': 0, 'size': 2600, 'inode': 25166331, 'dev': 2052, 'nlink': 1, 'atime': 1780675495.0, 'mtime': 1780675495.0, 'ctime': 1794197470.7910342, 'gr_name': 'root', 'pw_name': 'root', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': True, 'xoth': False, 'isuid': False, 'isgid': False})

TASK [Использовать прямой репозиторий AppStream] *******************************
ok: [ipa] => (item={'path': '/etc/yum.repos.d/centos-addons.repo', 'mode': '0644', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 0, 'gid': 0, 'size': 4245, 'inode': 25166330, 'dev': 2052, 'nlink': 1, 'atime': 1780675495.0, 'mtime': 1780675495.0, 'ctime': 1794197470.7903557, 'gr_name': 'root', 'pw_name': 'root', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': True, 'xoth': False, 'isuid': False, 'isgid': False})
changed: [ipa] => (item={'path': '/etc/yum.repos.d/centos.repo', 'mode': '0644', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 0, 'gid': 0, 'size': 2600, 'inode': 25166331, 'dev': 2052, 'nlink': 1, 'atime': 1780675495.0, 'mtime': 1780675495.0, 'ctime': 1794197470.7910342, 'gr_name': 'root', 'pw_name': 'root', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': True, 'xoth': False, 'isuid': False, 'isgid': False})

TASK [Создать каталоги настройки лимитов] **************************************
changed: [ipa] => (item=/etc/ipa)
changed: [ipa] => (item=/etc/systemd/system/pki-tomcatd@pki-tomcat.service.d)

TASK [Установить лимит запуска служб FreeIPA] **********************************
changed: [ipa]

TASK [Установить лимит запуска Dogtag] *****************************************
changed: [ipa]

TASK [Перечитать настройки systemd] ********************************************
ok: [ipa]

TASK [Установить таблицу имён лабораторных ВМ] *********************************
changed: [ipa]

TASK [Установить chrony] *******************************************************
ok: [ipa]

TASK [Запустить синхронизацию времени] *****************************************
ok: [ipa]

TASK [Проверить FQDN] **********************************************************
ok: [ipa]

TASK [Проверить адрес лабораторного интерфейса] ********************************
ok: [ipa] => {
    "changed": false,
    "msg": "All assertions passed"
}

TASK [Проверить состояние настройки FreeIPA] ***********************************
ok: [ipa]

TASK [Проверить наличие разных паролей для первичной установки] ****************
ok: [ipa]

TASK [Установить серверные пакеты] *********************************************
changed: [ipa]

TASK [Настроить сервер FreeIPA] ************************************************
changed: [ipa]

TASK [Проверить состояние firewalld] *******************************************
[WARNING]: Could not get unit files data from systemd: Failed to list unit
files: Connection timed out
ok: [ipa]

TASK [Проверить правило FreeIPA] ***********************************************
skipping: [ipa]

TASK [Добавить правило FreeIPA] ************************************************
skipping: [ipa]

TASK [Перечитать правила] ******************************************************
skipping: [ipa]

TASK [Проверить службы FreeIPA] ************************************************
fatal: [ipa]: FAILED! => {"msg": "Timeout (32s) waiting for privilege escalation prompt: "}

PLAY RECAP *********************************************************************
ipa                        : ok=18   changed=8    unreachable=0    failed=1    skipped=3    rescued=0    ignored=0

Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.

```

```bash
root@nfsc:~/ldap-lab-centos# timeout 1800s vagrant ssh ipa -c '
  nproc
  uptime
  sudo -n ipactl status
'
4
 02:10:30 up 45 min,  1 user,  load average: 1.94, 1.39, 1.80
Directory Service: RUNNING
krb5kdc Service: RUNNING
kadmin Service: RUNNING
httpd Service: RUNNING
ipa-custodia Service: RUNNING
pki-tomcatd Service: RUNNING
ipa-otpd Service: RUNNING
ipa: INFO: The ipactl command was successful
root@nfsc:~/ldap-lab-centos#

```


##  Подключить клиентов через Ansible

В том же терминале, где задан `IPA_ADMIN_PASSWORD`:

```bash
root@nfsc:~/ldap-lab-centos# cd ~/ldap-lab-centos
timeout 900s vagrant ssh client1 -c 'hostname -f; ip -br -4 addr; uptime'
client1.otus.lan
lo               UNKNOWN        127.0.0.1/8
eth0             UP             10.0.2.15/24
eth1             UP             192.168.57.11/24
 02:24:58 up 10 min,  1 user,  load average: 0.99, 2.46, 1.68
root@nfsc:~/ldap-lab-centos# ANSIBLE_TIMEOUT=1800 ANSIBLE_SSH_TIMEOUT=1800 vagrant provision client1
==> client1: Running provisioner: ansible...
    client1: Running ansible-playbook...

PLAY [Подключить клиент FreeIPA] ***********************************************

TASK [Gathering Facts] *********************************************************
ok: [client1]

TASK [Установить таблицу имён лабораторных ВМ] *********************************
changed: [client1]

TASK [Установить chrony] *******************************************************
ok: [client1]

TASK [Запустить синхронизацию времени] *****************************************
ok: [client1]

TASK [Проверить FQDN] **********************************************************
ok: [client1]

TASK [Проверить адрес лабораторного интерфейса] ********************************
ok: [client1] => {
    "changed": false,
    "msg": "All assertions passed"
}

TASK [Установить клиент FreeIPA и LDAP-утилиты] ********************************
changed: [client1]

TASK [Проверить состояние подключения к домену] ********************************
ok: [client1]

TASK [Дождаться HTTPS FreeIPA] *************************************************
ok: [client1]

TASK [Проверить пароль администратора для первого подключения] *****************
ok: [client1]

TASK [Подключить ВМ к домену и включить создание домашних каталогов] ***********
changed: [client1]

TASK [Запустить службу создания домашних каталогов] ****************************
ok: [client1]

TASK [Проверить службу SSSD] ***************************************************
ok: [client1]

PLAY RECAP *********************************************************************
client1                    : ok=13   changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

root@nfsc:~/ldap-lab-centos#
root@nfsc:~/ldap-lab-centos#  vagrant ssh client1 -c 'nproc; hostname -f; systemctl is-active sssd'


4
client1.otus.lan
active
root@nfsc:~/ldap-lab-centos#



```


##  Проверка LDAP, SSSD и Kerberos

TdYGihY!dfsd33cx

   ```bash
   vagrant ssh ipa
Last login: Sat Nov 21 04:09:55 2026 from 10.0.2.2
[vagrant@ipa ~]$ kinit admin
ipa ping
Password for admin@OTUS.LAN:
--------------------------------------------
IPA server version 4.13.4. API version 2.257
--------------------------------------------
[vagrant@ipa ~]$ ipa user-add ipauser --first=Lab --last=User
ipa passwd ipauser
ipa user-show ipauser
TdYGihY!dfsd33cx
--------------------
Added user "ipauser"
--------------------
  User login: ipauser
  First name: Lab
  Last name: User
  Full name: Lab User
  Display name: Lab User
  Initials: LU
  Home directory: /home/ipauser
  GECOS: Lab User
  Login shell: /bin/sh
  Principal name: ipauser@OTUS.LAN
  Principal alias: ipauser@OTUS.LAN
  Email address: ipauser@otus.lan
  UID: 1066800003
  GID: 1066800003
  Password: False
  Member of groups: ipausers
  Kerberos keys available: False
New Password:
Enter New Password again to verify:
---------------------------------------
Changed password for "ipauser@OTUS.LAN"
---------------------------------------
  User login: ipauser
  First name: Lab
  Last name: User
  Home directory: /home/ipauser
  Login shell: /bin/sh
  Principal name: ipauser@OTUS.LAN
  Principal alias: ipauser@OTUS.LAN
  Email address: ipauser@otus.lan
  UID: 1066800003
  GID: 1066800003
  Account disabled: False
  Password: True
  Member of groups: ipausers
  Kerberos keys available: True
[vagrant@ipa ~]$

   ```


   ```bash
root@nfsc:~/ldap-lab-centos#  for vm in client1; do
     echo "=== $vm ==="
     vagrant ssh "$vm" -c 'hostname -f; systemctl is-active sssd && getent passwd ipauser && id ipauser' || break
   done
   vagrant ssh client1 -c "ldapsearch -LLL -x -H ldap://ipa.otus.lan -b '' -s base namingContexts"
=== client1 ===
client1.otus.lan
active
ipauser:*:1066800003:1066800003:Lab User:/home/ipauser:/bin/sh
uid=1066800003(ipauser) gid=1066800003(ipauser) groups=1066800003(ipauser)
dn:
namingContexts: dc=otus,dc=lan
namingContexts: cn=changelog
namingContexts: o=ipaca

root@nfsc:~/ldap-lab-centos#

   ```
TdYGihY!dfsd33cx2
   ```bash
 root@nfsc:~/ldap-lab-centos# vagrant ssh client1
Last login: Sat Nov 21 04:35:39 2026 from 10.0.2.2
[vagrant@client1 ~]$ kinit ipauser
   klist
   su - ipauser
   id
   pwd
Password for ipauser@OTUS.LAN:
Password expired.  You must change it now.
Enter new password:
Enter it again:
Password mismatch.  Please try again.
Enter new password:
Enter it again:
Ticket cache: KCM:1000
Default principal: ipauser@OTUS.LAN

Valid starting     Expires            Service principal
11/21/26 04:42:00  11/22/26 04:31:50  krbtgt/OTUS.LAN@OTUS.LAN
Password:
Creating home directory for ipauser.
[ipauser@client1 ~]$ TdYGihY!dfsd33cx2^C
[ipauser@client1 ~]$ exit
logout
uid=1000(vagrant) gid=1000(vagrant) groups=1000(vagrant) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
/home/vagrant
[vagrant@client1 ~]$


   ```

# nano /etc/systemd/system/rc-local.service

Kemudian isi file tersebut dengan konfigurasi seperti berikut :
[Unit]
Description=/etc/rc.local
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target

#Simpan file, kemudian selanjutnya adalah membuat file rc.local pada direktori /etc.
# nano /etc/rc.local

Berikut adalah default isi dari file rc.local

#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

exit 0

Tambahkan permission execute pada file rc.local tersebut.
root@diaryconfig:~# chmod +x /etc/rc.local

Kemudian aktifkan service rc-local.
root@diaryconfig:~# systemctl enable rc-local
Created symlink /etc/systemd/system/multi-user.target.wants/rc-local.service ? /etc/systemd/system/rc-local.service.

# systemctl start rc-local 
# systemctl status rc-local

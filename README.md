# 脚本

修复PVE更新/去订阅/添加CPU温度显示

    cd /tmp/ && rm -rf fix.sh && wget --no-check-certificate https://raw.githubusercontent.com/pkpkgtr1/PVE-Fix/master/fix.sh && chmod +x fix.sh && sh fix.sh 
    
   
如需开机启动,则运行下列命令:
cat > /etc/systemd/system/rc-local.service <<EOF
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
EOF


cat > /etc/rc.local <<EOF
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
hddtemp -d /dev/sd?
exit 0
EOF

chmod +x /etc/rc.local&systemctl enable rc-local&systemctl start rc-local.service







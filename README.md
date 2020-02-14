```
sysctl -w net.ipv6.conf.all.disable_ipv6=1
cat <<EOF > /etc/sysctl.d/disable-ipv6.conf
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
EOF

sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
setenforce 0

systemctl disable firewalld
systemctl stop firewalld


cat <<EOF > /etc/profile.d/mc_xoria256.sh
if [[ $TERM == 'xterm-256color' ]];then
  alias mc="mc -S xoria256"
fi
EOF


```

```
systemctl start smb
systemctl enable smb
```












```
#version=DEVEL
# System authorization information
auth --enableshadow --passalgo=sha512
# Use graphical install
graphical
# Run the Setup Agent on first boot
firstboot --enable
ignoredisk --only-use=sda
# Keyboard layouts
keyboard --vckeymap=us --xlayouts='us','ru' --switch='grp:ctrl_shift_toggle'
# System language
lang ru_RU.UTF-8

# Network information
network  --bootproto=dhcp --device=eth0 --ipv6=auto --activate
network  --hostname=localhost.localdomain

# Use network installation
url --url="http://mirror.docker.ru/centos/7/os/x86_64"
# Root password
rootpw --iscrypted $6$UKK5itLMW.mrB5xD$jwpqP/YGdUZ6oxE8XEEliFDD/
# System services
services --enabled="chronyd"
# System timezone
timezone Europe/Moscow --isUtc
# System bootloader configuration
bootloader --append=" crashkernel=auto" --location=mbr --boot-drive=sda
autopart --type=lvm
# Partition clearing information
clearpart --none --initlabel

%packages
@^minimal
@core
chrony
kexec-tools

%end

%addon com_redhat_kdump --enable --reserve-mb='auto'

%end

%anaconda
pwpolicy root --minlen=6 --minquality=1 --notstrict --nochanges --notempty
pwpolicy user --minlen=6 --minquality=1 --notstrict --nochanges --emptyok
pwpolicy luks --minlen=6 --minquality=1 --notstrict --nochanges --notempty
%end


```


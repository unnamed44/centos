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




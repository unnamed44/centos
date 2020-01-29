```
sysctl -w net.ipv6.conf.all.disable_ipv6=1
echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf 
echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf

sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
setenforce 0

systemctl disable firewalld
systemctl stop firewalld

```

```
systemctl start smb
systemctl enable smb
```


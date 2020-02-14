```
sysctl -w net.ipv6.conf.all.disable_ipv6=1
echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.d/disable-ipv6.conf 
echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.d/disable-ipv6.conf

sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
setenforce 0

systemctl disable firewalld
systemctl stop firewalld

```

```
systemctl start smb
systemctl enable smb
```



```
/etc/profile.d/mc_xoria256.sh
if [[ $TERM == 'xterm-256color' ]];then
  alias mc="mc -S xoria256"
fi


```



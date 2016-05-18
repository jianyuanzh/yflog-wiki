---
title: "CentOSwe为SNMP添加Snmp v3账户"
date: 2016-05-18 09:02
---
使用如下命令为snmp添加一个v3用户：
```
service snmpd stop
net-snmp-config --create-snmpv3-user -ro -a testPassWord -x DES -X testPassWord vincent
```

在添加v3用户之前，首先要确保`snmpd`服务被停止，否则会报如下异常:
```
Apparently at least one snmpd demon is already running.
You must stop them in order to use this command.
```

添加用户后，启动`snmpd`。可以使用下面的命令去测试是否添加成功：
```
[root@vincent local]# snmpwalk -v3 -l authPriv -a MD5 -A testPassWord -x DES -X testPassWord -u vincent 127.0.0.1 .1.3.6.1.2.1.1.1.0
SNMPv2-MIB::sysDescr.0 = STRING: Linux vincent.logicmonitor.com 2.6.32-573.12.1.el6.x86_64 #1 SMP Tue Dec 15 21:19:08 UTC 2015 x86_64
```

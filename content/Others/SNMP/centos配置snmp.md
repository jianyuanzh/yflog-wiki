---
title: "CentOS配置SNMP"
date: 2016-04-22 13:42
---

首先安装必要的包
```
 yum install -y net-snmp net-snmp-devel net-snmp-libs net-snmp-per mrtg
```

修改`/etc/snmp/snmpd.conf`, 添加的内容如下：
```
com2sec notConfigUser  default       public
rocommunity6 LogicMan fe80::/64
rocommunity LogicMan yflog
rocommunity LogicMan 127.0.0.0/8
rocommunity LogicMan 0.0.0.0/0
rouser lmdev
```

最后启动`snmpd`服务，并设置开机启动
```
service snmpd start
chkconfig snmpd on
```

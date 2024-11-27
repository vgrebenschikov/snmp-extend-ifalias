# Add reporting of interface description for net-snmp

## Overview

This is instruction how to extend results of net-mgmt/net-snmp IF-MIB with
interface descriptions.

## Installation 

```sh

# install -m 0755 -o root -g wheel pass-persist-ifalias /usr/local/bin/

# echo "
# .1.3.6.1.2.1.31.1.1.1.18 -> IF-MIB::ifAlias
pass_persist .1.3.6.1.2.1.31.1.1.1.18 /usr/local/bin/pass-persist-ifalias
" >> /usr/local/etc/snmpd.conf

# service snmpd restart

```

## How to check if it was installed

Check if description set on some of interfaces:

```sh

# ifconfig
...
epair1a: flags=1008943<UP,BROADCAST,RUNNING,PROMISC,SIMPLEX,MULTICAST,LOWER_UP> metric 0 mtu 1500
	description: www-eth0
...
epair2a: flags=1008943<UP,BROADCAST,RUNNING,PROMISC,SIMPLEX,MULTICAST,LOWER_UP> metric 0 mtu 1500
	description: postgres-eth0
...
epair3a: flags=1008943<UP,BROADCAST,RUNNING,PROMISC,SIMPLEX,MULTICAST,LOWER_UP> metric 0 mtu 1500
	description: zabbix-eth0
...
```

Validate that results are returned with snmpwalk:

```sh
# snmpwalk -v 2c -c public localhost IF-MIB::ifAlias
...
IF-MIB::ifAlias.7 = STRING: www-eth0
IF-MIB::ifAlias.8 = STRING: postgres-eth0
IF-MIB::ifAlias.9 = STRING: zabbix-eth0
...
```

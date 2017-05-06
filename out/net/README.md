# Network devices
See root [README](https://github.com/v-zhuravlev/zbx_template_pack) for idea behind this template pack.  
## Devices List  
|Vendor|Known Models|OS|Known SNMP ObjectID|Template name|MIBS used|Reference|  
|----|-----|----|-----|------|---------|----------|    
|Juniper|	MX,SRX,EX models|JunOS|.1.3.6.1.4.1.636.1.1.1.2.[29,39]|Template Juniper|JUNIPER-MIB|-|  
|D-Link DES-xxxx|D-Link DES-xxxx|-|.1.3.6.1.4.1.171.10.113.3.1|Template D-Link DES|DLINK-AGENT-MIB,EQUIPMENT-MIB|-|
|D-Link DES-7xxx|D-Link DES-7206|-|.1.3.6.1.4.1.171.10.97.1.1|Template D-Link DES 7200|ENTITY-MIB,MY-SYSTEM-MIB,MY-PROCESS-MIB,MY-MEMORY-MIB|-|
|Cisco|-|IOS|.1.3.6.1.4.1.9.1.\[1045,1208,896,864\]|Template Cisco IOS Software releases 12.2\_3.5\_ or later|CISCO-PROCESS-MIB,CISCO-MEMORY-POOL-MIB,CISCO-ENVMON-MIB|<http://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/15216-contiguous-memory.html> , <http://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/15215-collect-cpu-util-snmp.html>|  
|Cisco|-|IOS|.1.3.6.1.4.1.9.1.\[1045,1208,896,864\]|Template Cisco IOS Software releases later to 12.0\_3\_T and prior to 12.2\_3.5\_|CISCO-PROCESS-MIB,CISCO-MEMORY-POOL-MIB,CISCO-ENVMON-MIB|<http://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/15216-contiguous-memory.html>, <http://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/15215-collect-cpu-util-snmp.html>|  
|Cisco|-|IOS|.1.3.6.1.4.1.9.1.\[1045,1208,896,864\]|Template Cisco IOS Software releases prior to 12.0\_3\_T|OLD-CISCO-CPU-MIB,CISCO-MEMORY-POOL-MIB|<http://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/15216-contiguous-memory.html>, <http://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/15215-collect-cpu-util-snmp.html>|  
|Mikrotik|-|RouterOS|.1.3.6.1.4.1.14988.1|Template Mikrotik|MIKROTIK-MIB,HOST-RESOURCES-MIB|-|  
|Ubiquiti|NanoBridge,NanoStation,Unifi|AirOS|.1.3.6.1.4.1.10002.1|Template Ubiquiti AirOS|FROGFOOT-RESOURCES-MIB,IEEE802dot11-MIB|-|  
|QTech|Qtech QSW-2800-28T|-|.1.3.6.1.4.1.27514.1.1.1.49|Template QTech QSW|QTECH-MIB,ENTITY-MIB|-|  
|Extreme|	X670V-48x|EXOS|.1.3.6.1.4.1.1916.2.168|Template Extreme EXOS|	EXTREME-SYSTEM-MIB,EXTREME-SOFTWARE-MONITOR-MIB|-|  
|Alcatel|ALCATEL SR 7750|TiMOS|.1.3.6.1.4.1.6527.1.3.4|Template Alcatel Timetra TiMOS|EXTREME-SYSTEM-MIB,EXTREME-SOFTWARE-MONITOR-MIB|https://share.zabbix.com/network_devices/extreme/template-extreme-x450a|  
|Brocade FC Switch|-|-|.1.3.6.1.4.1.1588.2.1.1.[1,71]|Template Brocade|SW-MIB,ENTITY-MIB|-|  
|Huawei VRP|	S2352P-EI|-|.1.3.6.1.4.1.2011.2.23.94|Template Huawei VRP|ENTITY-MIB,HUAWEI-ENTITY-EXTENT-MIB|-|  


## Items supported by template  
 
|Metric type|Application|key|name|units|required|Source type|note|inventory_link|  
|----|----|----|----|----|----|----|----|----|  
|Performance|CPU|__system.cpu.util__|CPU utilization|%|Y|SNMP|-|
||
|Performance|Memory|__vm.memory.pused__|Memory utilization|%|Y|SNMP/Calculated|-|
|Performance|Internal items|vm.memory.used|Memory units|-|N|SNMP|Inerited from 'Template HOST-RESOURCES-MIB'|
|Performance|Internal items|vm.memory.units.used|Used memory in units|units|N|SNMP|Inerited from 'Template HOST-RESOURCES-MIB'|
|Performance|Internal items|vm.memory.units.total|Total memory in units|units|N|SNMP|Inerited from 'Template HOST-RESOURCES-MIB'|
|Performance|Memory|memory_used|vm.memory.used|B|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Performance|Memory|memory_free|vm.memory.free|B|N|SMMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Performance|Memory|memory_total|vm.memory.total|B|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
||
|Fault|TBD|__icmpping__|ICMP ping|-|Y|Simple check|Inherited from 'Template ICMP ping'|
|Fault|Temperature|__sensor.temp.value__|Temperature|C|Y|SNMP|-|
|Fault|Temperature|sensor.temp.status|Temperature status|-|N|SNMP|-|
|Fault|Temperature|sensor.temp.locale|Temperature sensor location|-|N|SNMP|-|
|Fault|Power Supply|sensor.psu.status|Power supply status|-|N|SNMP|-|
|Fault|Fans|sensor.fan.status|Fan status|-|N|SNMP|-|
|Fault|Fans|sensor.fan.speed|Fan speed|rpm|N|SNMP|-|
|Fault|Status|system.status|Overall system health status|-|N|SNMP|-|
|Fault|Storage|vfs.fs.pused|Storage utilization|%|N|SNMP/Calculated|-|
|Fault|Internal items|vfs.fs.units|Storage units|-|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Fault|Internal items|vfs.fs.units.used|Used storage in units|units|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Fault|Internal items|vfs.fs.units.total|Total space in units|units|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Fault|Storage|vfs.fs.used|Used space|B|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Fault|Storage|vfs.fs.free|Free space|B|N|SMMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
|Fault|Storage|vfs.fs.total|Total space|B|N|SNMP|Could be inherited from 'Template HOST-RESOURCES-MIB'|
||
|Fault|General|__system.uptime__|Device uptime|uptime|Y|SNMP|Inerited|
|Fault|General|__snmptrap.fallback__|SNMP traps (fallback)|-|Y|SNMP|Inerited|
||
|Inventory|General|__system.name__|Device name|-|Y|SNMP|Inerited|3|
|Inventory|General|__system.contact__|Device contact details|-|Y|SNMP|Inerited|23|
|Inventory|General|__system.objectid__|System object ID|-|Y|SNMP|Inerited|
|Inventory|General|__system.description__|Device description|-|Y|SNMP|Inerited|14|
|Inventory|General|__system.location__|Device location|-|Y|SNMP|Inerited|24|
||
|Inventory|Inventory|__system.hw.model__|Hardware model name|-|Y|SNMP|-|model(29)|
|Inventory|Inventory|__system.hw.serialnumber__|Hardware serial number|-|Y|SNMP|-|serial_noa(8)|
|Inventory|Inventory|system.sw.os|Operating system|-|N|SNMP|-|5|
|Inventory|Inventory|system.hw.firmware|Firmware version|-|N|SNMP|-|-|
|Inventory|Inventory|system.hw.version|Hardware revision|-|N|SNMP|-|-|

__Internal items__ application is for metrics only required to calculate other metrics. Metrics in __Internal items__ application should be hidden from Latest data view, if possible.


## Supported triggers and events

The following USER MACROS are defined in Device class template in order to allow fine tune of end device template or end device.  
  * {$CPU_LOAD_MAX}=90  
  * {$MEMORY_UTIL_MAX}=90  
  * {$TEMP_WARN}=50  
  * {$TEMP_CRIT}=60  
  * {$TEMP_CRIT_LOW}=5  
  * {$STORAGE_UTIL_CRIT}=90  
  * {$STORAGE_UTIL_WARN}=80  
  * {$SNMP_TIMEOUT}=600  
 And they can be redefined on host level if needed  

Some other MACROSES could be seen in templates if some optional triggers are defined:      
  * {$HEALTH_DISASTER_STATUS}
  * {$HEALTH_CRIT_STATUS}
  * {$HEALTH_WARN_STATUS}

```need to be updated```

|Metric type|Application|trigger_id|name|expression|recovery_expression|severity|required|Tags|dependsOn|Manual close|  
|---|---|---|---|---|---|---|---|---|---|---|  
|Performance|CPU|cpu.util.high|CPU utilization is too high|system.cpu.util.avg(300)>{$CPU_UTIL_MAX}|-|Average(3)|Y|-|-|  
|Performance|Memory|memory_util_high|Memory utilization is too high|memory_used_percent.avg(300)>90|-|Average(3)|Y|-|-|  
||  
|Fault|Storage|storage_crit|Free disk space is less than 10% on $LOCATION|storage_used_percent.avg(300)>90|-|Average(3)|N|-|-|  
|Fault|Storage|storage_warn|Free disk space is less than 20% on $LOCATION|storage_used_percent.avg(300)>80|-|Warning(2)|N|-|storage_crit|  
|Fault|Temperature|temp_crit|[$LOCATION] temperature is above critical threshold: >{$TEMP_CRIT:"$LOCATION"}|temperature_value.avg(300)}>{$TEMP_CRIT:"$LOCATION"}|-|Average(3)|Y|Temperature|-|  
|Fault|Temperature|temp_warn|[$LOCATION] temperature is above warninig threshold: >{$TEMP_WARN:"$LOCATION"}|temperature_value.avg(300)}>{$TEMP_WARN:"$LOCATION"}|-|Warning(2)|Y|Temperature|temp_crit|  
||  
|Fault|Status|health_disaster|System is in unrecoverable state!|overall_status.last(0)}={$HEALTH_DISASTER_STATUS}|-|Disaster(5)|N|-|-|  
|Fault|Status|health_critical|System status is in critical state|overall_status.last(0)}={$HEALTH_CRIT_STATUS}|-|High(4)|N|-|health_disaster|  
|Fault|Status|health_warning|System status is in warning state|overall_status.last(0)}={$HEALTH_WARN_STATUS}|-|Warning(2)|N|-|health_critical|  
||  
|Fault|General|noping|{HOST.NAME} is unavailable by ICMP|icmpping.max(#3)=0|-|Average(3)|Y|-|-|N|  
|Fault|General|uptime_nodata|No SNMP data collection|sysUptime.nodata({$SNMP_TIMEOUT})}=1|-|Warning(2)|Y|-|noping|N|  
|Fault|General|uptime_restarted|The {HOST.NAME} has just been restarted|sysUptime.last(0)<600 or snmpTrapFallback.str(coldStart)}=1|sysUptime.last(0)}>600 or sysUptime.nodata(1800)=1|Warning(2)|N|-|-|Y|  
||  
|Inventory|Inventory|sn_changed|Device serial number has been changed|serial_number.diff(0)=1|-|Warning(2)|Y|-|-|ONLY MANUAL CLOSE|  
|Inventory|Inventory|firmware_changed|Device firmware has been changed|firmware_version.diff(0)=1|-|Warning(2)|N|-|-|ONLY MANUAL CLOSE| 

## Translations
Most Templates' items and triggers are also provided with translation in Russian. Use templates with `RU` suffix instead of `EN`.  

## Import  
Import templates from `deps` with RU or EN suffix depending on translation you need first.  
Also there is a dependency on default `Template ICMP Ping`  
Then import required templates from `net` directory.  

You can also use script provided to mass import the templates like so:
- in Centos:  
`yum install perl-JSON-XS perl-libwww-perl perl-LWP-Protocol-https`
- or in Debian:  
`apt-get install libwww-perl libjson-xs-perl`

- Then do:  
```git clone --recursive https://github.com/v-zhuravlev/zbx_template_pack.git
cd zbx_template_pack/bin
```


```
[user@host bin]$ perl import-templates.pl -u Admin -p zabbix --lang EN ../out/deps/3.2        
template_deps_host_resources_SNMPv1_EN.xml  
template_deps_host_resources_SNMPv2_EN.xml  
template_deps_system_snmp_SNMPv1_EN.xml  
template_deps_system_snmp_SNMPv2_EN.xml  
```


```
[user@host tmon bin]$ perl import-templates.pl -u Admin -p mypass --lang EN ../out/net/3.2  
template_net_cisco_SNMPv1_EN.xml  
template_net_cisco_SNMPv2_EN.xml  
template_net_dlink_des_SNMPv1_EN.xml  
template_net_dlink_des_SNMPv2_EN.xml  
template_net_juniper_SNMPv1_EN.xml  
template_net_juniper_SNMPv2_EN.xml  
template_net_mikrotik_SNMPv1_EN.xml  
template_net_mikrotik_SNMPv2_EN.xml  
template_net_ubiquiti_airos_SNMPv1_EN.xml  
template_net_ubiquiti_airos_SNMPv2_EN.xml
```


## Where are the network interfaces?  
Not here yet. Just attach regular SNMP Interfaces template to the template from this pack for now.

## Known issues  
- For some devices temperature sensors are discovered using LLD. Since too many sensors are discovered and no dependencies could be created between them, it could lead  to event storm in case if room cooling system is broken.Same problem could be faced with multi CPU network devices.  
- Sometimes additional LLD rules are used when they are not strictly necessary. This is done on purpose to provide same names to metrics of same Location (like `Temperature[Ambient]`).  

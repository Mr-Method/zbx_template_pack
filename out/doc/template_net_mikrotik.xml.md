## Template Net Mikrotik_SNMPvX
Template Net Mikrotik version: 0.14<br>MIBs used:<br>HOST-RESOURCES-MIB<br>MIKROTIK-MIB<br>Known Issues:<br>description : Doesn't have ifHighSpeed filled. fixed in more recent versions<br>version : RotuerOS 6.28 or lower<br>device : description : Doesn't have any temperature sensors<br>version : RotuerOS 6.38.5<br>device : Mikrotik 941-2nD, Mikrotik 951G-2HnD


## Templates links
- Template Module Generic_SNMPvX

## Discovery rules

| Name | Key | SNMP OID | Description |
|------|-----|----------|-------------|
| Storage Discovery | storage.discovery | discovery[{#SNMPVALUE},1.3.6.1.2.1.25.2.3.1.3,{#ALLOC_UNITS},1.3.6.1.2.1.25.2.3.1.4,{#STORAGE_TYPE},1.3.6.1.2.1.25.2.3.1.2] | HOST-RESOURCES-MIB::hrStorage discovery with storage filter |


## Items
| Application | Discovery Rule | Name | Key | SNMP OID | Description | Documentation | Type |
|-------------|----------------|------|-----|----------|-------------|---------------|------|
| CPU | CPU Discovery | #{#SNMPINDEX}: CPU utilization | system.cpu.util[hrProcessorLoad.{#SNMPINDEX}] | 1.3.6.1.2.1.25.3.3.1.2.{#SNMPINDEX} | MIB: HOST-RESOURCES-MIB<br>The average, over the last minute, of the percentage of time that this processor was not idle.Implementations may approximate this one minute smoothing period if necessary.<br> |  | snmp |
| Memory |  | Used memory | vm.memory.used[hrStorageUsed.Memory] | 1.3.6.1.2.1.25.2.3.1.6.65536 | MIB: HOST-RESOURCES-MIB<br>The amount of the storage represented by this entry that is allocated, in units of hrStorageAllocationUnits.<br> |  | snmp |
| Memory |  | Total memory | vm.memory.total[hrStorageSize.Memory] | 1.3.6.1.2.1.25.2.3.1.5.65536 | MIB: HOST-RESOURCES-MIB<br>The size of the storage represented by this entry, in<br>units of hrStorageAllocationUnits. This object is<br>writable to allow remote configuration of the size of<br>the storage area in those cases where such an<br>operation makes sense and is possible on the<br>underlying system. For example, the amount of main<br>memory allocated to a buffer pool might be modified or<br>the amount of disk space allocated to virtual memory<br>might be modified.<br> |  | snmp |
| Memory |  | Memory utilization | vm.memory.pused[memoryUsedPercentage.Memory] |  | Memory utilization in %<br> |  | calculated |
| Temperature |  | Device: Температура | sensor.temp.value[mtxrHlTemperature] | 1.3.6.1.4.1.14988.1.1.3.10.0 | MIB: MIKROTIK-MIB<br>(mtxrHlTemperature) Device temperature in Celsius (degrees C). Might be missing in entry models (RB750, RB450G..)<br>Reference: http://wiki.mikrotik.com/wiki/Manual:SNMP<br> |  | snmp |
| Storage | Storage Discovery | Disk-{#SNMPINDEX}: Used space | vfs.fs.used[hrStorageSize.{#SNMPINDEX}] | 1.3.6.1.2.1.25.2.3.1.6.{#SNMPINDEX} | MIB: HOST-RESOURCES-MIB<br>The amount of the storage represented by this entry that is allocated, in units of hrStorageAllocationUnits.<br> |  | snmp |
| Storage | Storage Discovery | Disk-{#SNMPINDEX}: Total space | vfs.fs.total[hrStorageSize.{#SNMPINDEX}] | 1.3.6.1.2.1.25.2.3.1.5.{#SNMPINDEX} | MIB: HOST-RESOURCES-MIB<br>The size of the storage represented by this entry, in<br>units of hrStorageAllocationUnits. This object is<br>writable to allow remote configuration of the size of<br>the storage area in those cases where such an<br>operation makes sense and is possible on the<br>underlying system. For example, the amount of main<br>memory allocated to a buffer pool might be modified or<br>the amount of disk space allocated to virtual memory<br>might be modified.<br> |  | snmp |
| Storage | Storage Discovery | Disk-{#SNMPINDEX}: Storage utilization | vfs.fs.pused[hrStorageSize.{#SNMPINDEX}] |  | Storage utilization in % for Disk-{#SNMPINDEX}<br> |  | calculated |
| Inventory |  | Operating system | system.sw.os | 1.3.6.1.4.1.14988.1.1.4.4.0 | MIB: MIKROTIK-MIB<br>Software version<br> |  | snmp |
| Inventory |  | Модель | system.hw.model | 1.3.6.1.2.1.1.1.0 | <br> |  | snmp |
| Inventory |  | Серийный номер | system.hw.serialnumber | 1.3.6.1.4.1.14988.1.1.7.3.0 | MIB: MIKROTIK-MIB<br>RouterBOARD serial number<br> |  | snmp |
| Inventory |  | Версия прошивки | system.hw.firmware | 1.3.6.1.4.1.14988.1.1.7.4.0 | MIB: MIKROTIK-MIB<br>Current firmware version<br> |  | snmp |

## Triggers

| Name  | Expression | Recovery Expression | Documentation  | Description | Severity |
|-------|------------|---------------------|----------------|-------------|----------|
| #{#SNMPINDEX}: Высокая загрузка процессора | {TEMPLATE_NAME:system.cpu.util[hrProcessorLoad.{#SNMPINDEX}].avg(5m)}>{$CPU_UTIL_MAX} |  | If alarmObject is defined, it's added to trigger name. | Last value: {ITEM.LASTVALUE1}.<br> | <span style="background-color:#FFA059;">Average(3)</span> |
| Мало свободной памяти ОЗУ | {TEMPLATE_NAME:vm.memory.pused[memoryUsedPercentage.Memory].avg(5m)}>{$MEMORY_UTIL_MAX} |  |  | Last value: {ITEM.LASTVALUE1}.<br> | <span style="background-color:#FFA059;">Average(3)</span> |
| Device: Температура слишком низкая: <{$TEMP_CRIT_LOW:"Device"} | {TEMPLATE_NAME:sensor.temp.value[mtxrHlTemperature].avg(5m)}<{$TEMP_CRIT_LOW:"Device"} | {TEMPLATE_NAME:sensor.temp.value[mtxrHlTemperature].min(5m)}>{$TEMP_CRIT_LOW:"Device"}+3 | Using recovery expression... Temperature has to be 3 points more than threshold level  ({$TEMP_CRIT_LOW}+3) | Last value: {ITEM.LASTVALUE1}.<br> | <span style="background-color:#FFA059;">Average(3)</span> |
| Disk-{#SNMPINDEX}: Мало свободного места | {TEMPLATE_NAME:vfs.fs.pused[hrStorageSize.{#SNMPINDEX}].avg(5m)}>{$STORAGE_UTIL_WARN} |  |  | Last value: {ITEM.LASTVALUE1}.<br> | <span style="background-color:#FFC859;">Warning(2)</span> |
| Возможно замена устройства (получен новый серийный номер) | {TEMPLATE_NAME:system.hw.serialnumber.diff()}=1 and {TEMPLATE_NAME:system.hw.serialnumber.strlen()}>0 |  |  | Последнее значение: {ITEM.LASTVALUE1}.<br>Изменился серийный номер устройства. Подтвердите и закройте. | <span style="background-color:#7499FF;">Info(1)</span> |
| Версия прошивки изменилась | {TEMPLATE_NAME:system.hw.firmware.diff()}=1 and {TEMPLATE_NAME:system.hw.firmware.strlen()}>0 |  |  | Последнее значение: {ITEM.LASTVALUE1}.<br>Версия прошивки изменилась. Подтвердите и закройте. | <span style="background-color:#7499FF;">Info(1)</span> |

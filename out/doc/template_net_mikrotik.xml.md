## Template Net Mikrotik_SNMPvX
Template Net Mikrotik version: 0.14<br>            MIBs used:<br>            HOST-RESOURCES-MIB<br>            MIKROTIK-MIB<br>            Known Issues:<br>            description : Doesn't have ifHighSpeed filled. fixed in more recent versions<br>            version : RotuerOS 6.28 or lower<br>            device : description : Doesn't have any temperature sensors<br>            version : RotuerOS 6.38.5<br>            device : Mikrotik 941-2nD, Mikrotik 951G-2HnD


## Templates links
- Template Module Generic_SNMPvX

## Discovery rules

| Name | SNMP OID | Description |
|------|----------|-------------|
| Storage Discovery | discovery[{#SNMPVALUE},1.3.6.1.2.1.25.2.3.1.3,{#ALLOC_UNITS},1.3.6.1.2.1.25.2.3.1.4,{#STORAGE_TYPE},1.3.6.1.2.1.25.2.3.1.2] | HOST-RESOURCES-MIB::hrStorage discovery with storage filter |


## Items
| Application | Name | Key | SNMP OID |
|-------------|------|-----|----------|
| CPU | #{#SNMPINDEX}: CPU utilization | system.cpu.util[hrProcessorLoad.{#SNMPINDEX}] | 1.3.6.1.2.1.25.3.3.1.2.{#SNMPINDEX} |
| Memory | Used memory | vm.memory.used[hrStorageUsed.Memory] | 1.3.6.1.2.1.25.2.3.1.6.65536 |
| Memory | Total memory | vm.memory.total[hrStorageSize.Memory] | 1.3.6.1.2.1.25.2.3.1.5.65536 |
| Memory | Memory utilization | vm.memory.pused[memoryUsedPercentage.Memory] |  |
| Temperature | Device: Температура | sensor.temp.value[mtxrHlTemperature] | 1.3.6.1.4.1.14988.1.1.3.10.0 |
| Storage | Disk-{#SNMPINDEX}: Used space | vfs.fs.used[hrStorageSize.{#SNMPINDEX}] | 1.3.6.1.2.1.25.2.3.1.6.{#SNMPINDEX} |
| Storage | Disk-{#SNMPINDEX}: Total space | vfs.fs.total[hrStorageSize.{#SNMPINDEX}] | 1.3.6.1.2.1.25.2.3.1.5.{#SNMPINDEX} |
| Storage | Disk-{#SNMPINDEX}: Storage utilization | vfs.fs.pused[hrStorageSize.{#SNMPINDEX}] |  |
| Inventory | Operating system | system.sw.os | 1.3.6.1.4.1.14988.1.1.4.4.0 |
| Inventory | Модель | system.hw.model | 1.3.6.1.2.1.1.1.0 |
| Inventory | Серийный номер | system.hw.serialnumber | 1.3.6.1.4.1.14988.1.1.7.3.0 |
| Inventory | Версия прошивки | system.hw.firmware | 1.3.6.1.4.1.14988.1.1.7.4.0 |

## Triggers

| Name  | Expression |
|-------|------------|
| #{#SNMPINDEX}: Высокая загрузка процессора |**Expression**:{TEMPLATE_NAME:system.cpu.util[hrProcessorLoad.{#SNMPINDEX}].avg(5m)}>{$CPU_UTIL_MAX}<br>**Recovery**: <br>**Severity:** <span style="background-color:#FFA059;">Average(3)</span> |
| Мало свободной памяти ОЗУ |**Expression**:{TEMPLATE_NAME:vm.memory.pused[memoryUsedPercentage.Memory].avg(5m)}>{$MEMORY_UTIL_MAX}<br>**Recovery**: <br>**Severity:** <span style="background-color:#FFA059;">Average(3)</span> |
| Device: Температура слишком низкая: <{$TEMP_CRIT_LOW:"Device"} |**Expression**:{TEMPLATE_NAME:sensor.temp.value[mtxrHlTemperature].avg(5m)}<{$TEMP_CRIT_LOW:"Device"}<br>**Recovery**:{TEMPLATE_NAME:sensor.temp.value[mtxrHlTemperature].min(5m)}>{$TEMP_CRIT_LOW:"Device"}+3 <br>**Severity:** <span style="background-color:#FFA059;">Average(3)</span> |
| Disk-{#SNMPINDEX}: Мало свободного места |**Expression**:{TEMPLATE_NAME:vfs.fs.pused[hrStorageSize.{#SNMPINDEX}].avg(5m)}>{$STORAGE_UTIL_WARN}<br>**Recovery**: <br>**Severity:** <span style="background-color:#FFC859;">Warning(2)</span> |
| Возможно замена устройства (получен новый серийный номер) |**Expression**:{TEMPLATE_NAME:system.hw.serialnumber.diff()}=1 and {TEMPLATE_NAME:system.hw.serialnumber.strlen()}>0<br>**Recovery**: <br>**Severity:** <span style="background-color:#7499FF;">Info(1)</span> |
| Версия прошивки изменилась |**Expression**:{TEMPLATE_NAME:system.hw.firmware.diff()}=1 and {TEMPLATE_NAME:system.hw.firmware.strlen()}>0<br>**Recovery**: <br>**Severity:** <span style="background-color:#7499FF;">Info(1)</span> |

## Template Net Mikrotik_SNMPvX
Template Net Mikrotik version: 0.14<br>            MIBs used:<br>            HOST-RESOURCES-MIB<br>            MIKROTIK-MIB<br>            Known Issues:<br>            description : Doesn't have ifHighSpeed filled. fixed in more recent versions<br>            version : RotuerOS 6.28 or lower<br>            device : description : Doesn't have any temperature sensors<br>            version : RotuerOS 6.38.5<br>            device : Mikrotik 941-2nD, Mikrotik 951G-2HnD


## Templates links
- Template Module Generic_SNMPvX

## Discovery rules

| Name | Key | SNMP OID | Description |
|------|-----|----------|-------------|
| Storage Discovery | storage.discovery | discovery[{#SNMPVALUE},1.3.6.1.2.1.25.2.3.1.3,{#ALLOC_UNITS},1.3.6.1.2.1.25.2.3.1.4,{#STORAGE_TYPE},1.3.6.1.2.1.25.2.3.1.2] | HOST-RESOURCES-MIB::hrStorage discovery with storage filter |


## Items

<table>
    <tr>
        <th>Application</th>
        <th>Discovery Rule</th>
        <th>Name</th>
        <th>Key</th>
        <th>SNMP OID</th>
        <th>Description</th>
        <th>Documentation</th>
        <th>Type</th>
    </tr>
    <tr>
        <td>CPU</td>
        <td>CPU Discovery</td>
        <td>#{#SNMPINDEX}: CPU utilization</td>
        <td>system.cpu.util[hrProcessorLoad.{#SNMPINDEX}]</td>
        <td>1.3.6.1.2.1.25.3.3.1.2.{#SNMPINDEX}</td>
        <td><small>MIB: HOST-RESOURCES-MIB<br>                    The average, over the last minute, of the percentage of time that this processor was not idle.Implementations may approximate this one minute smoothing period if necessary.<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Memory</td>
        <td></td>
        <td>Used memory</td>
        <td>vm.memory.used[hrStorageUsed.Memory]</td>
        <td>1.3.6.1.2.1.25.2.3.1.6.65536</td>
        <td><small>MIB: HOST-RESOURCES-MIB<br>                    The amount of the storage represented by this entry that is allocated, in units of hrStorageAllocationUnits.<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Memory</td>
        <td></td>
        <td>Total memory</td>
        <td>vm.memory.total[hrStorageSize.Memory]</td>
        <td>1.3.6.1.2.1.25.2.3.1.5.65536</td>
        <td><small>MIB: HOST-RESOURCES-MIB<br>                    The size of the storage represented by this entry, in<br>                    units of hrStorageAllocationUnits. This object is<br>                    writable to allow remote configuration of the size of<br>                    the storage area in those cases where such an<br>                    operation makes sense and is possible on the<br>                    underlying system. For example, the amount of main<br>                    memory allocated to a buffer pool might be modified or<br>                    the amount of disk space allocated to virtual memory<br>                    might be modified.<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Memory</td>
        <td></td>
        <td>Memory utilization</td>
        <td>vm.memory.pused[memoryUsedPercentage.Memory]</td>
        <td></td>
        <td><small>Memory utilization in %<br>                </small></td>
        <td><small></small></td>
        <td>calculated</td>
    </tr>
    <tr>
        <td>Temperature</td>
        <td></td>
        <td>Device: Температура</td>
        <td>sensor.temp.value[mtxrHlTemperature]</td>
        <td>1.3.6.1.4.1.14988.1.1.3.10.0</td>
        <td><small>MIB: MIKROTIK-MIB<br>                    (mtxrHlTemperature) Device temperature in Celsius (degrees C). Might be missing in entry models (RB750, RB450G..)<br>                    Reference: http://wiki.mikrotik.com/wiki/Manual:SNMP<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Storage</td>
        <td>Storage Discovery</td>
        <td>Disk-{#SNMPINDEX}: Used space</td>
        <td>vfs.fs.used[hrStorageSize.{#SNMPINDEX}]</td>
        <td>1.3.6.1.2.1.25.2.3.1.6.{#SNMPINDEX}</td>
        <td><small>MIB: HOST-RESOURCES-MIB<br>                    The amount of the storage represented by this entry that is allocated, in units of hrStorageAllocationUnits.<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Storage</td>
        <td>Storage Discovery</td>
        <td>Disk-{#SNMPINDEX}: Total space</td>
        <td>vfs.fs.total[hrStorageSize.{#SNMPINDEX}]</td>
        <td>1.3.6.1.2.1.25.2.3.1.5.{#SNMPINDEX}</td>
        <td><small>MIB: HOST-RESOURCES-MIB<br>                    The size of the storage represented by this entry, in<br>                    units of hrStorageAllocationUnits. This object is<br>                    writable to allow remote configuration of the size of<br>                    the storage area in those cases where such an<br>                    operation makes sense and is possible on the<br>                    underlying system. For example, the amount of main<br>                    memory allocated to a buffer pool might be modified or<br>                    the amount of disk space allocated to virtual memory<br>                    might be modified.<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Storage</td>
        <td>Storage Discovery</td>
        <td>Disk-{#SNMPINDEX}: Storage utilization</td>
        <td>vfs.fs.pused[hrStorageSize.{#SNMPINDEX}]</td>
        <td></td>
        <td><small>Storage utilization in % for Disk-{#SNMPINDEX}<br>                </small></td>
        <td><small></small></td>
        <td>calculated</td>
    </tr>
    <tr>
        <td>Inventory</td>
        <td></td>
        <td>Operating system</td>
        <td>system.sw.os</td>
        <td>1.3.6.1.4.1.14988.1.1.4.4.0</td>
        <td><small>MIB: MIKROTIK-MIB<br>                    Software version<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Inventory</td>
        <td></td>
        <td>Модель</td>
        <td>system.hw.model</td>
        <td>1.3.6.1.2.1.1.1.0</td>
        <td><small><br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Inventory</td>
        <td></td>
        <td>Серийный номер</td>
        <td>system.hw.serialnumber</td>
        <td>1.3.6.1.4.1.14988.1.1.7.3.0</td>
        <td><small>MIB: MIKROTIK-MIB<br>                    RouterBOARD serial number<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
    <tr>
        <td>Inventory</td>
        <td></td>
        <td>Версия прошивки</td>
        <td>system.hw.firmware</td>
        <td>1.3.6.1.4.1.14988.1.1.7.4.0</td>
        <td><small>MIB: MIKROTIK-MIB<br>                    Current firmware version<br>                </small></td>
        <td><small></small></td>
        <td>snmp</td>
    </tr>
</table>


## Triggers

<table width="100%">
    <tr>
        <th>Name</th>
        <th>Expression</th>
        <th>Documentation</th>
        <th>Description</th>
        <th>Severity</th>
    </tr>
    <tr>
        <td>#{#SNMPINDEX}: Высокая загрузка процессора</td>
        <td><strong>Expression</strong>:<small>{TEMPLATE_NAME:system.cpu.util[hrProcessorLoad.{#SNMPINDEX}].avg(5m)}>{$CPU_UTIL_MAX}</small><br><strong>Recovery</strong>:<small></small></td>
        <td><small>If alarmObject is defined, it's added to trigger name.</small></td>
        <td><small>Last value: {ITEM.LASTVALUE1}.<br>                        </small></td>
        <td style="background-color:#FFA059;">Average(3)</td>
    </tr>
    <tr>
        <td>Мало свободной памяти ОЗУ</td>
        <td><strong>Expression</strong>:<small>{TEMPLATE_NAME:vm.memory.pused[memoryUsedPercentage.Memory].avg(5m)}>{$MEMORY_UTIL_MAX}</small><br><strong>Recovery</strong>:<small></small></td>
        <td><small></small></td>
        <td><small>Last value: {ITEM.LASTVALUE1}.<br>                        </small></td>
        <td style="background-color:#FFA059;">Average(3)</td>
    </tr>
    <tr>
        <td>Device: Температура слишком низкая: <{$TEMP_CRIT_LOW:"Device"}</td>
        <td><strong>Expression</strong>:<small>{TEMPLATE_NAME:sensor.temp.value[mtxrHlTemperature].avg(5m)}<{$TEMP_CRIT_LOW:"Device"}</small><br><strong>Recovery</strong>:<small>{TEMPLATE_NAME:sensor.temp.value[mtxrHlTemperature].min(5m)}>{$TEMP_CRIT_LOW:"Device"}+3</small></td>
        <td><small>Using recovery expression... Temperature has to be 3 points more than threshold level  ({$TEMP_CRIT_LOW}+3)</small></td>
        <td><small>Last value: {ITEM.LASTVALUE1}.<br>                        </small></td>
        <td style="background-color:#FFA059;">Average(3)</td>
    </tr>
    <tr>
        <td>Disk-{#SNMPINDEX}: Мало свободного места</td>
        <td><strong>Expression</strong>:<small>{TEMPLATE_NAME:vfs.fs.pused[hrStorageSize.{#SNMPINDEX}].avg(5m)}>{$STORAGE_UTIL_WARN}</small><br><strong>Recovery</strong>:<small></small></td>
        <td><small></small></td>
        <td><small>Last value: {ITEM.LASTVALUE1}.<br>                        </small></td>
        <td style="background-color:#FFC859;">Warning(2)</td>
    </tr>
    <tr>
        <td>Возможно замена устройства (получен новый серийный номер)</td>
        <td><strong>Expression</strong>:<small>{TEMPLATE_NAME:system.hw.serialnumber.diff()}=1 and {TEMPLATE_NAME:system.hw.serialnumber.strlen()}>0</small><br><strong>Recovery</strong>:<small></small></td>
        <td><small></small></td>
        <td><small>Последнее значение: {ITEM.LASTVALUE1}.<br>                            Изменился серийный номер устройства. Подтвердите и закройте.</small></td>
        <td style="background-color:#7499FF;">Info(1)</td>
    </tr>
    <tr>
        <td>Версия прошивки изменилась</td>
        <td><strong>Expression</strong>:<small>{TEMPLATE_NAME:system.hw.firmware.diff()}=1 and {TEMPLATE_NAME:system.hw.firmware.strlen()}>0</small><br><strong>Recovery</strong>:<small></small></td>
        <td><small></small></td>
        <td><small>Последнее значение: {ITEM.LASTVALUE1}.<br>                            Версия прошивки изменилась. Подтвердите и закройте.</small></td>
        <td style="background-color:#7499FF;">Info(1)</td>
    </tr>
</table>
## Macros used

|Name|Description|Default|Type|
|----|-----------|-------|----|
|{$STRATUM}|Stratum of NTP Server|`1`|Text macro|
|{$SYNCSORCE}|SyncSource of NTP Server|`1`|Text macro|

## Template links

There are no template links in this template.

## Discovery rules

There are no discovery rules in this template.

## Items collected

|Name|Description|Type|Key and additional info|
|----|-----------|----|----|
|ntpLeapIndicator|NTP:Leap indicator condition.|`SNMP agent`|SPI-timeServer-MIB.ntpLeapIndicator|
|ntpPrecision|NTP:Accuracy.|`SNMP agent`|SPI-timeServer-MIB.ntpPrecision|
|ntpRootDispersion|NTP:Root dispersion.|`SNMP agent`|SPI-timeServer-MIB.ntpRootDispersion|
|ntpRootDistance|NTP:Root distance.|`SNMP agent`|SPI-timeServer-MIB.ntpRootDistance|
|ntpStratum|NTP:Stratum number.|`SNMP agent`|SPI-timeServer-MIB.ntpStratum|
|ntpSystemPeer|NTP:Address of system peer.|`SNMP agent`|SPI-timeServer-MIB.ntpSystemPeer|
|ntpSystemPeerMode|NTP:Mode of system peer.|`SNMP agent`|SPI-timeServer-MIB.ntpSystemPeerMode|
|timeServerErrno|Error code.|`SNMP agent`|SPI-timeServer-MIB.timeServerErrno|
|ts25ErrorCode|TS-2500 series:last error number.|`SNMP agent`|SPI-timeServer-MIB.ts25ErrorCode|
|ts25ErrorMessage|TS-2500 series:last error message.|`SNMP agent`|SPI-timeServer-MIB.ts25ErrorMessage|
|ts25ErrorTime|TS-2500 series:last error timestamp.|`SNMP agent`|SPI-timeServer-MIB.ts25ErrorTime|
|ts25gpsAltitude|TS-2500 series GPS:The altitude acquireal from GPS satellites.|`SNMP agent`|SPI-timeServer-MIB.ts25gpsAltitude|
|ts25gpsAntenna|TS-2500 series GPS:Anntena condition.<p>1 : Normal<p>Other than 1 : Abnormal|`SNMP agent`|SPI-timeServer-MIB.ts25gpsAntenna|
|ts25gpsCount|TS-2500 series GPS:Number of the satellites being used.|`SNMP agent`|SPI-timeServer-MIB.ts25gpsCount|
|ts25gpsLatitude|TS-2500 series GPS:Latitude acquireal from GPS satellites.|`SNMP agent`|SPI-timeServer-MIB.ts25gpsLatitude|
|ts25gpsLongitude|TS-2500 series GPS:The longitude acquireal from GPS satellites.|`SNMP agent`|SPI-timeServer-MIB.ts25gpsLongitude|
|ts25gpsState|TS-2500 series GPS:PPS signal condition.<p>1 : Normal<p>Other than 1 : Abnormal|`SNMP agent`|SPI-timeServer-MIB.ts25gpsState|
|ts25hdBattery|TS-2500 series:Battery voltage condition.|`SNMP agent`|SPI-timeServer-MIB.ts25hdBattery|
|ts25hdFan|TS-2500 series:Fan sensor condition.|`SNMP agent`|SPI-timeServer-MIB.ts25hdFan|
|ts25hdTemperature1|TS-2500 series:No.1 temperature sensor condition.|`SNMP agent`|SPI-timeServer-MIB.ts25hdTemperature1|
|ts25hdTemperature2|TS-2500 series:No.2 temperature sensor condition.|`SNMP agent`|SPI-timeServer-MIB.ts25hdTemperature2|
|ts25tjjyDelayTime|TS-2500 series TJJY:response delay time.|`SNMP agent`|SPI-timeServer-MIB.ts25tjjyDelayTime|
|ts25tjjyInterval|TS-2500 series TJJY:phone call interval.|`SNMP agent`|SPI-timeServer-MIB.ts25tjjyInterval|
|ts25tjjySignalTime|TS-2500 series TJJY:phone call time.|`SNMP agent`|SPI-timeServer-MIB.ts25tjjySignalTime|
|ts25tjjySyncErrCount|TS-2500 series TJJY:last phone call error count.|`SNMP agent`|SPI-timeServer-MIB.ts25tjjySyncErrCount|
|tsProduct|Product name.|`SNMP agent`|SPI-timeServer-MIB.tsProduct|
|tsSyncCondition|Synchronizing condition.<p>  1: GPS, TJJY<p>  2: Local clock<p>  3: Backup NTP serve<p>  9: Unsynchronized|`SNMP agent`|SPI-timeServer-MIB.tsSyncCondition|
|tsSyncSource|Synchronizing state.|`SNMP agent`|SPI-timeServer-MIB.tsSyncSource|
|tsTimeDifference|Time difference from UTC.|`SNMP agent`|SPI-timeServer-MIB.tsTimeDifference|
|tsTimeSource|Time source.|`SNMP agent`|SPI-timeServer-MIB.tsTimeSource|
|tsVerMain|Main system version.|`SNMP agent`|SPI-timeServer-MIB.tsVerMain|
|tsVerSub|Sub system version.|`SNMP agent`|SPI-timeServer-MIB.tsVerSub

## Triggers

|Name|Description|Expression|Priority|
|----|-----------|----------|--------|
|TS-2850: gps antenna error|GPS antenna failure|<p>**Expression**: in(last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.ts25gpsAntenna),1)=0</p><p>**Recovery expression** in(last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.ts25gpsAntenna),1)=1|Disaster|
|TS-2850: ntp error|NTP server is no longer in Strutum1|<p>**Expression**: in(last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.ntpStratum),1)<>{$STRATUM}</p><p>**Recovery expression** in(last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.ntpStratum),1)={$STRATUM}|Disaster|
|TS-2850: Synchronized error|Number of satellites acquired is less than 3|<p>**Expression**: last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.ts25gpsCount)<3</p><p>**Recovery expression** last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.ts25gpsCount)>=3|Warning|
|TS-2850: timesource(GPS) error|The time source has been changed|<p>**Expression**: last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.tsSyncSource)<>{$SYNCSORCE}</p><p>**Recovery expression** last(/SEIKO TS-2850 by SNMP/SPI-timeServer-MIB.tsSyncSource)={$SYNCSORCE}|High|
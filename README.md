# zabbix_get_jmx

### Requirements
python3
jq

### Install
```
wget -P /usr/bin/ https://raw.githubusercontent.com/alchuk/zabbix_get_jmx/master/zabbix_get_jmx
```
```
chmod +x /usr/bin/zabbix_get_jmx
```

### Usage
```
zabbix_get_jmx --help
```
```
usage: zabbix_get_jmx [-h] [--java-gateway-host JAVA_GATEWAY_HOST]
                      [--java-gateway-port JAVA_GATEWAY_PORT]
                      [--jmx-server JMX_SERVER] [--jmx-port JMX_PORT]
                      [--key KEY] [--jmx-user JMX_USER] [--jmx-pass JMX_PASS]
                      [--jmx-protocol JMX_PROTOCOL]

optional arguments:
  -h, --help            show this help message and exit
  --java-gateway-host JAVA_GATEWAY_HOST
  --java-gateway-port JAVA_GATEWAY_PORT
  --jmx-server JMX_SERVER
  --jmx-port JMX_PORT
  --key KEY
  --jmx-user JMX_USER
  --jmx-pass JMX_PASS
  --jmx-protocol JMX_PROTOCOL
```
Where:  
JAVA_GATEWAY_HOST: usually zabbix-server or zabbix-proxy host  
JAVA_GATEWAY_PORT: usually 10052  
JMX_SERVER: your JMX-enabled target host  
JMX_PROTOCOL: remote|remote+https|etc  

### Example zabbix_get_jmx
Test discovery Garbage collector **
```
zabbix_get_jmx --java-gateway-host HOST_WITH_INSTALLED_GW --java-gateway-port 10052 --jmx-server MONITORED_HOST --jmx-port 4447 --jmx-user USER --jmx-pass ZABBIX --jmx-protocol remote+https --key 'jmx.discovery[beans,"*:type=GarbageCollector,name=*"]' | jq '.data[0].value | fromjson | .data'
```
Output:
```
[
  {
    "{#JMXDOMAIN}": "java.lang",
    "{#JMXTYPE}": "GarbageCollector",
    "{#JMXOBJ}": "java.lang:type=GarbageCollector,name=PS MarkSweep",
    "{#JMXNAME}": "PS MarkSweep"
  },
  {
    "{#JMXDOMAIN}": "java.lang",
    "{#JMXTYPE}": "GarbageCollector",
    "{#JMXOBJ}": "java.lang:type=GarbageCollector,name=PS Scavenge",
    "{#JMXNAME}": "PS Scavenge"
  }
]
```

### Usage simple script
Test discovery Garbage collector
```
./zabbix_get_jmx.sh 'jmx.discovery[beans,"*:type=GarbageCollector,name=*"]'
```
Output:
```
[
  {
    "{#JMXDOMAIN}": "java.lang",
    "{#JMXTYPE}": "GarbageCollector",
    "{#JMXOBJ}": "java.lang:type=GarbageCollector,name=PS MarkSweep",
    "{#JMXNAME}": "PS MarkSweep"
  },
  {
    "{#JMXDOMAIN}": "java.lang",
    "{#JMXTYPE}": "GarbageCollector",
    "{#JMXOBJ}": "java.lang:type=GarbageCollector,name=PS Scavenge",
    "{#JMXNAME}": "PS Scavenge"
  }
]
```
[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=GEH7YJEBWTFWE&currency_code=USD&source=url)

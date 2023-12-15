# pfSense
Version 17.9

## System
| Option | Value |
| ------ | ----- |
| hostname | fw2 |
| domain | avkare.com |
| timeservers | 0.pfsense.pool.ntp.org |
| timezone | Etc/GMT-5 |
| language | en_US |
| dnsserver | 8.8.8.8, 8.8.4.4 |

## Interfaces
| Name | Enabled | Description | Interface | Address | Subnet |
| ---- | ------- | ----------- | --------- | ------- | ------ |
| lan | x |  | igb1 | 10.2.1.252 | 24 |
| opt1 | x | Karol_Ann | igb2 | 192.168.2.252 | 24 |
| opt2 |  | OPT2 | igb3 |  |  |
| wan | x | WAN | igb0 | 66.38.37.125 | 23 |

## Gateways
| Default | Name | Interface | Gateway | Weight | IP | Description |
| ------- | ---- | --------- | ------- | ------ | --- | ----------- |
| x | WANGW | [wan](#interfaces "WAN") | 66.38.36.1 | 1 | inet | WAN Gateway |

## DHCP ranges
### DHCPd configuration for lan
| Option | Value |
| ------ | ----- |
| enable |  |
| defaultleasetime |  |
| maxleasetime |  |

#### Ranges
| From | To |
| ---- | --- |
| 10.2.1.60 | 10.2.1.200 |

### DHCPd configuration for [opt1](#interfaces "Karol_Ann")
| Option | Value |
| ------ | ----- |
| enable | x |
| defaultleasetime |  |
| maxleasetime |  |

#### Ranges
| From | To |
| ---- | --- |
| 192.168.2.50 | 192.168.2.200 |


## Aliases
| Name | Type | Address | Description | Detail |
| ---- | ---- | ------- | ----------- | ------ |
| AK_P10 | network | 10.0.1.0/24 |  | Entry added Thu, 24 Aug 2017 01:03:04 +0500 |
| Milke | network | 192.168.45.0/24 |  | Entry added Thu, 24 Aug 2017 01:03:23 +0500 |
| NetGainIT | network | 72.250.162.188/32 165.227.180.232/32 | NetGain IT (Contractor) | NetGainIT Lexington Office\|\|NetGainIT Jake's Home Office |
| Oracle_LAN | network | 192.168.100.0/24 |  | Entry added Thu, 24 Aug 2017 01:02:39 +0500 |
| Pulaski_LANs | network | 10.1.1.0/24 10.1.2.0/24 10.1.99.0/24 10.0.60.0/24 |  | LAN\|\|Phones\|\|ARMS\|\|SSLVPN |
| Sweeney | network | 10.10.10.0/24 |  | Entry added Thu, 24 Aug 2017 01:03:38 +0500 |

## Filter rules
| Disabled | Interface | Type | IP | Protocol | Source | Destination | Description |
| -------- | --------- | ---- | --- | -------- | ------ | ----------- | ----------- |
|  | [wan](#interfaces "WAN") | pass | inet | icmp | any | [wanip](#interfaces "WAN") |  |
|  | [wan](#interfaces "WAN") | pass | inet | tcp | [NetGainIT](#aliases "72.250.162.188/32 165.227.180.232/32") | 66.38.37.125 | NetGain IT (Contractor) |
| x | [wan](#interfaces "WAN") | pass | inet | tcp | 192.168.0.0/20 | 10.2.1.0/24 | S2S tunnel from AKFR to AVKRS Azure |
|  | lan | pass | inet |  | [opt1](#interfaces "Karol_Ann") | lan | Allow Karol Ann to LAN |
|  | lan | pass | inet |  | lan | any | Default allow LAN to any rule |
|  | lan | pass | inet6 |  | lan | any | Default allow LAN IPv6 to any rule |
|  | enc0 | pass | inet |  | [Pulaski_LANs](#aliases "10.1.1.0/24 10.1.2.0/24 10.1.99.0/24 10.0.60.0/24") | lan |  |
| x | enc0 | pass | inet |  | [Sweeney](#aliases "10.10.10.0/24") | lan |  |
| x | enc0 | pass | inet |  | [Milke](#aliases "192.168.45.0/24") | lan |  |
|  | enc0 | pass | inet |  | [AK_P10](#aliases "10.0.1.0/24") | lan |  |
|  | enc0 | pass | inet |  | [Oracle_LAN](#aliases "192.168.100.0/24") | lan |  |
|  | [opt1](#interfaces "Karol_Ann") | pass | inet |  | [opt1](#interfaces "Karol_Ann") | any | Allow Karol Ann to any |

## Syslog configuration
| Option | Value |
| ------ | ----- |
| enable |  |
| logall |  |
| logfilesize |  |
| nentries |  |
| remoteserver |  |
| remoteserver2 |  |
| remoteserver3 |  |
| sourceip |  |
| ipproto |  |


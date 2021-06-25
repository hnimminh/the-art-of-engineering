
# CISCO CONFIGURATION NOTES

## BASIC
* Enable interactive `enable`
* Show Device configuration `show run-config`
* Access onfiguration terminal `configure terminal`
* Save configuration: `write memory`
* Disable domain lookup per conmand `no ip domain-lookup`

.
## ENABLE <span style="color:red">DEBUG</span>
```
configure terminal
enable > config term
logging buffer 4096
exit
terminal monitor
debug ccsip message | error | 
```

## TFTP BACKUP & RESTORE
* Select interface for TFTP:```ip tftp source-interface GigabitEthernet0/0/0```

### BACKUP
```
copy running-config tftp
Address or name of remote host []? 10.10.10
Destination filename [cisco-sw-minh-config]? cisco-sw-minh-config-2020-01-02

Search for and remove any line that starts with "AAA" in configuration file.
```
### RESTORE
```
copy tftp running-config
Address or name of remote host []? 10.10.10
Source filename []?cisco-sw-minh-config-2020-01-02
Destination filename [running-config]? 
```
### SSH ACCESS
```
username admin password mypassword
username admin privilege 15
ip domain-name github.com
crypto key generate rsa (1024)
ip ssh rsa keypair-name sshkeys
crypto key generate rsa usage-keys label sshkeys modulus 1024
line vty 0 4
 	login local
 		transport input SSH
ip ssh version 2
ip ssh time-out 60
```

## FIRWARE UPGRATE VIA USB/TFTP
```
dir flash:
copy usbflash0:cat3k_caa-universalk9.16.09.03a.SPA.bin flash:
copy tftp://<ip_address>/cat3k_caa-universalk9.16.06.07.SPA.bin flash
verify /md5 (flash:cat3k_caa-universalk9.16.09.03a.SPA.bin) = ff792a1c4a260db9c7c6f40d2a04206d
configure terminal
boot system flash:cat3k_caa-universalk9.16.09.03a.SPA.bin
exit
write memory
reload
```
## DELETE FILE:
```
delete <path>
delete flash:outupdate_script.gs
```

## RTU LICENSE
```
license right-to-use active ipservices acceptEULA
reload
```

## STATUS
```
show ip sockets
show interface status/summay/stat , 
systat
show user
show tcp brief
clear line tvy
```

## AS BGP
```
router bgp <SELF_ASN>
 bgp log-neighbor-changes
 network <that_advertise_to_remote_side_ex_10.0.0.0> mask <that_advertise_to_remote_side_ex_255.255.255.0>
 neighbor <REMOTE_IP_INTERFACE> remote-as <REMOTE_ASN>
 neighbor <REMOTE_IP_INTERFACE> password <REMOTE_PASSWORD>
 ```
 
## SSH Access By Private Key
```
username minh privilege 15

ip ssh pubkey-chain
  username minh
   key-hash ssh-rsa <public_key>
```

## LOST CONFIG 
https://www.cisco.com/c/en/us/support/docs/routers/2500-series-routers/6201-lose-config-6201.html
```
0x2142 --> 0x2102
#config-register 0x2102
#show version
Configuration register is 0x2142 (will be 0x2102 at next reload)
```

## ACL: ACCESS CONTROL LIST
```
access-list <list_id> permit <ip_address>
access-list <list_id> permit <network> <net_wildcard>
```
## ACCESS CLASS
```
line vty <vty_id> <privilege_level>
 access-class <class_id> in/out
```
## INTERFACE ACCESS GROUP
```
interface <interface>
 ip access-group <group_id> in/out
```


## QoS Management
```
configure terminal

policy-map NODROP_POLICY
 class class-default
  bandwidth percent 100
  queue-buffers ratio 100
end

interface GigabitEthernet 1/0/24
 service-policy output NODROP_POLICY

qos queue-softmax-multiplier 1200

show platform hardware fed switch 1 qos queue stats interface gigabitEthernet 1/0/24
show platform hardware fed switch 1 qos queue config interface gigabitEthernet 1/0/24
clear counters
show interface counter error
show platform hardware fed switch 1 qos queue config interface gigabitEthernet 1/0/24

DATA Port:26 GPN:24 AFD:Disabled FlatAFD:Disabled QoSMap:0 HW Queues: 208 - 215
  DrainFast:Disabled PortSoftStart:3 - 6480
----------------------------------------------------------
   DTS  Hardmax  Softmax   PortSMin  GlblSMin  PortStEnd
  ----- --------  --------  --------  --------  ---------
 0   1  5   120   7  2880   6   320   0     0   4  8640
 1   1  4     0   8  4320   3   480   2   180   4  8640
 2   1  4     0   5     0   5     0   0     0   4  8640
 3   1  4     0   5     0   5     0   0     0   4  8640
 4   1  4     0   5     0   5     0   0     0   4  8640
 5   1  4     0   5     0   5     0   0     0   4  8640
 6   1  4     0   5     0   5     0   0     0   4  8640
 7   1  4     0   5     0   5     0   0     0   4  8640
 Priority   Shaped/shared   weight  shaping_step  sharpedWeight
 --------   -------------   ------  ------------   -------------
 0      0     Shared            50           0           0
 1      0     Shared            75           0           0
 2      0     Shared         10000           0           0
 3      0     Shared         10000           0           0
 4      0     Shared         10000           0           0
 5      0     Shared         10000           0           0
 6      0     Shared         10000           0           0
 7      0     Shared         10000           0           0

   Weight0 Max_Th0 Min_Th0 Weigth1 Max_Th1 Min_Th1  Weight2 Max_Th2 Min_Th2
   ------- ------- ------- ------- ------- -------  ------- ------- ------
 0       0    2390       0       0    2671       0       0    3000       0
 1       0    3442       0       0    3847       0       0    4320       0
 2       0       0       0       0       0       0       0       0       0
 3       0       0       0       0       0       0       0       0       0
 4       0       0       0       0       0       0       0       0       0
 5       0       0       0       0       0       0       0       0       0
 6       0       0       0       0       0       0       0       0       0
 7       0       0       0       0       0       0       0       0       0
 ```
 
 ###  SERIAL NUMBER MAP TO PRODUCT ID
 ```https://cway.cisco.com/sncheck/```
 
### FACTORY RESET
```
#write erase 
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
Erase of nvram: complete
*May  5 06:46:14.551: %SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
System configuration has been modified. Save? [yes/no]: yes
#reload
Proceed with reload? [confirm]
```
### LOG
```
service timestamps log datetime show-timezone
logging trap informational
logging on
logging buffered 4096
logging moniter
logging origin-id hostname
logging source-interface Vlan10
logging host 172.21.4.172 transport tcp port 514
```

### PCAP
```
monitor capture CBUF buffer size 20 match any interface range GigabitEthernet 0/0/0-2 both
monitor capture CBUF start
monitor capture CBUF stop
show monitor capture CBUF buffer brief
monitor capture CBUF export tftp://x.x.x.x/CBUF.pcap
```

### ROUTER GET RESOURCE
```
#show platform software status control-processor brief
Load Average
 Slot Status 1-Min 5-Min 15-Min
 RP0 Healthy  1.03  1.01  1.00

Memory (kB)
 Slot Status  Total   Used (Pct)   Free (Pct) Committed (Pct)
 RP0 Healthy 3950548 3035068 (77%)  915480 (23%)  2542008 (64%)

CPU Utilization
 Slot CPU  User System  Nice  Idle  IRQ  SIRQ IOwait
 RP0  0  1.80  6.60  0.00 91.60  0.00  0.00  0.00
     1  0.70  0.50  0.00 98.79  0.00  0.00  0.00
     2  3.10  6.40  0.00 90.50  0.00  0.00  0.00
     3  0.70  0.40  0.00 98.89  0.00  0.00  0.00
     4  1.90  0.10  0.00 98.00  0.00  0.00  0.00
     5  0.00  0.00  0.00 100.00  0.00  0.00  0.00
     6 24.20 75.80  0.00  0.00  0.00  0.00  0.00
     7  0.00  0.00  0.00 100.00  0.00  0.00  0.00
```

---
https://networkdirection.net/articles/routingandswitching/ios-xepacketcapture/
https://www.cisco.com/c/en/us/support/docs/switches/catalyst-9500-series-switches/214484-cisco-smart-licensing-troubleshooting.html
https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/csa/configuration/xe-16/csa-xe-16-book/csa-smrt-license.html
https://blog.ine.com/2008/02/15/the-inside-and-outside-of-nat
https://networklessons.com/cisco/ccie-routing-switching/nat-virtual-interface
https://www.cisco.com/c/en/us/td/docs/routers/access/wireless/software/guide/SysMsgLogging.html
https://www.ciscozine.com/nat-virtual-interface-aka-nvi-what-is-that/




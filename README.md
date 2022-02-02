Place these scripts in `/etc/sysconfig/network-scripts` on your
RedHat/CentOS/Fedora system.

Sample configuration for a `vxlan` interface:

	TYPE=VXLAN
	DEVICE=vxlan1000
	BOOTPROTO=none
	ONBOOT=yes
	TTL=255
	VNI=1000
	DSTPORT=4789
	LOCAL_ADDR="192.168.1.1"
	PHYS_DEV="eth0"
	OPTIONS="nolearning"
	BRIDGE="br1000"


Collect PHYS_DEV and LOCAL_ADDR and VNI and DSTPORT
```
# ip r
ip r|grep src| cut -d' ' -f3,9
```
```
# PHYS_DEV and LOCAL_ADDR
eno1 192.168.1.53
```
```
# Find VNI for DSTPORT 4789 
tcpdump -nnni eno1 udp port 4789|grep VXLAN|tail -n1|awk '{print $(NF-1),$NF }'
```
```
vni 7310759
```

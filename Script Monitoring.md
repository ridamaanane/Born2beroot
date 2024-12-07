#!/bin/bash

#Architecture
arch=$(uname -a)

#CPU physical
cpu=$(grep "physical id" /proc/cpuinfo | wc -l)

#vCPU
vcpu=$(grep "processor" /proc/cpuinfo | wc -l)

#Memory Usage
f1=$(free -m | grep Mem | awk '{print $3}')
f2=$(free -m | grep Mem | awk '{print $2}')
div=$(printf "%.2f" $(($f1*100/$f2)))

#Disk Usage
disk=$(df --total -h | grep "total" | awk '{printf "%d/%dGB (%s)", $3, $4, $5}')

#CPU load
cpul=$(uptime | awk '{printf "%.1f%\n", $9}')

#Last boot
lboot=$(who -b | awk '{print $3 " " $4}')

#LVM use
lvmu=$(if [[ $(lsblk | grep 'lvm' | wc -l) -gt 0 ]]; then echo yes; else echo no; fi)

#Connections TCP
conne=$(ss -ta | grep 'ESTAB' | wc -l)

#User log
ulog=$(who | awk '{print $1}' | sort -u | wc -l)

#Network
netip=$(hostname -I | cut -d ' '  -f1)
netmc=$(ip route | grep default | cut -d ' ' -f5)
netw=$(ip address show $netmc | grep "link/ether" | awk '{print $2}')

#Sudo
sudo=$(sudoreplay -l -d /var/log/sudo | grep COMMAND | wc -l)

wall "	#Architecture: $arch
	#CPU physical : $cpu
	#vCPU : $vcpu
	#Memory Usage: $f1/${f2}MB ($div%)
	#Disk Usage: $disk
	#CPU load: $cpul
	#Last boot: $lboot
	#LVM use: $lvmu
	#Connections TCP : $conne ESTABLISHED
	#User log : $ulog
	#Network: IP $netip ($netw)
	#Sudo : $sudo cmd"

# Dell Omsa Zabbix monitoring

This repository includes script, config and zabbix template for monitoring different components and information from a dell server running omsa on linux.

Tested with: OMSA: 8.1.0 Zabbix: 3.4 / 4.0.0


server:DELL PowerEdge R610
os:centos7.2 64bit



What
Script and template in this repository will monitor the most important components and information from the server. It won't show every little detail provided by omsa. Below is a list of provided information:

Discovered items:

Virtual disks and their controller
Physical disks and their controller
Fans with their index number
Battery with their index number
PSU's with their index number
Temperature sensors
RAM with their index number

Monitored items and triggers:

* Individual physical disks and their status Trigger: physical disk not online or predictive failure is true
* Individual virtual disk RAID type/size and status Trigger: virtual disk status is not ok
* Individual battary and their status and state Trigger: battary status not ok
* Individual fans and their status and RPM Trigger: fan status not ok
* Individual PSU's and their status Trigger: PSU status not ok
* Individual temperature sensors and their value
* Individual RAM modules and their status Trigger: RAM status not ok
* Server model
* Server service tag
* Server BIOS version
* Server iDRAC version
* Server general health status Trigger: if any of the status indicators is not ok



Install OMSA
1.wget -q -O - http://linux.dell.com/repo/hardware/latest/bootstrap.cgi | bash
2.yum update
3.yum install srvadmin-all


Edit your zabbix agent configuration and add
Include=/etc/zabbix/zabbix_agentd.d/userparameter_omsa.conf

Restart zabbix-agent
Add sudo permissions for zabbix-agent to run omsa.sh script

visudo

add line:
zabbix ALL=(ALL)  NOPASSWD: /etc/zabbix/dell-omsa/omsa.sh

Add template
1. cp userparameter_omsa.conf /etc/zabbix/zabbix_agentd.d/
1. cp -r omsa.sh /etc/zabbix/dell-omsa/
1. chmod +x /etc/zabbix/dell-omsa/*.sh
1. systemctl restart zabbix-agent (OR reboot)
1. zabbix:Configuration--Templates--Import,dell-omsa-3_4.xml 


Have fun!thinks for gitlab people!
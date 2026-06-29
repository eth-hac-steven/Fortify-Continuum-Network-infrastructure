# PFsense-Vlan Segmentation Configuration

### Vlan Segmentation
---
  This is a very important setup in Enterprise network as this help to 
   - control access for End user Device
   - Aids to containing Breaches in the netwok stopping the lateral movement 
   - Protecting Critical Device like the servers and the firewalls

Currently the pfsense we have up is working on a flat network ie any system on the network can open the browser, connect to firewall and attempt to bruteforce it and we dont want that do we so segmentation is required.

### prerequisite
---
- PFsense wizard completed [view here](https://github.com/eth-hac-steven/Threatsphere-Consulting-Network-infrastructure/tree/main/Threatsphere%20PFsense%20Firewall%20config)
- Win pc 

### Vlan Setup
----
#### Defining Scope 
 These are the segment we will be creating are:
  - Human-Res               : 192.168.10.10-210 :  .1-.9 Reservered from static devices like printers
  - Accounting              : 192.168.20.10-210 :  .1-.9 Reservered from static devices like printers 
  - Underwriting            : 192.168.30.10-210:  .1-.9 Reservered from static devices like printers  
 

#### Configuring VLANS
- Login into the PFsense Firewall
- click the Menu button
- Click on ```interface```
- Click on ```Assignments```

![alt text](vlan-config-1.png)

- click on ```vlans```
- click on ```add```

![alt text](vlan-config-2.png)

- Change the parent interface to lan using the dropdown arrow
- set the vlan tag according to what is in the scope i.e 10
- leave the priority empty
- Description ; Describe what the segment is for
- Clik save 

![alt text](vlan-config-3.png)

- Repeat this for all the segment in the scope.

![alt text](vlan-config-4.png)

#### Inteface Assignments

- click on ```interface Assignment```
- Click on Add

![alt text](vlan-config-5.png)

- Add for the VLANS created 

![alt text](vlan-config-6.png) 

- Click on save

#### Enabling VLan interface

- click on OPT1
- Check Enable interface
- Enter a name eg Human-Res
- set the ipv4 configuration : static

![alt text](vlan-config-7.png)

- set the ip address : 192.168.10.1

![alt text](vlan-config-8.png) 

- leave the other as is 
- click on ```save```
- click ```apply changes```
- Repeat for all other vlans
- You should have something like this

![alt text](vlan-config-9.png)

- Click Save


#### Enabling DHCP server

- click the Menu button
- Click on Services
- Click on DHCP server

![alt text](vlan-config-Dhcp-server.png)

This should come up 

![alt text](vlan-config-Dhcp-server-isc-dep-pt1.png)

As the waring display lets make that change 

- click on the menu button
- click on systems 
- click on Advanced

![alt text](vlan-config-Dhcp-server-isc-dep-pt2.png)

- click on Networking 
- check KEA DHCP
- scroll down and save

![alt text](vlan-config-Dhcp-server-isc-dep-pt3.png) 

- Return back to the DHCP server
- the warning should be gone
- click on setting 
- check Early DNS and DNS registration
- click on save
- click on "Apply setting"

![alt text](vlan-config-Dhcp-server-isc-dep-pt4.png)

- click on HumanRes
- Check "Enable DHCP server on Human-Res"

![alt text](vlan-config-Dhcp-server-isc-dep-pt5.png)

- Enter a DHCP IP address pool range in Relation to the scope 
 ie 192.168.10.10 - 192.168.10.210

![alt text](HUMANRES-iprnage.png) 

- click on save
- Click on Apply Changes
- Repeats this for other VLANS

#### Static IP setup 

 Static ip for Devices like printers,scanner 

- Click  on "static Mapping"

 ![alt text](vlan-config-static-ip-1.png)

- Add the MAC address of the device 
- Pick an IP from the range we set aside in the scope ie .1-.9

![alt text](vlan-config-static-ip-2.png)

- click save

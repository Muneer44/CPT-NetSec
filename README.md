# Network-Security
Simulating real-world organization network configuration and security using Cisco Packet Tracer.

## Table of Contents
### Security controls and Advanced networking configuration:
- [📍 Topology: Network Design](#topology:-simulated-network-design)
- [🗺 Network Connectivity Map](#network-connectivity-map)
- [⛓ Advanced Network Configuration](#advanced-network-configuration)
    - [🔗 VLAN segmentation and Trunk Creation](#VLAN-Segmentation)
    - 🔗 Router On Stick Configuration
    - 🔗 OSPF implementation
    - 🔗 DR and BDR Assignments
    - 🔗 Stubby Area Creation

- 🔐 Network Security Controls:
    - [🗝 Port Access Security](#Port-access-security)
    - [🗝 Access Control Lists](#ACL)
    - [🗝 AAA Authentication](#AAA-Authntication)
    - [🗝 Industry Best Practices](#Industry)


# Topology: Network Design
_The topology diagram represents the simulated network configuration. It provides an overview of the network devices and their interconnections._

<img src="https://github.com/Muneer44/Security-Onion-Traffic-Analysis/assets/117259069/fd9aad62-e6d5-4281-ab0e-57646a641837" alt = "Network Topology Diagram" width="700" height="500">


# Network Connectivity Map
_The network connectivity map illustrates the connectivity and relationships between different devices in the network. The map shows the physical connections between the devices, including the interfaces, IP addresses, and subnet masks used for communication. It helps to understand the overall network layout and aids in troubleshooting and maintaining the network infrastructure._


<img src="https://github.com/Muneer44/Security-Onion-Traffic-Analysis/assets/117259069/37c0e2a2-7ec7-4b30-8aea-fc4f57d9d3d6" width="650" height="480">


<details>
<summary><h1>🔗Advanced Network Configuration</h1></summary>

## 💡 VLAN segmentation and Trunk Creation
![image](https://github.com/Muneer44/Network-Security/assets/117259069/5b5ca85a-f7dc-4896-89de-a90d52b8e1ea)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/a43eb16a-6571-4b34-83e2-0831fc1b5813)

```
Switch-A(config)# vlan <vlan-id>
Switch-A(config-vlan)# name <vlan-name>
Switch-A(config-if)# int vlan <vlan-id>
Switch-A(config-if)# ip address <ip-address> <subnet mask>
Switch-A(config-if)# exit

Switch-A(config)# int <PC-interface>
Switch-A(config-if)# switchport mode access
Switch-A(config-if)# switchport access vlan <vlan-id>
Switch-A(config-if)# exit

Switch-A(config)# int <network device int>
Switch-A(config-if)# switchport mode trunk
Switch-A(config-if)# switchport trunk allowed vlan <vlan IDs>
Switch-A(config-if)# exit
Switch-A(config)# exit

Switch-A# sh int trunk
```

---

## 💡 Router On Stick
![image](https://github.com/Muneer44/Network-Security/assets/117259069/bc86bda5-0c0b-4b26-85cd-34671e944adf)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/42b420e4-25a1-4d71-bebd-e14d50d45815)

```
HQ(config)# int <sub interfaces (ex: g0/1.10)>
HQ(config-if)# encapsulation dot1q <vlan id>
HQ(config-if)# ip address <Ip-address> <Subnet Mask>
HQ(config-if)#  exit

HQ(config)# int <native vlan sub int>
HQ(config)# encapsulation dot1q <native vlan id> native
```

<img src="https://github.com/Muneer44/Network-Security/assets/117259069/355e9e35-5a92-4d13-9442-7af87c8e0cc7" width="400" height="410">

_# Inter-Vlan connection test._

---

## 💡 OSPF implementation
**_HQ Router:_**  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/eec9aff6-9b5d-4791-8d67-6c8687fa5ba8)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/8e602617-944e-4c3d-8f1e-83c9e96e326a)

**_GW Router:_**  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/067a24d9-8bc7-4edf-a7b1-84a048c1d4d9)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/605c6c0a-069f-46c9-8980-0fc923349f8f)

**_BRANCH Router:_**  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/9028fdc7-55d3-4238-a6f2-0886d027a5e2)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/3825bfb6-14e5-4a42-9a1f-e044da25b5c2)

```
GW# sh ip route connected
GW(config)# router ospf <Process-id>
GW(config-router)# network <network-device-ip> <Wildcard-IP> area <area-id>
```
---

## 💡 DR and BDR   
![image](https://github.com/Muneer44/Network-Security/assets/117259069/d23d7098-11ca-403a-8745-431276fc167b)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/46fac190-c935-4085-862e-d70b1993f51f)

```
GW(confg)# router ospf <Process-id>
GW(config-router)# router-id <id>
```
---

## 💡 Stubby Area Creation and Default Route Verification
<img src="https://github.com/Muneer44/Network-Security/assets/117259069/a0e05523-d50f-41fb-9fdd-e0c5e3061371" width="400" height="450" >  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/4c28dcd7-7052-4048-ab0c-d7ede2654d3b)

```
GW(confg)# router ospf <process-id>
GW(config-router)# area <area-id> stub no-summary
```
---

</details>

---

# 🔐 Network Security Controls:

## 🗝 Port Access Security
![image](https://github.com/Muneer44/Network-Security/assets/117259069/ba465402-6d09-4aee-a524-ce891176b36b)

**_Attacker-1 = Restrict Violation_**  
<img src="https://github.com/Muneer44/Network-Security/assets/117259069/41bd5775-2982-4928-846a-dd4809414e5d" width="650" height="400">

**_Attacker-2 = Shutdown Violation_**  
<img src="https://github.com/Muneer44/Network-Security/assets/117259069/a4894522-91aa-44e5-88b3-eb3e9e001469" width="650" height="400">

```
SwitchA(config)# int <pc interface>
SwitchA(config-if)# switchport port-security
SwitchA(config-if)# switch port-security mac-address <pc mac-addr>
SwitchA(config-if)# switchport port-security violation <restrict/ shutdown>

SwitchA# sh port-security
```

# 🗝 Access Control Lists
#### _**Scenario A:**_  
![image](https://github.com/Muneer44/Network-Security/assets/117259069/2ae9a522-46c9-4710-b7b4-480b3d58301f)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/00685b0f-f986-49a2-b3a0-d7217b259b1c)  
_Demonstrates denial of SSH and Telnet traffic from 192.168.20.x Vlan network to host 172.16.1.2 (GW router)_  

```

```  
  
#### _**Scenario B:**_  
![image](https://github.com/Muneer44/Network-Security/assets/117259069/50fbddfa-a0ae-4bbe-97ac-923bb7efe96e)
![image](https://github.com/Muneer44/Network-Security/assets/117259069/49e8b120-55a3-4445-8bf1-075a192f460f)    
_Demonstrates denial of traffic from host 172.16.3.7 Attacker-ACL-PC to 192.168.x.x network_

---

# 🗝 AAA Authentication
AAA authentication, Authentication, Authorization and Accounting, refers to the process of verifying the identity of users, authorizing their access to network resources, and accounting for their activities for auditing and tracking purposes. Implementation of AAA Authentication also enables secure remote access to the network devices.    

![image](https://github.com/Muneer44/Network-Security/assets/117259069/da16c451-7391-48dd-a61b-8397cb88cb60) <img src="https://github.com/Muneer44/Network-Security/assets/117259069/377c1afb-bced-4ecf-8579-46accb4cf004" width="280" height="210">    

<img src="https://github.com/Muneer44/Network-Security/assets/117259069/bdcc05fb-ee4a-4955-a10d-35bcef7ec6b2" width="480" height="100">     
 
---

# 🗝 Industry Best Practices
## DHCP Snooping
DHCP snooping protects against rogue DHCP (Dynamic Host Configuration Protocol) servers and DHCP-related attacks. It that only authorized DHCP servers can assign IP addresses to network devices. The switch builds a trusted database of valid DHCP servers by inspecting DHCP messages exchanged between clients and servers. The switch then uses this information to validate DHCP messages and prevent unauthorized DHCP servers from distributing IP addresses.  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/a8a79251-3357-49ac-9508-d76078a2c962)


## VLAN Segmentation
Using VLANs to isolate sensitive systems and data from the rest of the network. This limits the impact of a potential breach and reduces the attack surface.  

<img src="https://github.com/Muneer44/Network-Security/assets/117259069/8bec5384-c375-43c5-8d9d-28c437ed2fec" width="250" height="350">

## Avoiding Default Native VLAN
The default Native VLAN is Vlan-1. Avoiding the default native VLAN provides isolation of management traffic and prevents potential VLAN hopping attacks, thus mitigating unauthorized access to sensitive network segments.  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/068cb16c-7a2a-4aae-a87c-c48043125c5d)

## Cryptography and Secure Protocols
Storing hashed console and remote acces credentials mitigates the risk of password compromise, thereby protects insider threats and other potential password attacks.  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/52d760ea-dabc-420c-802d-00d1fd50ff7e)  

Using secure protocols and preventing insecure protocols improves network security by encrypting communication, thereby safeguards against unauthorized access to sensitive information through potential attacks like eavesdropping.  

![image](https://github.com/Muneer44/Network-Security/assets/117259069/471da4c5-b317-46f7-ae0d-55e32648d2fa)

# 📖 CLI Command Cheat-Sheet — সম্পূর্ণ নেটওয়ার্কিং কমান্ড গাইড

> **নেভিগেশন:** [🏠 হোম](../README.md) · [🎓 ফাইনাল প্রজেক্ট](../lessons/08-final-project.md)
> এটি লেসন নয় — সব লেসনের কমান্ডের **রেফারেন্স/প্র্যাকটিস গাইড**। প্রয়োজন অনুযায়ী খুঁজে নাও।

**Tags:** `#cheatsheet` `#cli` `#commands` `#reference` `#ccna` `#show-commands` `#shortcut`

---

## 🟢 Part 1 · Cisco CLI Basic Commands

| Command | কাজ | Mode |
| :--- | :--- | :--- |
| `enable` | Privileged Mode-এ যাওয়া | User → Privileged |
| `disable` | User Mode-এ ফেরা | Privileged → User |
| `configure terminal` (conf t) | Global Config Mode | Privileged |
| `exit` | এক ধাপ পিছনে | যেকোনো Config |
| `end` | সরাসরি Privileged Mode | যেকোনো Config |
| `copy running-config startup-config` (copy run start) | কনফিগ **সেভ** | Privileged |
| `show running-config` (show run) | বর্তমান কনফিগ দেখা | Privileged |
| `show startup-config` | সেভ করা কনফিগ দেখা | Privileged |
| `show history` | আগের কমান্ড ইতিহাস | Privileged |
| `write` (wr) | সেভ-এর সংক্ষিপ্ত রূপ | Privileged |
| `reload` | রাউটার/সুইচ রিস্টার্ট | Privileged |
| `?` | সাহায্য (যেকোনো জায়গায়) | সব |

### ⚡ Shortcut — কমান্ড ছোট করে টাইপ করো (Abbreviation Rule)

**নিয়ম:** IOS-এ যেকোনো কমান্ড বা শব্দের **unique prefix** টাইপ করলেই চলে — অর্থাৎ এতটুকু লিখলেই যেন বাকি কোনো কমান্ড না মেলে। পুরোটা টাইপ করা **বাধ্যতামূলক নয়।**

| পুরো কমান্ড | শর্টকাট | নোট |
| :--- | :--- | :--- |
| `show interfaces` | `show int` (বা `sh int`) | ✅ **টেস্ট করা — কাজ করে** |
| `interface fastEthernet 0/0` | `interface fas 0/0` (বা `int fa0/0`) | ✅ **টেস্ট করা — কাজ করে** (`fas`/`fa` = `fastEthernet`-এরই শুরু) |
| `configure terminal` | `conf t` | প্রায় সবাই এটাই লেখে |
| `interface g0/0` | `int g0/0` | `interface` → `int` |
| `show running-config` | `show run` / `sh run` | |
| `show ip interface brief` | `sh ip int br` | সবচেয়ে জনপ্রিয় শর্টকাট |
| `copy running-config startup-config` | `copy run start` (বা `wr`) | |
| `no shutdown` | `no shut` | |
| `ip address ...` | `ip add ...` | |

⚠️ **কেন `show int` চলল, কিন্তু `show in` চলে না?** — `in` দিয়ে শুরু হয় একাধিক কমান্ড (`interface`, `inventory`...) → IOS দেবে `% Ambiguous command`। কিন্তু `int` দিয়ে শুরু হয় শুধু `interface`/`interfaces` → কোনো দ্বিধা নেই, তাই কাজ করে ✅ একইভাবে `fas` দিয়ে শুরু হয় শুধু `fastEthernet`।

> 🧠 তাই পুরো কমান্ড মুখস্থ না করেও লেখা যায় — শুধু মনে রাখো **কতটুকু লিখলে unique হবে**। নিশ্চিত না হলে `?` চাপো।

---

## 🔵 Part 2 · Router Configuration Commands

| Command | কাজ |
| :--- | :--- |
| `hostname R1` | নাম পরিবর্তন |
| `interface gigabitEthernet 0/0` (int g0/0) | Interface নির্বাচন |
| `ip address 192.168.1.1 255.255.255.0` | IP + Mask সেট |
| `no shutdown` | Interface **চালু** |
| `shutdown` | Interface **বন্ধ** |
| `show ip interface brief` (sh ip int br) | Interface IP/Status সারণি |
| `show interfaces` (show int ✅) | Interface-এর বিস্তারিত পরিসংখ্যান |
| `show ip route` | **Routing Table** |
| `ping 10.0.0.2` | Connectivity পরীক্ষা |
| `traceroute 10.0.0.2` | প্যাকেটের পথ পরীক্ষা |
| `erase startup-config` | কনফিগ **মুছে ফেলা** |
| `reload` | রিস্টার্ট |

---

## 🟡 Part 3 · Switch Essential Commands

| Command | কাজ |
| :--- | :--- |
| `hostname SW1` | সুইচের নাম |
| `show vlan brief` | VLAN ও Port তালিকা |
| `show mac address-table` | MAC Address Table |
| `show interfaces status` | সব পোর্টের স্ট্যাটাস |
| `show interfaces fa0/1` | নির্দিষ্ট পোর্টের বিস্তারিত |
| `show interfaces trunk` | Trunk পোর্ট তালিকা |
| `show spanning-tree` | STP স্ট্যাটাস |
| `interface vlan 1` + `ip address` + `no shutdown` | Management IP (SVI) |
| `ip default-gateway 192.168.1.1` | সুইচের ডিফল্ট গেটওয়ে |

---

## 🟣 Part 4 · IP Addressing ও Subnetting

| Subnet Mask | CIDR | Usable Hosts |
| :--- | :---: | ---: |
| `255.255.255.0` | /24 | 254 |
| `255.255.255.128` | /25 | 126 |
| `255.255.255.192` | /26 | 62 |
| `255.255.255.224` | /27 | 30 |
| `255.255.255.240` | /28 | 14 |
| `255.255.255.252` | /30 | **2** (Point-to-Point Link) |

**PC-তে:**
```text
ipconfig              ← IP/Mask/Gateway দেখা
ipconfig /all         ← DNS সহ সব তথ্য
ping [IP]             ← সংযোগ পরীক্ষা
tracert [IP]          ← পথ পরীক্ষা (Windows)
arp -a                ← ARP টেবিল
```

---

## 🟠 Part 5 · DHCP Commands

| Command | কাজ |
| :--- | :--- |
| `ip dhcp pool [NAME]` | Pool তৈরি |
| `network 192.168.1.0 255.255.255.0` | বিতরণ রেঞ্জ |
| `default-router 192.168.1.1` | ক্লায়েন্টের Gateway |
| `dns-server 192.168.1.100` | ক্লায়েন্টের DNS |
| `ip dhcp excluded-address 192.168.1.1 192.168.1.10` | সংরক্ষিত রেঞ্জ |
| `show ip dhcp pool` | পুল পরিসংখ্যান |
| `show ip dhcp binding` | লিজ টেবিল |
| `show ip dhcp conflict` | কনফ্লিক্ট চেক |
| `no ip dhcp pool [NAME]` | Pool মুছে ফেলা |

---

## 🔴 Part 6 · Static ও Dynamic Routing

### Static Route
```text
ip route [DEST_NET] [MASK] [NEXT_HOP]
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

### Default Route (ইন্টারনেটের জন্য)
```text
ip route 0.0.0.0 0.0.0.0 [NEXT_HOP]
```

### RIP Version 2
```text
router rip
 version 2
 network 192.168.1.0
 network 10.0.0.0
 no auto-summary
 exit
```

### OSPF Basic
```text
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
 exit
```

### যাচাই
| Command | কাজ |
| :--- | :--- |
| `show ip route` | Routing Table (`C`/`S`/`R`/`O` কোড) |
| `show ip protocols` | চলমান Routing Protocol |
| `show ip ospf neighbor` | OSPF প্রতিবেশী |

| Route Code | অর্থ |
| :--- | :--- |
| `C` | Connected |
| `S` | Static |
| `R` | RIP |
| `O` | OSPF |
| `S*` | Default Static Route |

---

## 🟢 Part 7 · VLAN, Trunk ও Inter-VLAN

```text
vlan 10                        ← VLAN তৈরি
 name CSE
interface fa0/1
 switchport mode access        ← Access Port
 switchport access vlan 10     ← Port-এ VLAN
interface g0/1
 switchport mode trunk         ← Trunk Port
interface g0/0.10              ← Subinterface
 encapsulation dot1Q 10        ← 802.1Q Tag
 ip address 192.168.10.1 255.255.255.0
```

| Verification | Command |
| :--- | :--- |
| VLAN তালিকা | `show vlan brief` |
| Trunk স্ট্যাটাস | `show interfaces trunk` |
| Subinterface | `show ip interface brief` |

---

## 🔐 Part 8 · Network Security Commands

### Password সেট
```text
enable secret [PASS]           ← Enable Password (encrypted)
line console 0
 password [PASS]
 login
 exit
line vty 0 4
 password [PASS]
 login
 exit
service password-encryption    ← সব পাসওয়ার্ড encrypt
```

### SSH (Telnet-এর নিরাপদ বিকল্প)
```text
ip domain-name office.local
crypto key generate rsa
username admin secret [PASS]
line vty 0 4
 transport input ssh
 login local
 exit
```

### Port Security
```text
interface fa0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
```
```text
show port-security
show port-security interface fa0/1
show port-security address
```

---

## 🔵 Part 9 · STP, EtherChannel ও Discovery

### STP
```text
show spanning-tree
spanning-tree vlan 1 root primary
spanning-tree vlan 1 priority 4096
```

### EtherChannel (LACP)
```text
interface range g0/1 - 2
 channel-group 1 mode active
interface port-channel 1
 switchport mode trunk
```
```text
show etherchannel summary
```

### CDP / LLDP (প্রতিবেশী ডিভাইস খোঁজা)
```text
show cdp neighbors            ← Cisco ডিভাইস তালিকা
show cdp neighbors detail
show lldp neighbors           ← সব ভেন্ডর
```

---

## 🟣 Part 10 · Troubleshooting Master Commands

| Command | কখন ব্যবহার করবে |
| :--- | :--- |
| `show ip interface brief` | Interface up/up কি না |
| `show ip route` | পথ আছে কি না |
| `show vlan brief` | VLAN/Port ঠিক কি না |
| `show interfaces trunk` | Trunk চলছে কি না |
| `show mac address-table` | সুইচ ঠিকভাবে শিখছে কি না |
| `show running-config` | কনফিগ মেলানো |
| `show ip dhcp binding` | DHCP লিজ |
| `show spanning-tree` | লুপ/STP সমস্যা |
| `show logging` | ইভেন্ট লগ |
| `debug ip dhcp` / `debug ip packet` | লাইভ ডিবাগ (⚠️ সাবধানে) |

### Troubleshooting-এর সহজ Formula 🧠
```text
১. Physical Layer?  → কেবল, লিংক লাইট, no shutdown
২. IP/Mask/Gateway? → ipconfig + show ip interface brief
৩. Route আছে?      → show ip route
৪. VLAN/Trunk ঠিক?  → show vlan brief + show interfaces trunk
৫. Service চালু?    → DHCP/DNS/HTTP ON কি না
৬. Ping ধাপে ধাপে  → কাছের Device → Gateway → দূরের Device
```

---

## 🏆 Final Practice Challenge

নিজে একটি টপোলজি তৈরি করো: **2 VLAN + 2 Router + DHCP + DNS + HTTP + Static Route**, তারপর নিচের Task সম্পন্ন করো:

1. প্রতিটি VLAN-এর PC স্বয়ংক্রিয়ভাবে IP পাচ্ছে
2. ভিন্ন VLAN-এর মধ্যে Ping কাজ করছে
3. ডোমেন নাম দিয়ে ওয়েবসাইট খুলছে
4. সব কনফিগ সেভ করা আছে
5. Port Security দিয়ে একটি পোর্ট সুরক্ষিত

---

> **নেভিগেশন:** [🏠 হোম](../README.md) · [🎓 ফাইনাল প্রজেক্ট](../lessons/08-final-project.md)

**Tags:** `#cheatsheet` `#cli-reference` `#show-commands` `#troubleshooting` `#ccna-prep`

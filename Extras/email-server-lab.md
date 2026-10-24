# 📧 Cisco Packet Tracer Lab — Email Server Configuration

**Level:** CCNA Practical  
**Topology:** 2 PCs + 2 Switches + 1 Router + 1 Server  
**Protocols Covered:** SMTP, POP3, ICMP (Ping), Inter-Network IP Routing  
**pkt File:** [Email-Server.pkt](../pkt-files/practice/Email-Server.pkt)

এই Lab-এ আমরা Cisco Packet Tracer-এ একটি সম্পূর্ণ Email Server কনফিগার করব। আলাদা দুটি LAN সাবনেটে থাকা পিসির মধ্যে (PC0 থেকে PC1) ইমেইল আদান-প্রদান করে যাচাই করব এবং DNS ছাড়া সরাসরি IP দিয়ে কীভাবে Mail Client কনফিগার ও ট্রাবলশুট করতে হয় তা শিখব।

---

## 1. Network Topology

### প্রয়োজনীয় ডিভাইসসমূহ:
* **$2 \times$ PC:** PC0 ও PC1
* **$2 \times$ Switch:** Switch 2960 (SW1 ও SW2)
* **$1 \times$ Router:** Cisco 1941 (Router2)
* **$1 \times$ Server:** Generic Server (Email Server)

### Topology Diagram:
```text
                     [ PC0 ]
                        |
                     [ SW1 ]
                        |
                  [ Router2 ]
                        |
                     [ SW2 ]
                   /         \
              [ PC1 ]     [ Email Server ]
```

### কেবল:
সব কানেকশনে **Copper Straight-Through** কেবল ব্যবহার করো।

---

## 2. IP Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway | DNS Server |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Router2** | `GigabitEthernet0/0` | `192.168.10.1` | `255.255.255.0` | — | — |
| **Router2** | `GigabitEthernet0/1` | `192.168.20.1` | `255.255.255.0` | — | — |
| **PC0 (makshedul)** | `FastEthernet0` | `192.168.10.3` | `255.255.255.0` | `192.168.10.1` | `192.168.20.3` |
| **PC1 (antor)** | `FastEthernet0` | `192.168.20.2` | `255.255.255.0` | `192.168.20.1` | `192.168.20.3` |
| **Email Server** | `FastEthernet0` | `192.168.20.3` | `255.255.255.0` | `192.168.20.1` | `192.168.20.3` |

### 📌 Network বুঝে রাখো

| কী | ঠিকানা |
| :--- | :--- |
| **PC0 Network** | `192.168.10.0/24` |
| **PC1 + Email Server Network** | `192.168.20.0/24` |
| **Router2 G0/0** | `192.168.10.1` |
| **Router2 G0/1** | `192.168.20.1` |
| **Email Server** | `192.168.20.3` |

> 🔁 দুটি আলাদা নেটওয়ার্কের মধ্যে প্যাকেট পাঠানোর জন্য **Router2** Inter-Network Routing করে।

---

## 3. Router2 Configuration

Router2-এর CLI ওপেন করে নিচের কমান্ডগুলো দিন:

```cisco
Router> enable
Router# configure terminal
Router(config)# hostname Router2

! LAN 1 Interface (Connecting to PC0 via SW1)
Router2(config)# interface gigabitEthernet 0/0
Router2(config-if)# ip address 192.168.10.1 255.255.255.0
Router2(config-if)# no shutdown
Router2(config-if)# exit

! LAN 2 Interface (Connecting to PC1 & Server via SW2)
Router2(config)# interface gigabitEthernet 0/1
Router2(config-if)# ip address 192.168.20.1 255.255.255.0
Router2(config-if)# no shutdown
Router2(config-if)# exit

Router2(config)# end
Router2# write memory
```

### স্ট্যাটাস ভেরিফিকেশন:
```cisco
Router2# show ip interface brief
```
*যাচাই করো `GigabitEthernet0/0` এবং `GigabitEthernet0/1` দুটোর Status এবং Protocol `up / up` প্রদর্শন করছে।*

---

## 4. End-Device IP Configuration

### PC0 (makshedul) Setup:
* ক্লিক: `PC0` $\rightarrow$ `Desktop` $\rightarrow$ `IP Configuration`
```text
IP Address:      192.168.10.3
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
DNS Server:      192.168.20.3
```

### PC1 (antor) Setup:
* ক্লিক: `PC1` $\rightarrow$ `Desktop` $\rightarrow$ `IP Configuration`
```text
IP Address:      192.168.20.2
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1
DNS Server:      192.168.20.3
```

### Email Server IP Setup:
* ক্লিক: `Server` $\rightarrow$ `Desktop` $\rightarrow$ `IP Configuration`
```text
IP Address:      192.168.20.3
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1
DNS Server:      192.168.20.3
```

---

## 5. Configure Email Services on Server

সার্ভারে ক্লিক করে `Services` $\rightarrow$ `EMAIL` ট্যাবে যাও।

```text
+-------------------------------------------------------+
|                 EMAIL SERVICE SETUP                   |
+-------------------------------------------------------+
|  SMTP Service:   (*) On    ( ) Off                    |
|  POP3 Service:   (*) On    ( ) Off                    |
|                                                       |
|  Domain Name:    [ university.com   ]  [ Set ]        |
+-------------------------------------------------------+
```

### ধাপসমূহ:
1. **Service Toggle:** **SMTP Service** এবং **POP3 Service** দুটোতেই `On` রেডিও সিলেক্ট করো।
2. **Domain Name:** টেক্সটবক্সে `university.com` লিখে পাশে থাকা **Set** বাটনে ক্লিক করো।
3. **User Accounts তৈরি:**

| User | Username | Password | Action | Complete Email Address |
| :--- | :--- | :--- | :--- | :--- |
| **PC0 User** | `pc0` | `1234` | ক্লিক **[ + ]** বা **Add** | `pc0@university.com` |
| **PC1 User** | `pc1` | `1234` | ক্লিক **[ + ]** বা **Add** | `pc1@university.com` |

*লিস্টে `User List`-এ দুটি অ্যাকাউন্ট যোগ হয়েছে কি না নিশ্চিত হও।*

---

## 6. Configure Email Clients on PCs

Incoming এবং Outgoing দুই সার্ভার ফিল্ডেই সরাসরি Email Server-এর IP Address (`192.168.20.3`) ব্যবহার করব।

### PC0 Client Setup:
* যাও: `PC0` $\rightarrow$ `Desktop` $\rightarrow$ `Email` $\rightarrow$ `Configure Mail`

```text
Your Name:              PC0
Email Address:          pc0@university.com
Incoming Mail Server:   192.168.20.3
Outgoing Mail Server:   192.168.20.3
Username:               pc0
Password:               1234
```
*সব তথ্য দিয়ে নিচে **Save** বাটনে ক্লিক করো।*

---

### PC1 Client Setup:
* যাও: `PC1` $\rightarrow$ `Desktop` $\rightarrow$ `Email` $\rightarrow$ `Configure Mail`

```text
Your Name:              PC1
Email Address:          pc1@university.com
Incoming Mail Server:   192.168.20.3
Outgoing Mail Server:   192.168.20.3
Username:               pc1
Password:               1234
```
*সব তথ্য দিয়ে নিচে **Save** বাটনে ক্লিক করো।*

---

## 7. Testing: Send & Receive Email

### ধাপ ১: PC0 থেকে ইমেইল পাঠানো (Compose & Send)
1. **PC0** $\rightarrow$ `Desktop` $\rightarrow$ `Email` $\rightarrow$ **Compose** এ ক্লিক করো।
2. ফিল্ডগুলো পূরণ করো:
   * **To:** `pc1@university.com`
   * **Subject:** `Test Email from PC0`
   * **Message body:**  
     `Hello PC1, this is my first email from Cisco Packet Tracer lab.`
3. **Send** বাটনে ক্লিক করো।
4. উইন্ডোর নিচে স্ট্যাটাস লাইনে প্রদর্শিত হবে:  
   `Send Success`

---

### ধাপ ২: PC1-এ ইমেইল গ্রহণ ও রিড করা (Receive)
1. **PC1** $\rightarrow$ `Desktop` $\rightarrow$ `Email` এ যাও।
2. **Receive** বাটনে ক্লিক করো।
3. ইনবক্সে নতুন মেইল দেখতে পাবে:
   * From: `pc0@university.com`
   * Subject: `Test Email from PC0`
4. মেইলের ওপর ডাবল ক্লিক করে মেসেজটি ওপেন করো।

🎉 **অভিনন্দন! তোমার Inter-VLAN / Inter-Subnet Email Server Lab সফলভাবে সম্পন্ন হয়েছে!**

---

## 8. Troubleshooting Checklist

যদি ইমেইল আদান-প্রদান ব্যর্থ হয়, তবে নিচের ধারাবাহিকতায় পরীক্ষা করো:

```
[ IP Connectivity (Ping) ]
           ↓
[ Router Interface Status ]
           ↓
[ Server Service & Domain ]
           ↓
[ Client Mail Credentials ]
```

### ১. লেয়ার ৩ পিং টেস্ট:
* **PC0 Command Prompt:**
  ```cmd
  ping 192.168.10.1      (লজিস্টিক: গেটওয়ে সচল কি না)
  ping 192.168.20.3      (লজিস্টিক: রাউটার পার হয়ে সার্ভারে পৌঁছায় কি না)
  ```
* **PC1 Command Prompt:**
  ```cmd
  ping 192.168.20.3      (লজিস্টিক: লোকাল ল্যানে সার্ভার সাড়া দেয় কি না)
  ```

### ২. রাউটার ইন্টারফেস ত্রুটি:
* `show ip interface brief` কমান্ডে যদি কোনো পোর্ট `administratively down` দেখায়, তবে ইন্টারফেসে ঢুকে `no shutdown` কমান্ড দিতে হবে।

### ৩. ইমেইল সার্ভার ত্রুটি:
* সার্ভারে **Set** বাটনে ক্লিক না করলে ডোমেইন নাম সক্রিয় হয় না।
* SMTP এবং POP3 সার্ভিস অন (`On`) আছে কি না নিশ্চিত হও।
* ইউজারনেম ও পাসওয়ার্ডে কোনো অতিরিক্ত স্পেস বা কেস-সেনসিটিভিটি গরমিল আছে কি না মেলাও।

---

## 9. CCNA Viva / Interview Questions

### Q1. What is the role of an Email Server in a TCP/IP network?
> **Answer:** An email server acts as a centralized message transfer and storage agent. It accepts outgoing messages from clients via SMTP, routes them across networks, and holds incoming messages in mailboxes until users retrieve them using protocols like POP3 or IMAP.

### Q2. What is SMTP, and what is its primary operational role?
> **Answer:** **SMTP (Simple Mail Transfer Protocol)** is an Application Layer protocol used for **sending/pushing** email from a mail client to a mail server, and for relaying email between mail servers.

### Q3. What is POP3, and how does it differ from IMAP?
> **Answer:** **POP3 (Post Office Protocol version 3)** is an Application Layer protocol used by clients to **retrieve/download** email from a server to a local device. By default, POP3 downloads and deletes messages from the server, whereas **IMAP (Internet Message Access Protocol)** synchronizes folders and keeps emails stored centrally on the server.

### Q4. Which transport protocol and well-known ports are used by SMTP and POP3?
> **Answer:** Both protocols use **TCP** for reliable transmission:
> * **SMTP:** TCP Port **25** (Server-to-Server transfer) and TCP Port **587** (Client Submission / STARTTLS).
> * **POP3:** TCP Port **110** (Unencrypted) and TCP Port **995** (POP3S over SSL/TLS).

### Q5. Why was a Router strictly required in this specific topology?
> **Answer:** PC0 belongs to network `192.168.10.0/24` while PC1 and the Email Server belong to network `192.168.20.0/24`. A Layer 2 Switch cannot forward frames between distinct IP subnets; a Layer 3 Router is required to perform logical addressing lookups and packet routing.
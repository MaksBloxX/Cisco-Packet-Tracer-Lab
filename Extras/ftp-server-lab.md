# 🌐 Cisco Packet Tracer Full Lab: FTP Server Configuration

> **Level:** Beginner to CCNA Practical
> **Language:** English Commands + বাংলা ব্যাখ্যা
> **pkt File:** [FTP-Server.pkt](../pkt-files/practice/FTP-Server.pkt)

---

## 1. Network Topology & IP Addressing

### Network Diagram

```text
                        [ FTP SERVER ]
                               |
                         [ Router 1941 ]
                              (R1)
                               |
                        [ Switch 2960 ]
                             (SW1)
                     /     |     |     \
                   /       |     |       \
               [PC0]     [PC1]  [PC2]    [PC3]
```

### IP Address Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Router (R1)** | GigabitEthernet 0/0 | `192.168.1.1` | `255.255.255.0` | N/A |
| **Router (R1)** | GigabitEthernet 0/1 | `10.10.10.1` | `255.255.255.0` | N/A |
| **FTP Server** | FastEthernet 0 | `10.10.10.2` | `255.255.255.0` | `10.10.10.1` |
| **PC0** | FastEthernet 0 | `192.168.1.2` | `255.255.255.0` | `192.168.1.1` |
| **PC1** | FastEthernet 0 | `192.168.1.3` | `255.255.255.0` | `192.168.1.1` |
| **PC2** | FastEthernet 0 | `192.168.1.4` | `255.255.255.0` | `192.168.1.1` |
| **PC3** | FastEthernet 0 | `192.168.1.5` | `255.255.255.0` | `192.168.1.1` |

> ⚠️ **Important Note:** Server-এর IP Address `10.10.10.2` ব্যবহার করা হয়েছে, কারণ `10.10.10.1` Router-এর Server-facing interface-এর IP standard।

---

## 2. Router Configuration

Router-এ ক্লিক করে **CLI** ট্যাবে যান এবং নিচের কমান্ডগুলো ধারাবাহিকভাবে প্রদান করুন:

```cisco
enable
configure terminal

! Configure LAN Interface
interface gigabitEthernet 0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

! Configure Server-side Interface
interface gigabitEthernet 0/1
 ip address 10.10.10.1 255.255.255.0
 no shutdown
 exit

end
write memory
```

### Command Description (বাংলা ব্যাখ্যা)

| Command | Description (বিবরণ) |
| :--- | :--- |
| `enable` | Privileged EXEC Mode-এ প্রবেশ করার জন্য। |
| `configure terminal` | Global Configuration Mode-এ প্রবেশ করার জন্য। |
| `interface gigabitEthernet X/X` | নির্দিষ্ট Interface নির্বাচন করার জন্য। |
| `ip address <IP> <Subnet>` | Interface-এ IP Address এবং Subnet Mask প্রদান করার জন্য। |
| `no shutdown` | Port/Interface চালু (UP) করার জন্য। |
| `exit` | পূর্ববর্তী Configuration Mode-এ ফিরে যাওয়ার জন্য। |
| `end` | Privileged EXEC Mode-এ ফিরে যাওয়ার জন্য। |
| `write memory` | বর্তমান Configuration NVRAM-এ Save করার জন্য। |

### Verification Command

```cisco
show ip interface brief
```
> **Check:** নিশ্চিত করুন যে উভয় Interface-এর Status **`UP`** এবং Protocol **`UP`** রয়েছে।

---

## 3. PC Configuration

প্রতিটি PC-তে ক্লিক করে **Desktop → IP Configuration** সিলেক্ট করুন এবং নিচের তথ্যগুলো বসান:

#### 💻 PC0 Configuration
- **IP Address:** `192.168.1.2`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `192.168.1.1`

#### 💻 PC1 Configuration
- **IP Address:** `192.168.1.3`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `192.168.1.1`

#### 💻 PC2 Configuration
- **IP Address:** `192.168.1.4`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `192.168.1.1`

#### 💻 PC3 Configuration
- **IP Address:** `192.168.1.5`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `192.168.1.1`

---

## 4. FTP Server Configuration

### Step A: Configure Server IP
**Server → Desktop → IP Configuration**

- **IP Address:** `10.10.10.2`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `10.10.10.1`

### Step B: Enable & Configure FTP Service
**Server → Services → FTP**

1. Service **On** রেডিও বাটন নির্বাচন করুন।
2. **User Setup** সেকশনে Credential ও Permission সেট করুন:
   - **Username:** `admin`
   - **Password:** `5415@` (অথবা আপনার পছন্দের পাসওয়ার্ড)
   - **Permissions:** ✅ Write, ✅ Read, ✅ Delete, ✅ Rename, ✅ List (RWDNL)
3. **Add** বাটনে ক্লিক করুন।

*(বিকল্প হিসেবে ডিফল্ট `cisco` / `cisco` ইউজারও ব্যবহার করা যেতে পারে)*

---

## 5. Test Network Connectivity

PC0 (বা PC1) থেকে Connectivity যাচাই করতে **Desktop → Command Prompt** ওপেন করুন:

```cmd
C:\> ipconfig
C:\> ping 192.168.1.1
C:\> ping 10.10.10.2
```

### Expected Output
```text
Pinging 10.10.10.2 with 32 bytes of data:
Reply from 10.10.10.2: bytes=32 time<1ms TTL=127
Reply from 10.10.10.2: bytes=32 time<1ms TTL=127
```

> 💡 **Note:** Ping সফল না হলে FTP Client কাজ করবে না। Ping ব্যর্থ হলে Cable Connections, IP, Subnet Mask এবং Router Interface চেক করুন।

---

## 6. Create & Verify Local Files on PC

PC-এর Command Prompt-এ স্থানীয় ফাইল চেক করুন:

```cmd
C:\> dir
```

### Output:
```text
Volume in drive C has no label.
Volume Serial Number is 5E12-4AF3
Directory of C:\

1/1/1970   6:00 PM            26 sampleFile.txt
               1 File(s)      26 bytes
```

### 📝 টেক্সট ফাইল তৈরি করতে চাইলে:
Packet Tracer-এর **Desktop → Text Editor** ব্যবহার করে নতুন ফাইল তৈরি করে **`sampleFile.txt`** অথবা **`ftb.txt`** নামে Save করুন।
> ⚠️ **পরামর্শ:** ফাইলের নামে **Space** ব্যবহার না করাই উত্তম।

---

## 7. Connect to the FTP Server

PC-এর Command Prompt থেকে FTP Server-এ কানেক্ট করুন:

```cmd
C:\> ftp 10.10.10.2
```

### Step-by-Step Login Prompt:

```text
Trying to connect...10.10.10.2
Connected to 10.10.10.2
220- Welcome to PT Ftp server
Username: admin
331- Username ok, need password
Password: 
230- Logged in
(passive mode On)
ftp>
```

---

## 8. FTP Commands Detailed Explanation

Packet Tracer Client-এর `ftp>` প্রম্পটে `?` প্রেস করলে নিচের কমান্ডগুলো পাওয়া যায়:

```text
ftp> ?
    ?           cd          delete      dir         get         
    help        passive     put         pwd         quit        
    rename      
```

### Commands Detailed Table (বাংলা ব্যাখ্যা)

| Command | Usage Example | Explanation (বিবরণ) |
| :--- | :--- | :--- |
| **`?`** | `ftp> ?` | সমর্থিত (Supported) সকল FTP Command-এর তালিকা দেখায়। |
| **`help`** | `ftp> help` | Help মেনু ও কমান্ডের বিবরণ দেখায়। |
| **`dir`** | `ftp> dir` | FTP Server-এ থাকা ফাইল এবং ডিরেক্টরির তালিকা দেখায়। |
| **`pwd`** | `ftp> pwd` | FTP Server-এর বর্তমান Working Directory দেখায়। |
| **`put`** | `ftp> put sampleFile.txt` | Local PC থেকে Server-এ File Upload করে। |
| **`get`** | `ftp> get sampleFile.txt` | FTP Server থেকে Local PC-তে File Download করে। |
| **`delete`** | `ftp> delete test.txt` | Server-এ থাকা নির্দিষ্ট ফাইল Delete/মুছে ফেলে। |
| **`rename`** | `ftp> rename old.txt new.txt` | Server-এর ফাইলের নাম পরিবর্তন করে। |
| **`cd`** | `ftp> cd foldername` | Server-এর ডিরেক্টরি/ফোল্ডার পরিবর্তন করে। |
| **`passive`** | `ftp> passive` | FTP-এর Passive Mode ON/OFF (Toggle) করে। |
| **`quit`** | `ftp> quit` | FTP সেশন শেষ করে PC-র মূল প্রম্পটে (`C:\>`) ফিরে আসে। |

---

## 9. Uploading Files (`put`)

### Action: Uploading `sampleFile.txt` to Server

```ftp
ftp> dir
ftp> put sampleFile.txt
```

### Upload Verification Output:
```text
250 File transfer started
226 Transfer complete
```

### ❌ Common Error & Solution:
আপনি যদি স্পেসযুক্ত ফাইলের নাম দিন, যেমন:
```ftp
ftp> put "ftp test.txt"
Error opening "ftp test.txt" (No such file or directory)
```
> **কারণ:** Packet Tracer-এর FTP Client স্পেসযুক্ত ফাইলের নাম সঠিকভাবে হ্যান্ডেল করতে পারে না।
> **সমাধান:** স্পেস ছাড়া নাম ব্যবহার করুন (যেমন: `sampleFile.txt` বা `ftb.txt`)।

---

## 10. Downloading Files (`get`)

Server থেকে Local PC-তে ফাইল ডাউনলোডের নির্দেশ:

```ftp
ftp> get sampleFile.txt
```

### Download Verification Output:
```text
250 File transfer started
226 Transfer complete
```

সেশন শেষে প্রম্পট বের করে চেক করুন:
```ftp
ftp> quit
```
```cmd
C:\> dir
```

---

## 11. File Management (`delete` & `rename`)

> ⚠️ **Warning:** এগুলো প্র্যাকটিস সার্ভারে করার সময় সতর্ক থাকুন।

### ✏️ Rename Command:
```ftp
ftp> rename sampleFile.txt renamedFile.txt
```
*Output: `250 File renamed successfully`*

### 🗑️ Delete Command:
```ftp
ftp> delete renamedFile.txt
```
*Output: `250 File deleted successfully`*

---

## 12. Complete Lab Workflow Summary

```cmd
:: 1. PC Command Prompt Step
C:\> ipconfig
C:\> ping 10.10.10.2
C:\> dir
C:\> ftp 10.10.10.2

:: 2. Authentication Step
Username: admin
Password: 5415@

:: 3. FTP File Operations
ftp> ?
ftp> pwd
ftp> dir
ftp> put sampleFile.txt
ftp> dir
ftp> get sampleFile.txt
ftp> quit

:: 4. Verify Local Files
C:\> dir
```

---

## 13. Common Errors & Solutions

| Error Message | Possible Cause | Troubleshooting Steps |
| :--- | :--- | :--- |
| `Connection timed out` | IP/Gateway কনফিগারেশনে ভুল বা Router Interface বন্ধ (`shutdown`) | IP Address, Default Gateway এবং Router Interface Status পরীক্ষা করুন। |
| `Connection refused` | Server-এ FTP Service **OFF** হয়ে আছে | Server → Services → FTP তে গিয়ে Service **ON** করুন। |
| `530 Login incorrect` | ভুল Username বা Password | Server-এর FTP User Configuration থেকে তথ্য মিলিয়ে নিন। |
| `Error opening ... (No file)` | PC-তে ফাইলের অস্তিত্ব নেই বা নামে স্পেস আছে | PC-তে `C:\> dir` দিয়ে ফাইলের নাম নিশ্চিত করুন। |
| `Permission denied` | ইউজার অ্যাকাউন্টে Write/Read পারমিশন নেই | Server FTP Options থেকে `Write`, `Read`, `Delete` পারমিশন চেক করুন। |

---

## 14. CCNA Viva Questions & Answers

### **Q1. What is FTP and which OSI layer does it operate at?**
> **Answer:** FTP (File Transfer Protocol) is a network protocol used to transfer files between a client and a server. It operates at the **Application Layer (Layer 7)** of the OSI model.

---

### **Q2. What are the default port numbers used by FTP?**
> **Answer:** FTP uses two TCP ports:
> - **Port 21:** Control Connection (Commands and Authentication)
> - **Port 20:** Data Connection (Actual File Transfer)

---

### **Q3. What is the difference between `put` and `get` commands?**
> **Answer:**
> - **`put`**: Uploads a file from the local client machine to the remote FTP server.
> - **`get`**: Downloads a file from the remote FTP server to the local client machine.

---

### **Q4. Why is a Default Gateway configured on PC0 and the FTP Server?**
> **Answer:** The Default Gateway allows devices to communicate outside their local IP subnet. Since PC0 (`192.168.1.0/24`) and the Server (`10.10.10.0/24`) belong to different subnets, routing through the router interfaces is mandatory.

---

### **Q5. Is traditional FTP secure? What are its secure alternatives?**
> **Answer:** No, traditional FTP transmits passwords and data in plain text without encryption. Secure alternatives include:
> - **SFTP (SSH File Transfer Protocol)** - Uses SSH (Port 22)
> - **FTPS (FTP over SSL/TLS)** - Encrypts standard FTP sessions

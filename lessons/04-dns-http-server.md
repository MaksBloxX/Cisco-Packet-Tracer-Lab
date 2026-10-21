# লেসন ০৪ · DNS Server ও HTTP Web Server

> **নেভিগেশন:** [⬅ লেসন ০৩](03-dhcp.md) · [🏠 হোম](../README.md) · [পরের লেসন ০৫ ➡](05-vlan.md)

| 🎯 লক্ষ্য | ⏱️ সময় | 📊 লেভেল | 🧰 ল্যাব ফাইল |
| :--- | :--- | :--- | :--- |
| Packet Tracer-এ DNS + HTTP Server সেটআপ, DHCP সহ সম্পূর্ণ নেটওয়ার্ক | ~৫০ মিনিট | 🟡 Beginner–Intermediate | `lesson-04-dns-http-server.pkt` ✍️ তুমি বানাবে (নাম এই রাখো) |

**Tags:** `#dns` `#http` `#web-server` `#dhcp` `#domain` `#server-config`

---

## 🎯 এই লেসনে যা শিখবে

1. **DNS কী** এবং Domain Name কীভাবে IP-তে রূপান্তর হয়
2. Server-এ **Static IP** সেট করা (সার্ভারের IP কখনো DHCP নয়!)
3. DNS Service-এ **A Record** (Name → IP) যোগ করা
4. **HTTP Service** চালু করে ছোট ওয়েবসাইট হোস্ট করা
5. PC থেকে **ডোমেন নাম দিয়ে** ওয়েবসাইট খোলা (DHCP + DNS একসাথে)

---

# 📖 Part 1 — DNS কী?

**DNS** = *Domain Name System* — মানুষের বোঝার উপযোগী **Domain Name** (`www.google.com`) কে মেশিনের উপযোগী **IP Address**-এ রূপান্তর (Resolve) করে।

* **DNS ছাড়া:** `192.168.1.100` — এই আইপি মুখস্থ করে টাইপ করতে হতো
* **DNS সহ:** `www.office.local` — সহজ নাম; DNS ব্যাকগ্রাউন্ডে আইপি বের করে দেয়

### 💡 তিনটি সার্ভিসের পার্থক্য

| সার্ভিস | কী করে | মনে রাখার ট্রিক |
| :--- | :--- | :--- |
| **DNS** | নাম → IP খুঁজে বের করে | "ফোনবুক" 📖 |
| **DHCP** | Client-কে স্বয়ংক্রিয় IP/Gateway দেয় | "IP বিতরণকারী" 🎫 |
| **Default Gateway** | বাইরের নেটওয়ার্কে যাওয়ার দরজা | "প্রধান ফটক" 🚪 |

---

# 🧩 Part 2 — Network Topology

১টি Router, ১টি Switch, ২টি PC, ১টি Server:

```text
                    Router R1
                  192.168.1.1
                        │
                     Switch0
                  ┌─────┼─────┐
                 PC0  Server0  PC1
                DHCP   DNS/Web  DHCP
                      192.168.1.100
```

### 📋 Addressing Table (`192.168.1.0/24`)

| Device | IP Address | Subnet Mask | Default Gateway | DNS Server | কাজ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **R1** (G0/0) | `192.168.1.1` | `255.255.255.0` | N/A | N/A | Gateway + DHCP Server |
| **Server0** (Fa0) | `192.168.1.100` **(Static)** | `255.255.255.0` | `192.168.1.1` | `192.168.1.100` (নিজে) | DNS + HTTP Server |
| **PC0** | DHCP | `255.255.255.0` | `192.168.1.1` | `192.168.1.100` | Client |
| **PC1** | DHCP | `255.255.255.0` | `192.168.1.1` | `192.168.1.100` | Client |

> 📌 **নিয়ম:** সার্ভারের IP সবসময় **Static** — যাতে কখনো তার IP বদলে না যায়।

**Domain:** `www.office.local` → `192.168.1.100`

### 🔌 Connection Table (Copper Straight-Through)

| From | Port | To | Port |
| :--- | :--- | :--- | :--- |
| **R1** | G0/0 | **Switch0** | G0/1 |
| **Server0** | Fa0 | **Switch0** | Fa0/1 |
| **PC0** | Fa0 | **Switch0** | Fa0/2 |
| **PC1** | Fa0 | **Switch0** | Fa0/3 |

---

# ⚙️ Part 3 — Router Configuration (Gateway + DHCP)

```cisco
enable
configure terminal
hostname R1

interface gigabitEthernet 0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

! সার্ভারের Static IP সুরক্ষিত রাখতে Exclude
ip dhcp excluded-address 192.168.1.1 192.168.1.100

ip dhcp pool OFFICE
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 192.168.1.100
 exit

end
copy running-config startup-config
```

> 💡 **নতুন কমান্ড:** `dns-server 192.168.1.100` — DHCP ক্লায়েন্টরা স্বয়ংক্রিয়ভাবে DNS Server হিসেবে `192.168.1.100` পাবে। `ip dhcp excluded-address` `.1` থেকে `.100` পর্যন্ত দিয়েছি যাতে সার্ভারের `.100`-ও সুরক্ষিত থাকে।

---

# 🖥️ Part 4 — Server0 Configuration

## Step 1: Static IP

**Server0 → Desktop → IP Configuration → Static:**

```text
IP Address:      192.168.1.100
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.1
DNS Server:      192.168.1.100
```

## Step 2: DNS Service চালু

**Server0 → Services → DNS:**
1. **DNS Service** = **ON** করো
2. **A Record** যোগ করো:

| Field | Value |
| :--- | :--- |
| **Name** | `www.office.local` |
| **Type** | A Record |
| **Address** | `192.168.1.100` |
3. **Add** ক্লিক করো ✅

## Step 3: HTTP Web Service চালু

**Server0 → Services → HTTP (or WEB):**
1. **HTTP** ও **HTTPS** = **ON** (সাধারণত ডিফল্ট ON থাকে)
2. **index.html** ফাইলটি সম্পাদনা করে চাইলে নিজের টেক্সট বসাতে পারো:

```html
<html><body><h1>Welcome to Office Network!</h1></body></html>
```

---

# 💻 Part 5 — PC Configuration

PC0 ও PC1 দুটোতেই: **Desktop → IP Configuration → DHCP**

```text
PC0: IP 192.168.1.101 (approx)  Gateway 192.168.1.1  DNS 192.168.1.100
PC1: IP 192.168.1.102 (approx)  Gateway 192.168.1.1  DNS 192.168.1.100
```
*(নির্দিষ্ট IP ভিন্ন হতে পারে — `ipconfig` দিয়ে দেখে নাও)*

---

# 🧪 Part 6 — DNS ও Web Testing

## Test 1: Server-এ Ping
PC0 → Command Prompt:
```text
ping 192.168.1.100
```
✅ Reply আসলে Connectivity ঠিক আছে।

## Test 2: ব্রাউজারে ডোমেন টেস্ট
PC0 → **Desktop → Web Browser**, Address Bar-এ:
```text
www.office.local
```
✅ **"Welcome to Office Network!"** (বা index.html-এর কনটেন্ট) দেখা গেলে DNS + HTTP দুটোই সফল!

## Test 3: PC1 থেকেও একইভাবে
```text
www.office.local
```
✅ দুই Client-ই একই সার্ভারে পৌঁছাচ্ছে।

---

# 🔁 Part 7 — লজিক: DHCP + DNS একসাথে কীভাবে কাজ করে?

```text
১. PC0 DHCP-তে IP চায় → Router দেয়: IP + Gateway + DNS=192.168.1.100
২. PC0-এর ব্রাউজারে www.office.local টাইপ
৩. PC0 → DNS Server (192.168.1.100): "www.office.local এর IP কী?"
৪. DNS Server → PC0: "192.168.1.100"
৫. PC0 → HTTP Server (192.168.1.100): "index.html দাও"
৬. HTTP Server → PC0: 📄 "Welcome to Office Network!"
```

> 🧠 **মনে রাখো:** DNS শুধু **নাম থেকে IP** দেয় — আসল ওয়েবপেজটা **HTTP Server** পাঠায়। তাই দুটো Service-ই ON করতে হয়।

---

# ❌ Troubleshooting

| সমস্যা | কী চেক করবে |
| :--- | :--- |
| `ping 192.168.1.100` হয় না | Server-এর Static IP, কেবল, `no shutdown` |
| IP টাইপ করলে সাইট খোলে, নাম দিলে না | DNS Service ON? A Record সঠিক? PC-তে DNS IP `192.168.1.100`? |
| DNS Request Failed | `www.office.local` স্পেলিং মেলাও (`.local` বাদ যায় না) |
| PC-তে DNS IP আসছে না | Router-এর DHCP Pool-এ `dns-server 192.168.1.100` আছে কি না |
| Website খুলতে চাইলে ভুল পেজ | HTTP Service ON কি না, `index.html` আছে কি না দেখো |

---

# ✅ Final Checklist

| Task | Expected Result |
| :--- | :--- |
| Server0 Static IP `192.168.1.100` | ✅ |
| DNS ON + A Record (`www.office.local` → `192.168.1.100`) | ✅ |
| HTTP ON | ✅ |
| Router DHCP Pool-এ `dns-server 192.168.1.100` | ✅ |
| PC0/PC1 DHCP-তে IP + DNS পাচ্ছে | ✅ |
| ব্রাউজারে `www.office.local` খুলছে | ✅ |

---

# 🔮 পরের ধাপ

একই সুইচে সবাই এক নেটওয়ার্কে আছে। এবার শিখব **VLAN** — একটি সুইচকে ভাগ করে আলাদা আলাদা সুরক্ষিত গ্রুপ বানানো → [লেসন ০৫ · VLAN](05-vlan.md)

---

> **নেভিগেশন:** [⬅ লেসন ০৩](03-dhcp.md) · [🏠 হোম](../README.md) · [পরের লেসন ০৫ ➡](05-vlan.md)

**এই লেসনের Tags:** `#dns` `#a-record` `#http` `#web-browser` `#static-ip` `#server`

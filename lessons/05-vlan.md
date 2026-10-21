# লেসন ০৫ · VLAN Configuration ও VLAN Isolation

> **নেভিগেশন:** [⬅ লেসন ০৪](04-dns-http-server.md) · [🏠 হোম](../README.md) · [পরের লেসন ০৬ ➡](06-trunk-inter-vlan.md)

| 🎯 লক্ষ্য | ⏱️ সময় | 📊 লেভেল | 🧰 ল্যাব ফাইল |
| :--- | :--- | :--- | :--- |
| একটি Switch-এ VLAN তৈরি, Port Assign ও VLAN Isolation প্রমাণ | ~৪৫ মিনিট | 🟡 Intermediate | `lesson-05-vlan.pkt` ✍️ তুমি বানাবে (নাম এই রাখো) |

**Tags:** `#vlan` `#switch` `#broadcast-domain` `#isolation` `#access-port` `#vlan-10-20`

---

## 🎯 এই লেসনে যা শিখবে

1. **VLAN কী** এবং কেন এটি নেটওয়ার্ক নিরাপত্তা ও পারফরম্যান্সের জন্য দরকার
2. Switch-এ `vlan` কমান্ড দিয়ে **VLAN তৈরি** করা
3. `switchport access vlan` দিয়ে **Port Assign** করা
4. `show vlan brief` দিয়ে **ভেরিফিকেশন**
5. **একই VLAN = Ping ✅**, **ভিন্ন VLAN = Ping ❌** — Isolation প্রমাণ

---

# 📖 Part 1 — VLAN কী?

**VLAN** = *Virtual Local Area Network* — একটি ফিজিক্যাল সুইচকে সফটওয়্যারের মাধ্যমে একাধিক **আলাদা লজিক্যাল সুইচে** ভাগ করা।

### 🔹 VLAN ছাড়া (সবাই এক Broadcast Domain):
```text
        Switch (সব এক নেটওয়ার্ক)
     ┌────┼────┬────┐
    PC0  PC1  PC2  PC3    ← সবার ট্রাফিক একসাথে, একটি ভুল ব্রডকাস্ট = সবাই ক্ষতিগ্রস্ত
```

### 🔹 VLAN সহ (আলাদা আলাদা Broadcast Domain):
```text
        Switch
     ┌────┼────┬────┐
    PC0  PC1  PC2  PC3
   [─── VLAN 10 ───] [─── VLAN 20 ───]
      CSE গ্রুপ         EEE গ্রুপ
```

## 🧠 VLAN কেন ব্যবহার করা হয়?

| সুবিধা | ব্যাখ্যা |
| :--- | :--- |
| **🔒 নিরাপত্তা** | VLAN 10-এর ইউজার VLAN 20-এর তথ্য দেখতে পারবে না |
| **📡 Broadcast Control** | ব্রডকাস্ট ট্রাফিক নিজের VLAN-এই সীমাবদ্ধ থাকে |
| **⚙️ সহজ ব্যবস্থাপনা** | ইউজারকে ঘর বদলানোর দরকার নেই — শুধু Port-এর VLAN বদলালেই হবে |
| **🚀 পারফরম্যান্স** | ছোট ছোট গ্রুপে ট্রাফিক ভাগ হয়ে নেটওয়ার্ক দ্রুত চলে |

---

# 🧩 Part 2 — Lab Setup

**ডিভাইস:** ১ × Switch (2960) · ৪ × PC (PC-PT)

```text
                 Switch0
        ┌────┬────┬────┬────┐
      Fa0/1 Fa0/2 Fa0/3 Fa0/4
        │    │     │     │
       PC0  PC1   PC2   PC3
      192.168.10.1  192.168.10.2   192.168.20.1  192.168.20.2
```

| VLAN | নাম | Port | Subnet | PC |
| :---: | :--- | :--- | :--- | :--- |
| **10** | CSE | Fa0/1, Fa0/2 | `192.168.10.0/24` | PC0, PC1 |
| **20** | EEE | Fa0/3, Fa0/4 | `192.168.20.0/24` | PC2, PC3 |

### 🔌 Cable: সবক্ষেত্রে **Copper Straight-Through** (PC ↔ Switch)

---

# ⚙️ Part 3 — Switch Configuration

## Step 1: VLAN তৈরি করো

```cisco
enable
configure terminal
hostname SW1

vlan 10
 name CSE
 exit

vlan 20
 name EEE
 exit
```

**যাচাই:**
```cisco
show vlan brief
```
```text
VLAN Name                             Status    Ports
10   CSE                              active
20   EEE                              active
```

## Step 2: Port-গুলো VLAN-এ Assign করো

**VLAN 10 (CSE) — Fa0/1 ও Fa0/2:**
```cisco
interface range fastEthernet 0/1 - 2
 switchport mode access
 switchport access vlan 10
 exit
```

**VLAN 20 (EEE) — Fa0/3 ও Fa0/4:**
```cisco
interface range fastEthernet 0/3 - 4
 switchport mode access
 switchport access vlan 20
 exit

end
copy running-config startup-config
```

> 💡 `switchport mode access` = এই পোর্টটি শুধুমাত্র একটি VLAN-এর End Device-এর জন্য (PC, Printer)।

**Port Assignment যাচাই:**
```cisco
show vlan brief
```
```text
10   CSE                              active    Fa0/1, Fa0/2
20   EEE                              active    Fa0/3, Fa0/4
```

---

# 💻 Part 4 — PC IP Configuration (Static)

### 🔹 VLAN 10 (CSE): `192.168.10.0/24`
| PC | IP | Mask | Gateway |
| :--- | :--- | :--- | :--- |
| PC0 | `192.168.10.1` | `255.255.255.0` | `192.168.10.254` *(রাউটার নেই তাই ঐচ্ছিক)* |
| PC1 | `192.168.10.2` | `255.255.255.0` | `192.168.10.254` |

### 🔹 VLAN 20 (EEE): `192.168.20.0/24`
| PC | IP | Mask | Gateway |
| :--- | :--- | :--- | :--- |
| PC2 | `192.168.20.1` | `255.255.255.0` | `192.168.20.254` |
| PC3 | `192.168.20.2` | `255.255.255.0` | `192.168.20.254` |

> 📌 **গুরুত্বপূর্ণ:** ভিন্ন VLAN = ভিন্ন Subnet। VLAN 10 → `10.x`, VLAN 20 → `20.x` — এই নিয়মটা মনে রাখলে পরে Inter-VLAN Routing-এ কোনো সমস্যা হবে না।

---

# 🧪 Part 5 — Ping Test ও Isolation প্রমাণ

### Test 1: একই VLAN (PC0 → PC1) ✅
```cmd
ping 192.168.10.2
```
👉 **Reply from 192.168.10.2** — সফল! কারণ দুজনই VLAN 10-এ।

### Test 2: একই VLAN (PC2 → PC3) ✅
```cmd
ping 192.168.20.2
```
👉 **Reply** — সফল! দুজনই VLAN 20-এ।

### Test 3: ভিন্ন VLAN (PC0 → PC2) ❌
```cmd
ping 192.168.20.1
```
👉 **Request timed out / Destination host unreachable** — ইচ্ছাকৃতভাবে ব্যর্থ!

> ❓ **কেন ব্যর্থ?** — VLAN 10 ও VLAN 20 আলাদা Broadcast Domain। সুইচ এক VLAN-এর ফ্রেম অন্য VLAN-এ পাঠাবে না। এই আলাদাত্বটাই **VLAN Isolation**। দুই VLAN-এর মধ্যে যোগাযোগ করতে হলে **Router** (Inter-VLAN Routing) লাগবে — যা [লেসন ০৬](06-trunk-inter-vlan.md)-এ শিখব।

---

# 🔍 Part 6 — Verification Commands

| Command | কাজ |
| :--- | :--- |
| `show vlan brief` | সব VLAN ও তাদের Port দেখা |
| `show interfaces switchport` | নির্দিষ্ট Port-এর Mode/VLAN দেখা |
| `show mac address-table` | কোন MAC কোন পোর্টে শেখা হয়েছে |
| `show running-config` | পুরো কনফিগ দেখা |

---

# 🧠 Quick Cheat-Sheet

| কাজ | কমান্ড |
| :--- | :--- |
| VLAN তৈরি | `vlan [ID]` + `name [NAME]` |
| Port-এ VLAN Assign | `switchport mode access` + `switchport access vlan [ID]` |
| একসাথে একাধিক Port | `interface range fa0/1 - 2` |
| VLAN তালিকা | `show vlan brief` |
| সেভ | `copy running-config startup-config` |

---

# ❌ Troubleshooting

| সমস্যা | সমাধান |
| :--- | :--- |
| একই VLAN-এও Ping হয় না | PC-র IP একই Subnet-এ কি না, কেবল সঠিক কি না দেখো |
| Port ভুল VLAN-এ | `show vlan brief` দিয়ে Port Assignment মেলাও |
| `switchport` কমান্ড কাজ করছে না | সুইচ হলেই চলবে (L3 Switch/Router-এ ভিন্ন সিনট্যাক্স) |
| ভিন্ন VLAN-এ Ping হয়ে যাচ্ছে | VLAN Assign ভুল হয়েছে — পোর্টগুলো আবার চেক করো |

---

# ✅ Final Checklist

| Task | Expected Result |
| :--- | :--- |
| VLAN 10 (CSE) + VLAN 20 (EEE) তৈরি | ✅ |
| Fa0/1–2 → VLAN 10, Fa0/3–4 → VLAN 20 | ✅ |
| PC0↔PC1 Ping (সমান VLAN) | ✅ Success |
| PC2↔PC3 Ping (সমান VLAN) | ✅ Success |
| PC0→PC2 Ping (ভিন্ন VLAN) | ❌ Fail (Isolation প্রমাণিত) |
| `show vlan brief` | সঠিক Port Assignment দেখাচ্ছে ✅ |

---

# 🔮 পরের ধাপ

VLAN-এর Isolation বুঝেছ। এবার জানো **একাধিক সুইচে কীভাবে VLAN বহন করতে হয় (Trunk Link)** এবং **Router দিয়ে কীভাবে ভিন্ন VLAN-গুলোকে যোগাযোগ করাতে হয় (Inter-VLAN Routing)** → [লেসন ০৬ · Trunk ও Inter-VLAN Routing](06-trunk-inter-vlan.md)

---

> **নেভিগেশন:** [⬅ লেসন ০৪](04-dns-http-server.md) · [🏠 হোম](../README.md) · [পরের লেসন ০৬ ➡](06-trunk-inter-vlan.md)

**এই লেসনের Tags:** `#vlan` `#vlan-isolation` `#access-port` `#broadcast-domain` `#show-vlan-brief`

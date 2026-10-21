# লেসন ০৯ · বাস্তব নেটওয়ার্ক হার্ডওয়্যার পরিচিতি (Real Hardware Guide)

> **নেভিগেশন:** [⬅ লেসন ০৮](08-final-project.md) · [🏠 হোম](../README.md) · [পরের লেসন ১০ ➡](10-practice-lab.md)

| 🎯 লক্ষ্য | ⏱️ সময় | 📊 লেভেল | 🧰 pkt ফাইল |
| :--- | :--- | :--- | :--- |
| Packet Tracer-এর প্রতিটি ডিভাইস/কেবল বাস্তবে কেমন দেখায় — আসল ছবি দিয়ে পরিচয় | ~২৫ মিনিট | 🟢 সবার জন্য | নেই (শুধু দেখার লেসন) |

**Tags:** `#hardware` `#real-device` `#cable` `#rj45` `#sfp` `#rack` `#console-cable`

---

## 🎯 এই লেসনে যা শিখবে

1. Packet Tracer-এর **Router, Switch বাস্তবে কেমন** — কোন পোর্টগুলো কোথায়
2. **কেবলের আসল রূপ** — Straight-Through, Cross-Over, Console (Rollover)
3. **RJ-45, SFP, Fiber** কানেক্টর ও মডিউল
4. **Crimping Tool** দিয়ে কেবল তৈরির সরঞ্জাম
5. **Rack ও Patch Panel** — আসল ডেটা সেন্টারে নেটওয়ার্ক কেমন থাকে
6. **PT Device ↔ Real Device** ম্যাপিং টেবিল

> 📌 এই লেসনে কোনো কনফিগারেশন নেই — শুধু **চোখে দেখা ও মনে রাখা**। ল্যাব পরীক্ষা/ইন্টারন্টে এই সব বাস্তব ডিভাইস দেখলে যেন অচেনা না লাগে!

---

# 📡 Part 1 — বাস্তব Router (Real Router)

Packet Tracer-এ তুমি যে **1941 Router** ব্যবহার করো, বাস্তবে সেটা ঠিক এরকম:

![Cisco 1941 Router Back Panel](images/router-cisco-1941-back-panel.jpg)
*▲ Cisco 1941 Router — Back Panel (উপরে: পুরো রাউটার, নিচে: পোর্টগুলোর কাছাকাছি দৃশ্য)*

### 🔍 বাস্তব Router-এ যা যা থাকে

| পোর্ট/অংশ | কেমন দেখায় | কাজ |
| :--- | :--- | :--- |
| **GigabitEthernet 0/0, 0/1** | হলুদ রঙের RJ-45 পোর্ট | PT-তে যেমন `G0/0`, `G0/1` — LAN/WAN সংযোগ |
| **Console Port** | সবচেয়ে বাঁদিকে ছোট RJ-45 পোর্ট, "CONSOLE" লেখা | প্রথমবার কনফিগ করতে **Console কেবল** দিয়ে ল্যাপটপ জোড়া |
| **AUX Port** | Console-এর পাশে | পুরনো মডেম/রিমোট অ্যাক্সেস (আজকাল কম ব্যবহার) |
| **USB Port** | আয়তকার ছোট পোর্ট | ফ্ল্যাশ/কনফিগ কপি |
| **WIC / EHWIC Slots** | ঢোকানো কার্ডের স্লট | Serial বা অতিরিক্ত ইন্টারফেস কার্ড লাগানো যায় |
| **Power Switch + Socket** | পিছনে পাওয়ার | চালু/বন্ধ |

> 💡 **মনে রাখো:** PT-তে তুমি যে সব `interface g0/0`, `console` দেখো — বাস্তবে সেগুলো এই রাউটারের **শারীরিক পোর্ট**। কনফিগারেশন কমান্ড হুবহু একই চলে!

### বাস্তবে জনপ্রিয় Router মডেল

| মডেল | কোথায় ব্যবহার | PT-তে সমতুল্য |
| :--- | :--- | :--- |
| **Cisco 1941** | ছোট অফিস/ল্যাব | 1941 (হুবহু এটাই) |
| **Cisco 2911 / 4331 (ISR)** | মাঝারি অফিস | 2911 / 4331 |
| **Home Router (TP-Link/Asus)** | বাসাবাড়ি | Packet Tracer-এ নেই (সমতুল্য: Home Router icon) |

---

# 🔌 Part 2 — বাস্তব Switch (Real Switch)

তোমার ল্যাবের **Cisco 2960 Switch** বাস্তবে এরকম:

![Cisco 2960 Switch Front Panel](images/switch-cisco-2960-front.jpg)
*▲ Cisco Catalyst 2960 Switch — Front Panel (সারি সারি পোর্ট, ডানে Uplink ও প্রতিটি পোর্টে LED)*

### 🔍 বাস্তব Switch-এ যা যা থাকে

| অংশ | কেমন দেখায় | কাজ |
| :--- | :--- | :--- |
| **Fa0/1 – Fa0/24 (বা 48)** | সামনে সারি সারি RJ-45 পোর্ট | PC, Printer, IP Phone লাগানো — PT-তে যেমন `Fa0/1` |
| **GigabitEthernet Uplink (SFP)** | পোর্টের পাশে ছোট গর্তের স্লট | Fiber/SFP মডিউল — রাউটার বা অন্য সুইচে Uplink |
| **Console Port** | পাশে আলাদা | সুইচ কনফিগ করতে |
| **LED Lights** | প্রতিটি পোর্টে ছোট বাতি | 🟢 সবুজ = Link Up, 🟠 কমলা = STP Learning, ⚫ বন্ধ = Link Down |
| **System LED** | সামনে SYST | সুইচ চালু আছে কি না |

> 💡 **ল্যাব টিপ:** তুমি যখন কেবল লাগাও, তখন PT-তে যে Amber→Green বাতি দেখো — বাস্তবেও হুবহু সেই LED-ই সবুজ হয়। লোকাল পরীক্ষায় LED দেখে Link Status বলতে বলতে পারে!

---

# 🔌 Part 3 — বাস্তব কেবল (Real Cables)

## ১. Ethernet কেবল + RJ-45 কানেক্টর

![Cat6 Cable with RJ-45](images/cable-cat6-rj45.jpg)
*▲ Cat6 Ethernet কেবল — সবুজ, নীল, হলুদ রঙে থাকে; শেষে স্বচ্ছ **RJ-45** কানেক্টর (8P8C)*

| কেবল | কোথায় ব্যবহার (PT-তে যেমন) | বাস্তবে কেমন |
| :--- | :--- | :--- |
| **Copper Straight-Through** | PC↔Switch, Switch↔Router, PC↔Hub | দুই প্রান্তে **একই রঙের সাজানো** তার (T568B—T568B) — সবচেয়ে বেশি ব্যবহৃত |
| **Copper Cross-Over** | Switch↔Switch, Router↔Router, PC↔PC | এক প্রান্ত T568A, অন্য প্রান্ত T568B — রঙ দুই প্রান্তে আলাদা |
| **Console (Rollover)** | PC ↔ Router/Switch Console Port | হালকা নীল (Light Blue) কেবল; তারগুলো **উল্টো ক্রমে** যুক্ত — এক প্রান্ত RJ-45, অন্য প্রান্ত DB9 (COM পোর্ট) |

![Console Rollover Cable](images/cable-console-rollover.jpg)
*▲ Cisco Console Cable — এক প্রান্তে RJ-45 (রাউটারের CONSOLE), অন্য প্রান্তে DB9 (কম্পিউটারের COM/Serial) — বাংলায় "রোলোভার কেবল"*

### 🎨 T568A vs T568B রঙের ক্রম (মনে রাখলে কেবল বানাতে পারবে)

| পিন | T568B (বেশি ব্যবহৃত) | T568A |
| :---: | :--- | :--- |
| 1 | 🟧 সাদা-কমলা | 🟩 সবুজ-সাদা |
| 2 | 🟧 কমলা | 🟩 সবুজ |
| 3 | 🟩 সবুজ-সাদা | 🟧 কমলা-সাদা |
| 4 | 🟦 নীল | 🟦 নীল |
| 5 | 🟦 সাদা-নীল | 🟦 সাদা-নীল |
| 6 | 🟩 সবুজ | 🟧 কমলা |
| 7 | 🟫 সাদা-বাদামি | 🟫 সাদা-বাদামি |
| 8 | 🟫 বাদামি | 🟫 বাদামি |

> **সহজ নিয়ম:**
> * **Straight-Through** = দুই প্রান্তে একই স্ট্যান্ডার্ড (B—B বা A—A) → ভিন্ন ধরনের ডিভাইস
> * **Cross-Over** = এক প্রান্ত A, অন্য প্রান্ত B → একই ধরনের ডিভাইস
> * **Console** = উল্টো ক্রম (1↔8, 2↔7, 3↔6, 4↔5)

## ২. Fiber ও SFP মডিউল

![SFP Fiber Module](images/sfp-fiber-lc-module.jpg)
*▲ SFP Transceiver Module — সুইচের Uplink স্লটে ঢোকে, সামনে **LC** কানেক্টর দিয়ে Fiber কেবল লাগে*

| অংশ | কাজ |
| :--- | :--- |
| **SFP Module** | সুইচের ছোট স্লটে ঢোকানো মডিউল — এতে Fiber বা তামার Uplink লাগে |
| **Fiber Cable (LC Connector)** | আলো দিয়ে ডেটা — লম্বা দূরত্ব (কয়েক কিমি) ও উচ্চ গতি |
| **কেন Fiber?** | বিল্ডিং-বিল্ডিং সংযোগ, ডেটা সেন্টার Uplink — বিদ্যুৎচৌম্বকীয় হস্তক্ষেপ নেই |

---

# 🛠️ Part 4 — কেবল তৈরির সরঞ্জাম

![Crimping Tool Kit](images/tool-rj45-crimping-kit.jpg)
*▲ RJ-45 Crimping Kit — Crimping Tool, Wire Stripper, Cable Tester একসাথে*

| সরঞ্জাম | কাজ |
| :--- | :--- |
| **Crimping Tool** | RJ-45 কানেক্টরে তার চেপে (crimp) জোড়া লাগানো |
| **Wire Stripper** | কেবলের আবরণ খোলা |
| **Cable Tester** | কেবল ঠিক আছে কি না — ৮টি তার পরপর জ্বলে কি না দেখা |

> 🔧 ল্যাব পরীক্ষায় বলতে পারে: *"কেবল কাটার পর কীভাবে যাচাই করবে?"* — উত্তর: **Cable Tester** দিয়ে — দুই প্রান্তে ১-৮ পর্যন্ত বাতি সিরিয়ালে জ্বলতে হবে।

---

# 🗄️ Part 5 — আসল Network Rack ও Patch Panel

![Network Rack with Patch Panel](images/rack-patch-panel-cabling.jpg)
*▲ বাস্তব Data Rack — Patch Panel, Switch ও সুবিন্যস্ত কেবলিং (সবগুলো লেবেল দেওয়া)*

| অংশ | কাজ |
| :--- | :--- |
| **Rack (19" Cabinet)** | Router, Switch, Server রাখার ধাতুর ফ্রেম |
| **Patch Panel** | দেয়াল/ডেস্কের সব কেবল এক জায়গায় এনে সুইচে লাগানো — ব্যবস্থাপনা সহজ |
| **Patch Cord** | Patch Panel ↔ Switch সংযোগের ছোট রঙিন কেবল |
| **Cable Management** | তারগুলো সোজা রাখার পাতা — আলগা তার থাকলে সমস্যা হয় |
| **Labels** | প্রতিটি কেবলে নম্বর/নাম — সমস্যা হলে দ্রুত খুঁজে পাওয়া যায় |

> 🏢 তোমার বিশ্ববিদ্যালয়ের Lab/Office-এ গেলে দেখবে ঠিক এই Rack — ভেতরে তোমার ল্যাবের **2960 সুইচ** সারি সারি বসানো!

---

# 🗺️ Part 6 — PT Device ↔ Real Device ম্যাপিং

| Packet Tracer-এ যা দেখো | বাস্তবে কী | তোমার ল্যাবের ফাইল |
| :--- | :--- | :--- |
| **Router 1941** | Cisco 1941 ISR Router | [lesson-01-router-cli-basics.pkt](../pkt-files/labs/lesson-01-router-cli-basics.pkt) |
| **Switch 2960** | Cisco Catalyst 2960 (24/48-port) | [lesson-02-static-routing.pkt](../pkt-files/labs/lesson-02-static-routing.pkt) |
| **PC-PT** | আসল ডেস্কটপ/ল্যাপটপ | সব ল্যাবে |
| **Server-PT** | Rack-mount Server (Dell/HP) | লেসন ০৪ ও ০৮ |
| **Printer-PT** | Network Printer | [office-shared-printer-network.pkt](../pkt-files/practice/office-shared-printer-network.pkt) |
| **Copper Straight-Through** | সাদা/নীল/সবুজ Cat5e/Cat6 কেবল | সব ল্যাবে |
| **Copper Cross-Over** | কমলা-সবুজ ভিন্ন ক্রমের কেবল | লেসন ০২ (Router↔Router) |
| **Console Cable** | Light Blue Rollover কেবল | প্রথমবার ডিভাইস কনফিগে |
| **SFP + Fiber** | সুইচের Uplink | বড় নেটওয়ার্কে |

---

# ❓ দ্রুত পরীক্ষা (মনে রাখা যাচাই)

1. Router-এর **Console Port** কেন ব্যবহার হয়?
2. **Straight-Through vs Cross-Over** — কোনটা কখন?
3. Switch-এর **কমলা LED** মানে কী?
4. **SFP Module** কোথায় বসে এবং কেন?
5. **Patch Panel** ছাড়া নেটওয়ার্কে কী সমস্যা হয়?

<details>
<summary>💡 উত্তর দেখো</summary>

1. Router প্রথমবার কনফিগ করতে (IP না থাকায় Telnet/SSH কাজ করে না) — Console কেবল দিয়ে সরাসরি ল্যাপটপ থেকে CLI খোলা হয়।
2. Straight-Through = ভিন্ন ধরনের ডিভাইস (PC↔Switch, Switch↔Router); Cross-Over = একই ধরনের (Switch↔Switch, PC↔PC, Router↔Router)।
3. Amber (কমলা) = পোর্ট STP Listening/Learning অবস্থায় আছে — কিছুক্ষণ পর সবুজ হবে।
4. Switch-এর **Uplink SFP স্লট**ে বসে; Fiber লাগিয়ে লম্বা দূরত্ব/উচ্চ গতির সংযোগ করা হয়।
5. সব কেবল এলোমেলো গুঁড়িয়ে যায়, সমস্যা খুঁজে পাওয়া কঠিন হয়, পোর্ট পরিবর্তনে সময় বেশি লাগে।

</details>

---

# ✅ Final Checklist

| বিষয় | মনে আছে? |
| :--- | :--- |
| Router-এ Console, GE, WIC পোর্ট চেনা | ☐ |
| Switch-এ ২৪/৪৮ পোর্ট + SFP Uplink + LED চেনা | ☐ |
| Straight-Through / Cross-Over / Console কেবল আলাদা করা | ☐ |
| T568A/B রঙের ক্রম (কমপক্ষে T568B) মনে রাখা | ☐ |
| SFP, Fiber, Crimping Tool, Patch Panel চেনা | ☐ |

---

# 🔮 পরের ধাপ

এবার তুমি বাস্তব সরঞ্জামও চেনো! এবার সময় **নিজে হাতে-কলমে অনুশীলনের** — সমাধানসহ Practice Lab → [লেসন ১০ · Practice Lab (সমাধানসহ)](10-practice-lab.md)

---

> **নেভিগেশন:** [⬅ লেসন ০৮](08-final-project.md) · [🏠 হোম](../README.md) · [পরের লেসন ১০ ➡](10-practice-lab.md)

**এই লেসনের Tags:** `#hardware` `#router-ports` `#switch-ports` `#t568b` `#console` `#sfp` `#patch-panel`

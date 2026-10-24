<div align="center">

# 🌐 Cisco Packet Tracer Lab

### 🇧🇩 বাংলায় ধাপে-ধাপে নেটওয়ার্কিং ল্যাব কোর্স

*হাতে-কলমে Packet Tracer-এ নেটওয়ার্ক তৈরি করতে করতে শেখো — CLI থেকে শুরু করে সম্পূর্ণ অফিস নেটওয়ার্ক পর্যন্ত!*

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Language](https://img.shields.io/badge/Language-Bangla-006A4E?style=for-the-badge)
![Lessons](https://img.shields.io/badge/Lessons-12%20%2B%20Cheat--Sheet-FF6F00?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-2E8B57?style=for-the-badge)
![CCNA Fundamentals](https://img.shields.io/badge/CCNA%20Fundamentals-9%20Lessons-9B59B6?style=for-the-badge)

[📚 লেসন](#lessons) · [🎓 CCNA ফাউন্ডেশন](ccna-fundamentals/README.md) · [🔗 pkt কানেকশন](#pkt) · [🗺️ শেখার পথ](#path) · [🗂️ স্ট্রাকচার](#structure) · [🚀 ব্যবহার](#usage) · [📖 Cheat-Sheet](reference/cli-command-cheatsheet.md) · [📁 Rename Map](RENAME-MAP.md)

</div>

---

## 📖 এই রিপোজিটরি সম্পর্কে

এটি **EBAUB — Computer Networking Lab** এর প্র্যাকটিক্যাল কোর্স। প্রতিটি লেসনে থাকবে:

> 🧠 **ধারণা (Concept)** → 🧩 **ধাপে-ধাপে ল্যাব** → 🔍 **ভেরিফিকেশন** → 🔁 **প্যাকেট ফ্লো লজিক** → ❌ **ট্রাবলশুটিং** → ✅ **চেকলিস্ট**

প্রতিটি লেসনের শুরুতে ও শেষে **⬅ আগের / পরের ➡** নেভিগেশন আছে — সিরিয়াল ধরে পড়তে পারবে। পাশে পাশে `.pkt` ল্যাব ফাইলগুলো Packet Tracer-এ খুলে সরাসরি হাতে-কলমে অনুশীলন করো।

---

<a id="tracks"></a>

## 🚪 দুইটা কোর্স — কোনটা আগে?

একই রেপোতে দুটো আলাদা ট্র্যাক — একই ভাষা, একই স্টাইল, শুধু শুরুর জায়গা আলাদা।

| | 🅰️ [হাতে-কলমে কোর্স](lessons/01-router-cli-basics.md) | 🅱️ [CCNA Fundamentals](ccna-fundamentals/README.md) |
| :--- | :--- | :--- |
| **শুরু** | Router-এর CLI দিয়ে | "নেটওয়ার্ক আসলে কী?" দিয়ে |
| **ধরন** | config-first — সোজা ল্যাব | theory-first — আগে ধারণা, তারপর ল্যাব |
| **লেসন** | ১২টা (০১–১২) | ৯টা (০১–০৯) |
| **ভালো লাগবে যদি** | "আজই PT-তে নেটওয়ার্ক বানাব" | "আগে বুঝব, তারপর বানাব" |
| **শেষ** | Final Project + Problem Solve | 🏆 University Capstone |

> 🧭 **সেরা পথ:** CCNA Fundamentals-এর **০১–০৪** → হাতে-কলমে **০১–০২** → আবার **০৫–০৬** → হাতে-কলমে **০৩–০৮** → শেষে **০৭–০৯**।
> সময় কম? অন্তত **CCNA ০১–০৫** পড়ো — subnetting না জানলে বাকি কোর্সটা শুধু কমান্ড মুখস্থ হয়ে যায়।

---

<a id="lessons"></a>

## 📚 লেসন সমূহ — ক্লিক করলেই লেসনে যাবে!

<table>
<tr>
<th>#</th>
<th>লেসন</th>
<th>বিস্তারিত বিবরণ</th>
<th>লেভেল</th>
<th>ট্যাগ</th>
</tr>

<tr>
<td><b>০১</b></td>
<td><a href="lessons/01-router-cli-basics.md"><b>🖥️ Router CLI Basics ও প্রথম ল্যাব</b></a></td>
<td>CLI Mode (User/Privileged/Global/Interface), Basic Commands, Configuration Formula — এবং ১ Router + ১ Switch + ২ PC দিয়ে প্রথম Ping Lab। লেসন শেষে PC0 → PC1 সফল হবে!</td>
<td>🟢 Beginner</td>
<td><code>cli</code> <code>router</code> <code>ping</code> <code>first-lab</code></td>
</tr>

<tr>
<td><b>০২</b></td>
<td><a href="lessons/02-static-routing.md"><b>🛣️ Two Routers + Static Routing</b></a></td>
<td>দুটি Router ও দুটি আলাদা LAN (<code>192.168.1.0/24</code>, <code>192.168.2.0/24</code>) এর মাঝে <code>ip route</code> দিয়ে Static Routing। <code>/30</code> WAN Link, Routing Table (<code>show ip route</code>), দ্বিমুখী রুটের লজিক ও End-to-End Ping।</td>
<td>🟢 Beginner</td>
<td><code>static-routing</code> <code>ip-route</code> <code>next-hop</code> <code>wan</code></td>
</tr>

<tr>
<td><b>০৩</b></td>
<td><a href="lessons/03-dhcp.md"><b>🎫 Router DHCP Configuration</b></a></td>
<td>DHCP-এর DORA প্রক্রিয়া, <code>ip dhcp pool</code> তৈরি, <code>excluded-address</code> দিয়ে Static IP সুরক্ষা, PC-তে স্বয়ংক্রিয় IP বরাদ্দ ও <code>show ip dhcp binding</code> লিজ টেবিল যাচাই।</td>
<td>🟢 Beginner</td>
<td><code>dhcp</code> <code>pool</code> <code>auto-ip</code> <code>dora</code></td>
</tr>

<tr>
<td><b>০৪</b></td>
<td><a href="lessons/04-dns-http-server.md"><b>🌍 DNS Server ও HTTP Web Server</b></a></td>
<td>Server-এ Static IP, DNS Service-এ A Record (<code>www.office.local</code>), HTTP দিয়ে ওয়েবসাইট হোস্ট — তারপর PC থেকে ডোমেন নাম দিয়ে সাইট খোলা। DHCP + DNS + HTTP তিনটি সার্ভিস একসাথে!</td>
<td>🟡 Beginner–Intermediate</td>
<td><code>dns</code> <code>http</code> <code>web-server</code> <code>domain</code></td>
</tr>

<tr>
<td><b>০৫</b></td>
<td><a href="lessons/05-vlan.md"><b>🔀 VLAN Configuration ও Isolation</b></a></td>
<td>একটি সুইচকে ভাগ করে VLAN 10 (CSE) ও VLAN 20 (EEE) বানানো, <code>switchport access vlan</code> দিয়ে Port Assign — এবং প্রমাণ: একই VLAN-এ Ping ✅, ভিন্ন VLAN-এ Ping ❌ (Isolation)।</td>
<td>🟡 Intermediate</td>
<td><code>vlan</code> <code>switch</code> <code>isolation</code> <code>access-port</code></td>
</tr>

<tr>
<td><b>০৬</b></td>
<td><a href="lessons/06-trunk-inter-vlan.md"><b>🔗 Trunk Link ও Inter-VLAN Routing</b></a></td>
<td>802.1Q Trunk দিয়ে দুই সুইচে একাধিক VLAN বহন, তারপর Router-on-a-Stick (Subinterface + <code>encapsulation dot1Q</code>) — ভিন্ন VLAN-এর PC-দের মধ্যে সফল Ping (TTL=127)।</td>
<td>🟡 Intermediate</td>
<td><code>trunk</code> <code>802.1q</code> <code>inter-vlan</code> <code>router-on-a-stick</code></td>
</tr>

<tr>
<td><b>০৭</b></td>
<td><a href="lessons/07-switching.md"><b>⚡ Switching: STP · Port Security · EtherChannel</b></a></td>
<td>সুইচের ৩টি শক্তিশালী প্রযুক্তি — STP দিয়ে লুপ প্রতিরোধ (Root Bridge), Port Security দিয়ে নিরাপদ Access Port (sticky MAC, violation) এবং LACP EtherChannel দিয়ে ব্যান্ডউইথ ও Redundancy।</td>
<td>🟠 Intermediate–Advanced</td>
<td><code>stp</code> <code>port-security</code> <code>etherchannel</code> <code>lacp</code></td>
</tr>

<tr>
<td><b>০৮</b></td>
<td><a href="lessons/08-final-project.md"><b>🎓 Final Project — সম্পূর্ণ অফিস নেটওয়ার্ক</b></a></td>
<td>Capstone: VLAN + Inter-VLAN Routing + প্রতি VLAN-এ DHCP Pool + DNS (<code>www.office.local</code>) + HTTP — সব একসাথে। ভিন্ন VLAN-এর ইউজার একই ওয়েবসাইট খুলতে পারবে! 🎉</td>
<td>🔴 Advanced</td>
<td><code>final-project</code> <code>capstone</code> <code>all-in-one</code></td>
</tr>

<tr>
<td><b>০৯</b></td>
<td><a href="lessons/09-real-hardware.md"><b>📷 Real Network Hardware</b></a></td>
<td>Packet Tracer-এর প্রতিটি ডিভাইস বাস্তবে কেমন — আসল Router (1941/4331), Switch (2960/2950) ও <b>Hub</b>-এর পোর্ট, প্রতিটি কেবল (Straight/Cross/Console/Fiber/Coaxial) <b>পেয়ারের পার্থক্যসহ</b>, RJ-45, SFP, Crimping Tool ও Rack — সব সত্যিকারের ছবিসহ। ল্যাব পরীক্ষার আগে চোখে দেখে ফেলো!</td>
<td>🟢 সবার জন্য</td>
<td><code>hardware</code> <code>real-device</code> <code>cable</code> <code>pairs</code> <code>hub</code> <code>sfp</code></td>
</tr>

<tr>
<td><b>১০</b></td>
<td><a href="lessons/10-practice-lab.md"><b>🧪 Practice Lab (সমাধানসহ)</b></a></td>
<td>১০টি ল্যাব টাস্ক — <b>৬টি Simple + ৪টি Small Hard</b>। প্রতিটি টাস্কে সম্পূর্ণ সমাধান লুকানো অবস্থায় (ক্লিক করলে খুলবে) — যাতে আগে নিজে চেষ্টা করো, আটকে গেলে সমাধান দেখে শেখো। Score Card সহ!</td>
<td>🟢→🟠</td>
<td><code>practice</code> <code>solution</code> <code>self-study</code></td>
</tr>

<tr>
<td><b>১১</b></td>
<td><a href="lessons/11-practice-list.md"><b>📝 Practice List (সমাধান ছাড়া)</b></a></td>
<td>২০টি Self-Practice টাস্ক (Basic → Exam Simulation) — এখানে কোনো সমাধান নেই ও থাকবে না। সম্পূর্ণ নিজে ভেবে করবে — এটাই আসল পরীক্ষা। Progress Tracker সহ।</td>
<td>🟢→🔴</td>
<td><code>homework</code> <code>exam-prep</code> <code>no-solution</code></td>
</tr>

<tr>
<td><b>১২</b></td>
<td><a href="lessons/12-problem-solve.md"><b>🛠️ Problem Solve — সমস্যা ও সমাধান</b></a></td>
<td>যেকোনো নতুন সমস্যা ও তার <b>ধাপে ধাপে সমাধান</b> — সব এখানেই জমা হবে (Problem Bank)। প্রথম সমস্যা: VLAN 20 থেকে অতিরিক্ত পোর্ট সরানো। ❌ সমস্যা → 🎯 চাইছি → ✅ সমাধান → 🔍 যাচাই → 🧠 লজিক — প্রতিটি সমস্যা একই গঠনে।</td>
<td>🟢→🔴</td>
<td><code>problem-solve</code> <code>troubleshooting</code> <code>bank</code></td>
</tr>

<tr>
<td><b>📖</b></td>
<td><a href="reference/cli-command-cheatsheet.md"><b>CLI Command Cheat-Sheet</b></a></td>
<td>সব লেসনের কমান্ড এক জায়গায়: CLI <b>Shortcut (Abbreviation)</b>, Router, Switch, Subnetting, DHCP, Routing (Static/RIP/OSPF), VLAN/Trunk, Security (Password/SSH), STP, EtherChannel, CDP ও Troubleshooting Formula। পরীক্ষার আগে ঘাটতে হবে এমন রেফারেন্স!</td>
<td>⭐ সব লেভেল</td>
<td><code>cheatsheet</code> <code>reference</code> <code>ccna</code></td>
</tr>
</table>

> 💡 **টিপ:** উপরের লেসনের **নামে ক্লিক করলেই** সেই লেসনের `.md` পেজে চলে যাবে। প্রতিটি লেসনের ভেতরেও **⬅ আগের লেসন · 🏠 হোম · পরের লেসন ➡** লিংক আছে।

---

<a id="pkt"></a>

## 🔗 লেসন ↔ pkt ফাইল কানেকশন

প্রতিটি লেসনের সাথে **একটি নির্দিষ্ট `.pkt` ফাইল** যুক্ত — নাম ঠিক লেসন ফাইলের মতোই:

```text
lessons/05-vlan.md   ←→   pkt-files/labs/lesson-05-vlan.pkt
```

### 📋 লেসন ভিত্তিক pkt ফাইল (✅ = ফাইল আছে · ✍️ = এখনো বাকি)

| লেসন | pkt ফাইলের নাম | অবস্থা | নোট |
| :--- | :--- | :---: | :--- |
| [০১](lessons/01-router-cli-basics.md) | `lesson-01-router-cli-basics.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০২](lessons/02-static-routing.md) | `lesson-02-static-routing.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৩](lessons/03-dhcp.md) | `lesson-03-dhcp.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৪](lessons/04-dns-http-server.md) | `lesson-04-dns-http-server.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৫](lessons/05-vlan.md) | `lesson-05-vlan.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৬](lessons/06-trunk-inter-vlan.md) | `lesson-06-trunk-inter-vlan.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৭](lessons/07-switching.md) | `lesson-07-switching.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৮](lessons/08-final-project.md) | `lesson-08-final-project.pkt` | ✅ আছে | রিপোতে যুক্ত |
| [০৯](lessons/09-real-hardware.md) | — | — | লাগবে না (ছবির লেসন) |
| [১০](lessons/10-practice-lab.md) | `practice-lab.pkt` | ⭐ ঐচ্ছিক | নিজের অনুশীলনের ফাইল |
| [১১](lessons/11-practice-list.md) | `practice-list.pkt` | ⭐ ঐচ্ছিক | নিজের অনুশীলনের ফাইল |
| [১২](lessons/12-problem-solve.md) | `lesson-12-problem-solve.pkt` | ✍️ নেই | পরে যোগ হবে — problem-র ভাঙা scenario ধরে |

> 📌 **নতুন/আপডেট করা pkt যোগ করতে চাইলে:** ফাইলটা Packet Tracer-এ সেভ করে নামটা উপরের টেবিল অনুযায়ী হুবহু রেখে `pkt-files/labs/` ফোল্ডারে দিন — লেসনের সাথে অটো কানেক্ট হয়ে যায়।

### 📁 এক্সট্রা প্র্যাকটিস ফাইল (লেসনের সাথে যুক্ত নয়)

আপনার বানানো প্র্যাকটিস ফাইলগুলো এখানে রাখা — এগুলো কোনো লেসনের অংশ নয়, নিজের অনুশীলনের জন্য:

* `pkt-files/practice/` — office-shared-printer-network.pkt, ip-subnet-tester.pkt
* `pkt-files/topologies/` — bus, star, ring, mesh, tree, hybrid

---

<a id="path"></a>

## 🗺️ শেখার পথ (Learning Path)

```text
  🟢 Beginner                🟡 Intermediate              🟠 Advanced            🔴 Practice & Exam
┌────────────────┐   ┌────────────────────────┐   ┌──────────────────────┐   ┌─────────────────────┐
│ 01 CLI Basics  │ → │ 04 DNS + Web Server    │ → │ 07 STP / Security /  │ → │ 09 Real Hardware 📷 │
│ 02 Static Route│ → │ 05 VLAN                │ → │    EtherChannel      │ → │ 10 Practice Lab 🧪  │
│ 03 DHCP        │ → │ 06 Trunk + Inter-VLAN  │ → │ 08 Final Project 🎓  │ → │ 11 Practice List 📝 │
│                │   │                        │   │                      │   │ 12 Problem Solve 🔧 │
└────────────────┘   └────────────────────────┘   └──────────────────────┘   └─────────────────────┘
        │                       │                            │                          │
        └─────────── প্রতিটি ধাপে .pkt ফাইল দিয়ে হাতে-কলমে অনুশীলন ──────────────────────┘
```

> **Practice এর ধরন:** [লেসন ১০](lessons/10-practice-lab.md)-এ সমাধান আছে (আটকে গেলে দেখবে) — [লেসন ১১](lessons/11-practice-list.md)-এ কোনো সমাধান নেই (নিজে পারতে হবে)। দুটোই দরকারি! আর যেকোনো নতুন সমস্যা/কেস এলে সেটা [লেসন ১২ · Problem Solve](lessons/12-problem-solve.md)-এ জমা হবে, সমাধানসহ।

**পরামর্শ:** লেসন বাদ না দিয়ে **০১ → ০৮ সিরিয়াল ধরে** যাও — প্রতিটি লেসন পরের লেসনের ভিত্তি। প্রতিটি লেসনের শেষের **✅ Checklist** ও **🎯 Challenge** সম্পন্ন করেই পরের ধাপে যাওয়া উচিত।

---

<a id="structure"></a>

## 🗂️ ফাইল স্ট্রাকচার

```text
Cisco-Packet-Tracer-Lab/
├── 📄 README.md                        ← তুমি এখন এখানে!
├── 📄 RENAME-MAP.md                    ← পুরনো → নতুন ফাইল নামের ম্যাপ
│
├── 📁 lessons/                         ← 📚 ১২টি সিরিয়াল লেসন
│   ├── 01-router-cli-basics.md
│   ├── 02-static-routing.md
│   ├── 03-dhcp.md
│   ├── 04-dns-http-server.md
│   ├── 05-vlan.md
│   ├── 06-trunk-inter-vlan.md
│   ├── 07-switching.md
│   ├── 08-final-project.md
│   ├── 09-real-hardware.md            ← 📷 আসল ডিভাইস/কেবলের ছবি
│   ├── 10-practice-lab.md             ← 🧪 সমাধানসহ প্র্যাকটিস
│   ├── 11-practice-list.md            ← 📝 সমাধান ছাড়া চ্যালেঞ্জ
│   ├── 12-problem-solve.md            ← 🛠️ সমস্যা ও সমাধান (বাড়তে থাকবে)
│   └── 📁 images/                     ← লেসন ০৬–০৯-এর ছবি ও GIF
│
├── 📁 Extras/                          ← 📤 বাড়তি ল্যাব (পাঠ্যক্রমের বাইরে)
│   └── ftp-server-lab.md               ← FTP সার্ভার — আপলোড/ডাউনলোড
│
├── 📁 reference/
│   └── cli-command-cheatsheet.md       ← 📖 সব কমান্ডের রেফারেন্স
│
├── 📁 ccna-fundamentals/               ← 🎓 তত্ত্ব-আগে কোর্স (০১–০৯)
│   ├── README.md                       ← কোর্স সূচি + স্টাডি প্ল্যান
│   ├── 01-network-basics.md
│   ├── 02-osi-tcp-ip.md
│   ├── 03-mac-ethernet-arp.md
│   ├── 04-ipv4-addressing.md
│   ├── 05-subnetting-basics.md
│   ├── 06-subnetting-vlsm.md
│   ├── 07-acl-nat.md
│   ├── 08-troubleshooting.md
│   └── 09-capstone-university-lab.md   ← 🏆 সব একসাথে
│
└── 📁 pkt-files/                       ← 🧰 Cisco Packet Tracer ফাইল
    ├── 📁 labs/                        ← 🔗 লেসন-সংযুক্ত (lesson-NN-*.pkt)
    ├── 📁 practice/                    ← আপনার এক্সট্রা প্র্যাকটিস (লেসনের অংশ নয়)
    └── 📁 topologies/                  ← bus / star / ring / mesh / tree / hybrid
```

---

<a id="ideas"></a>

## 💡 ভবিষ্যতের আইডিয়া (রোডম্যাপ)

রিপোজিটরিটাকে আরও শক্তিশালী করতে যে আইডিয়াগুলো পরে যোগ করা যেতে পারে:

| # | আইডিয়া | কেন দরকার |
| :---: | :--- | :--- |
| 1 | **🏷️ প্রতি লেসনে Glossary Box** — নতুন শব্দের ছোট অভিধান | শব্দ মনে রাখা সহজ হয় |
| 2 | **🎥 Video/Animated GIF** — প্রতিটি ল্যাবের ৩০ সেকেন্ডের স্ক্রিনরেকর্ডিং লিংক | দেখে করতে সবচেয়ে সহজ (শুরু: লেসন ০৬-এ ২টা GIF) |
| 3 | **🧩 Subnetting Drill Lesson** — শুধু Subnet গণনার ২০টি দ্রুত সমস্যা | পরীক্ষায় সবচেয়ে বেশি কাজে লাগে |
| 4 | **❓ Quiz Lesson** — প্রতি লেসনের পর ৫টি MCQ (সমাধানসহ) | নিজেকে যাচাই করা যায় |
| 5 | **🔧 Troubleshooting Lab** — ইচ্ছাকৃতভাবে ভুল করা pkt (broken-lab) — খুঁজে ঠিক করতে হবে | আসল দক্ষতা এখানেই (শুরু: [লেসন ১২ · Problem Solve](lessons/12-problem-solve.md)) |
| 6 | **🌐 English Version** — প্রতিটি লেসনের EN সংস্করণ (দ্বিভাষিক) | সবার জন্য উন্মুক্ত |
| 7 | **📊 Progress Badge/Checklist** — লেসন শেষ করলে টিক দেওয়ার ট্র্যাকার | মোটিভেশন থাকে |
| 8 | **🏭 Capstone 2** — ছোট অফিস (৩ VLAN + DHCP + VoIP + WiFi) প্রজেক্ট | চূড়ান্ত দক্ষতা |

---

<a id="usage"></a>

## 🚀 কীভাবে ব্যবহার করবে

1. **[Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)** ডাউনলোড ও ইনস্টল করো (NetAcad অ্যাকাউন্ট লাগবে)
2. উপরের লেসন টেবিল থেকে **লেসন ০১** খোলো — ধারণা পড়ো
3. লেসনের **🔗 pkt ফাইলটি** (থাকলে) Packet Tracer-এ খোলো — না থাকলে লেসনের Topology দেখে **নিজে তৈরি করো, এটাই বেশি শেখায়!**
4. **ধাপগুলো অনুসরণ** করো → `show` কমান্ড দিয়ে ভেরিফাই করো → Ping টেস্ট করো
5. লেসনের শেষের **✅ Checklist** সম্পন্ন করো → পরের লেসনে যাও!
6. সব লেসন শেষে [Practice Lab](lessons/10-practice-lab.md) (সমাধানসহ) → [Practice List](lessons/11-practice-list.md) (নিজে চেষ্টা) দিয়ে নিজেকে পরীক্ষা করো — আর যেকোনো নতুন সমস্যা/কেস এলে [Problem Solve](lessons/12-problem-solve.md)-এ সমাধানসহ জমা হবে।

---

<a id="contribute"></a>

## 🤝 Contribute

ভুল/টাইপো পেলে Issue তুলো বা PR পাঠাও — বিশেষ করে:
* কমান্ড/আউটপুটে কোনো ভুল থাকলে
* নতুন লেসন/ল্যাব যোগ করতে চাইলে
* `.pkt` ফাইলের কোনো সমস্যা থাকলে

---

<div align="center">

**⭐ ভালো লাগলে Star দিতে ভুলবে না!**

*Happy Networking! 🌐*

</div>

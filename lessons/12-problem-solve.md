# লেসন ১২ · Problem Solve — সমস্যা ও সমাধান

> **নেভিগেশন:** [⬅ লেসন ১১](11-practice-list.md) · [🏠 হোম](../README.md) · [📖 Cheat-Sheet](../reference/cli-command-cheatsheet.md)

| 🎯 লক্ষ্য | ⏱️ সময় | 📊 লেভেল | 🧰 pkt ফাইল |
| :--- | :--- | :--- | :--- |
| যেকোনো সমস্যা → ধাপে ধাপে সমাধান — নতুন সমস্যা এলে এই লেসনেই জমা হবে | ~১৫ মিনিট (প্রতি সমস্যা) | 🟢→🔴 (সমস্যা ধরে) | `lesson-12-problem-solve.pkt` ✍️ তুমি বানাবে (নাম এই রাখো) |

**Tags:** `#problem-solve` `#troubleshooting` `#vlan` `#switchport` `#show-vlan-brief`

---

## 📌 এই লেসনটা কী?

এখানে তত্ত্ব নেই — শুধু **সমস্যা ও তার সমাধান**। Lab করার সময় যেকোনো নতুন সমস্যা এলে সেটা এখানে **Problem ০২, ০৩, ০৪...** হিসেবে যুক্ত হবে, সমাধানসহ। তাই লেসনটা বুকমার্ক করে রাখো!

প্রতিটি সমস্যা একই গঠনে লেখা:

| ধাপ | কী থাকবে |
| :--- | :--- |
| ❌ **সমস্যা** | কী হচ্ছে / কী ভুল দেখাচ্ছে (বর্তমান অবস্থা) |
| 🎯 **চাইছি** | ঠিক কী আউটপুট/অবস্থা চাই (Expected) |
| ✅ **সমাধান** | Switch/Router CLI কমান্ড — প্রতিটি লাইনের কাজসহ |
| 🔍 **যাচাই** | `show` কমান্ডের Expected Output — প্রমাণসহ |
| 🧠 **লজিক** | কেন এটা কাজ করল — যাতে পরের বার নিজেই পারো |

> ⚠️ **নিয়ম:** সমাধান দেখার আগে একবার নিজে চেষ্টা করো। [লেসন ১০](10-practice-lab.md)-এর মতো এখানেও সমাধান আছে যাতে আটকে গেলে শেখো — কিন্তু **চেষ্টা ছাড়া দেখা** মানে শেখা না।

---

# 🛠️ Problem ০১ — VLAN 20 থেকে অতিরিক্ত পোর্ট সরানো

## ❌ সমস্যা

একটি সুইচে দুটি VLAN আছে — **VLAN 10 (CSE)** ও **VLAN 20 (EEE)**। প্রতি VLAN-এ একটা করে পোর্ট লাগবে: `Fa0/1` → VLAN 10, `Fa0/2` → VLAN 20।

কিন্তু কনফিগ করার সময় ভুল হয়েছে — `interface range` দিতে গিয়ে তিনটে পোর্টই VLAN 20-এ চলে গেছে। `show vlan brief`:

```text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -----------------------
1    default                          active    ...
10   CSE                              active    Fa0/1
20   EEE                              active    Fa0/2, Fa0/3, Fa0/4   ← ভুল!
```

> 💡 **কীভাবে হলো:** ধরো, `interface range fastEthernet 0/2 - 4` লেখা হয়েছে (লাগত শুধু `Fa0/2`) — তাই `Fa0/3` ও `Fa0/4`-ও VLAN 20-এ ঢুকে গেছে। [লেসন ০৫](05-vlan.md)-এর `interface range` কথাটা মনে করো — **রেঞ্জ টোপোলজি দেখেই লিখতে হয়।**

## 🎯 চাইছি (Expected Output)

`Fa0/3` ও `Fa0/4` কে VLAN 20 থেকে সরিয়ে **Default VLAN 1**-এ ফেরাতে চাই:

- **VLAN 10 — CSE:** `Fa0/1`
- **VLAN 20 — EEE:** `Fa0/2`
- **VLAN 1 — default:** `Fa0/3, Fa0/4`

## ✅ সমাধান (Switch CLI)

```cisco
enable
configure terminal

interface range fastEthernet 0/3 - 4
 switchport access vlan 1
 exit

end
```

**প্রতিটি লাইন কী করল:**

| কমান্ড | কাজ |
| :--- | :--- |
| `interface range fastEthernet 0/3 - 4` | সরাতে চাওয়া পোর্ট দুটো (`Fa0/3`, `Fa0/4`) একসাথে সিলেক্ট |
| `switchport access vlan 1` | দুই পোর্টকে VLAN 1 (default)-এ পাঠাল — **এই এক লাইনেই পোর্টগুলো VLAN 20 থেকে বেরিয়ে গেল** |
| `exit` | interface mode থেকে বেরিয়ে global config-এ ফেরা |
| `end` | সরাসরি privileged mode (`#`)-এ ফেরা |

Configuration Save করতে চাইলে:

```cisco
copy running-config startup-config
```

> 💡 শুধু একটা পোর্ট সরাতে হলে `range` লাগে না — `interface fastEthernet 0/3` লিখলেই চলে।

## 🔍 যাচাই

```cisco
show vlan brief
```

**Expected Output:**

```text
VLAN Name                             Status    Ports
---- -------------------------------- --------- -----------------------
1    default                          active    Fa0/3, Fa0/4, ...
10   CSE                              active    Fa0/1
20   EEE                              active    Fa0/2
```

(`default` VLAN-এ `Fa0/3, Fa0/4`-এর পাশে ব্যবহার না করা অন্য পোর্টও দেখাতে পারে — সমস্যা নেই।)

## 🧠 লজিক — কেন এটা কাজ করল?

1. **একটি Access Port একই সময়ে একটাই VLAN-এ থাকে।** তাই `switchport access vlan 1` দিলেই পোর্টগুলো আগের VLAN 20 ছেড়ে VLAN 1-এ চলে যায় — আলাদা করে "সরানো"-র কোনো কমান্ড লাগে না।
2. **VLAN 10 বা VLAN 20 মুছে যায় না** — শুধু পোর্ট Move হলো। VLAN-কে আসলে মুছতে হলে `no vlan [ID]` লাগে — এখানে সেটা লাগেনি।
3. **মনে রাখবে:** `switchport access vlan 1` = পোর্টকে Default VLAN 1-এ ফেরানো। ফাঁকা/অব্যবহৃত পোর্ট Default VLAN 1-এ পড়ে থাকলে কোনো সমস্যা হয় না ([লেসন ০৫](05-vlan.md))।

## ❌ যদি এখনো কাজ না করে

| সমস্যা | যা দেখবে |
| :--- | :--- |
| `show vlan brief`-এ পোর্ট এখনো VLAN 20-এ দেখাচ্ছে | পোর্টের ভেতরে গিয়ে আবার `switchport access vlan 1` দাও → `end` → আবার `show vlan brief` |
| কমান্ড accepted হয়নি | পোর্টে আগে `switchport mode access` দাও, তারপর `switchport access vlan 1` |
| কোন পোর্টে হাত দিচ্ছো বুঝতে পারছো না | `do show vlan brief` দিয়ে পোর্ট নাম (`Fa0/3`) মেলিয়ে দেখো — ভুল পোর্টে হাত দিলে নতুন সমস্যা বানাবে |

---

# ✅ Problem ০১ — Checklist

| Task | Expected Result |
| :--- | :--- |
| সমস্যার অবস্থা দেখা (`show vlan brief`) | `Fa0/2, Fa0/3, Fa0/4` VLAN 20-এ দেখাচ্ছে |
| `switchport access vlan 1` দিয়ে `Fa0/3, Fa0/4` ফেরানো | পোর্টগুলো VLAN 1-এ গেছে |
| আবার `show vlan brief` | VLAN 10: `Fa0/1` · VLAN 20: `Fa0/2` · default: `Fa0/3, Fa0/4` ✅ |
| বোঝা — VLAN মুছে যায়নি, শুধু পোর্ট Move হয়েছে | ✅ |

---

# 🔮 পরের ধাপ

এটাই শেষ লেসন — কিন্তু অনুশীলনের কোনো শেষ নেই! যত বেশি Lab করবে, তত বেশি সমস্যা আসবে — আর প্রতিটির সমাধান এই লেসনেই জমা হবে। হাত গরম রাখো → [Practice Lab](10-practice-lab.md) · [Practice List](11-practice-list.md)

---

> **নেভিগেশন:** [⬅ লেসন ১১](11-practice-list.md) · [🏠 হোম](../README.md) · [📖 Cheat-Sheet](../reference/cli-command-cheatsheet.md)

**এই লেসনের Tags:** `#problem-solve` `#troubleshooting` `#switchport` `#vlan` `#cli-fix`

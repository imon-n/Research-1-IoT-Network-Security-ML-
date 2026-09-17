# IoT Network Security & Machine Learning — Key Terms

## 1. Network & IoT Related

**IoT (Internet of Things)** → Internet-এর সাথে connected physical device।
যেমন: **Smart Plug, CCTV, Smart Bulb**।

**MQTT (Message Queuing Telemetry Transport)** → IoT device-গুলোর মধ্যে message আদান-প্রদানের একটি **communication protocol**।

**Broker** → MQTT-এর **মাঝখানের server**। Device সরাসরি একে অপরকে message না দিয়ে broker-এর মাধ্যমে message পাঠায় ও receive করে।

**Packet** → Network-এর মধ্যে চলাচল করা **data-এর ছোট ছোট অংশ**।

**Router** → কোন data কোন পথে যাবে সেটা ঠিক করে এবং network-এর বিভিন্ন device-কে connect করে।

**OpenWrt** → OpenWrt হলো router-এর জন্য একটি **Linux-based operating system/firmware**, normally router-এর ভিতরে একটা operating system থাকে। OpenWrt সেই router-কে অনেক বেশি control করার সুযোগ দেয়। এই research-এ router থেকে network traffic capture করার কাজে OpenWrt ব্যবহার হয়েছে।

---

## 2. Traffic Capture & ML Data

**Wireshark** → Network-এর মধ্যে কী কী packet যাচ্ছে সেটা **দেখা ও capture করার tool**।

**Tcpdump** → Network packet capture করার একটি **command-line tool**।

**PCAP (Packet Capture)** → Capture করা network traffic **file হিসেবে save করার format**।

**Feature** → Packet বা network traffic থেকে পাওয়া এমন **গুরুত্বপূর্ণ information**, যেটা ML model decision নেওয়ার জন্য ব্যবহার করে।

উদাহরণ:

* Packet length
* Time difference
* MQTT information

Paper-এ প্রথমে **43টি feature** নিয়ে পরে **10টি important feature** নির্বাচন করা হয়েছে।

**Dataset** → ML model-কে শেখানো ও পরীক্ষা করার জন্য collected data-এর **বড় collection**।

**Label** → প্রতিটি data কোন category-এর সেটা বোঝানোর **tag**।

উদাহরণ:

* `Normal`
* `Attack`
* Device identity

---

## 3. Security & Machine Learning

**ML (Machine Learning)** → Computer-কে অনেক data দেখিয়ে **pattern শেখানো**, যাতে পরে নতুন data দেখে decision নিতে পারে।

**IDS (Intrusion Detection System)** → Network traffic **monitor করে suspicious বা attack activity detect করার system**।

**DoS (Denial of Service)** → একটি service-কে এত বেশি request বা traffic দিয়ে চাপ দেওয়া যে service **স্বাভাবিকভাবে কাজ করতে পারে না**।

**DDoS (Distributed Denial of Service)** → DoS-এর মতো attack, কিন্তু **অনেক source/device একসাথে** traffic পাঠায়।

**MitM (Man-in-the-Middle)** → দুই পক্ষের communication-এর **মাঝখানে attacker ঢুকে communication observe বা modify করার চেষ্টা করে**।

**Anomaly** → স্বাভাবিক behaviour থেকে **অস্বাভাবিক behaviour**।

উদাহরণ:

> একটি device সাধারণত অল্প traffic পাঠায়, কিন্তু হঠাৎ অনেক বেশি traffic পাঠানো শুরু করল।

---

## 4. Model Training & Results

**Feature Selection** → অনেক feature-এর মধ্য থেকে ML-এর জন্য **সবচেয়ে দরকারি feature বেছে নেওয়া**।

Paper-এ:

```text
43 Features
     ↓
20 Features
     ↓
10 Features
```

এইভাবে feature selection করে পরীক্ষা করা হয়েছে।

**Training** → পুরোনো বা known data দেখিয়ে ML model-কে **শেখানো**।

**Testing** → Training-এর পরে নতুন বা unseen data দিয়ে model **কতটা সঠিকভাবে decision নিতে পারে তা পরীক্ষা করা**।

Paper-এ:

```text
80% → Training
20% → Testing
```

ব্যবহার করা হয়েছে।

**Accuracy** → মোট prediction-এর মধ্যে **কতগুলো prediction সঠিক হয়েছে** তার পরিমাণ।

**Random Forest (RF)** → অনেকগুলো **Decision Tree একসাথে কাজ করে** এবং তাদের decision combine করে final result দেয়।

Paper-এ **Random Forest 10টি selected feature নিয়ে 0.9932 accuracy** পেয়েছে।

**Isolation Forest** → কোন data **স্বাভাবিক pattern থেকে আলাদা বা অস্বাভাবিক** সেটা detect করার একটি ML method।

এই paper-এ প্রথমে device চেনার পর known device-এর behaviour suspicious কি না সেটা পরীক্ষা করতে **Isolation Forest** ব্যবহার করা হয়েছে।

---

## 5. Complete Flow

### Flow Diagram

```text
IoT Devices
     ↓
   MQTT
     ↓
   Router
     ↓
Network Traffic
     ↓
Wireshark / Tcpdump
     ↓
    PCAP
     ↓
Feature Extraction
     ↓
Feature Selection
     ↓
     ML
     ↓
Known / Unknown Device
     ↓
Isolation Forest
     ↓
Normal / Anomaly
     ↓
    Alert
```

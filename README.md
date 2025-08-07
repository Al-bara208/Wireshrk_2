تحليل ملف PCAP لاكتشاف نشاط خبيث باستخدام Wireshark
🧪 نظرة عامة
في هذا التحليل، قمت بفحص ملف حركة مرور شبكة (PCAP) مشبوه باستخدام أداة Wireshark بهدف التعرف على مؤشرات تدل على وجود نشاط خبيث داخل الشبكة. وقد استخدمت عددًا من الفلاتر والبروتوكولات لتحليل البيانات واستخلاص الأدلة الرقمية.

🔧 الأدوات المستخدمة
Wireshark

VirusTotal

🧵 خطوات التحليل
بدأت عملية التحليل باستخدام الفلتر التالي في Wireshark لعزل الحزم التي يُحتمل أن تكون خبيثة:

scss

(http.request or tls.handshake.type eq 1) and !(ssdp)
كما قمت بفحص البيانات بناءً على البروتوكولات التالية:

DNS

HTTP

DHCP

🔎 اكتشاف نطاق مشبوه
أثناء مراجعة حزم HTTP، لفت انتباهي عنوان URL غريب في أحد الطلبات. قمت بالنقر على الحزمة والاطلاع على تفاصيلها، ثم استخرجت اسم النطاق منها. وعند التحقق من هذا النطاق باستخدام موقع VirusTotal، تبين أنه مصنف على أنه نطاق خبيث (Malware) من قبل عدة محركات فحص.

🖥️ تحديد الجهاز المصاب
من خلال فحص أعمدة source IP وتفاصيل البروتوكولات، تمكنت من استخراج معلومات الجهاز المصاب:

المؤشر و القيمة
عنوان IP للجهاز المصاب	: 10.6.13.133
عنوان MAC للجهاز المصاب : 	24:77:03:ac:97:df (الجزء الظاهر: ac:97:df)
اسم المضيف : (GET)	event-time-microsoft.org
اسم المضيف : (POST)	eventdata-microsoft.live
اسم حساب المستخدم	: Microsoft-CryptoAPI

📌 أبرز النتائج
تم رصد طلبات HTTP واتصالات TLS مشبوهة.

تم التأكد من أن النطاق eventdata-microsoft.live نطاق خبيث

أمكن تحديد الجهاز المصاب من خلال عناوين IP وMAC وطلبات DNS

استخدم المهاجم أسماء نطاقات تحاكي أسماء خدمات مايكروسوفت لتضليل المحللين

📁 ملخص التحليل
يعرض هذا التحليل كيفية التعامل مع ملفات PCAP لتحديد الأجهزة المخترقة واكتشاف النشاط الخبيث داخل الشبكة باستخدام أدوات مفتوحة المصدر. يمكن أن يشكل هذا العمل نموذجًا مفيدًا لمحللي الأمن السيبراني أو الطلاب في مجال الشبكات.

📂 الحالة: مكتمل
📅 التاريخ: أغسطس 2025
✍️ الكاتب: [albara alsadiq]






PCAP Malware Traffic Analysis using Wireshark
🧪 Overview
In this analysis, I examined a suspicious network capture file (PCAP) using Wireshark to detect signs of malicious activity. I applied several protocol filters and carefully reviewed the traffic patterns to identify indicators of compromise.

🔍 Tools Used
Wireshark

VirusTotal

🧵 Analysis Process
I began the analysis by applying the following Wireshark display filter to isolate potentially malicious traffic:

scss
نسخ
تحرير
(http.request or tls.handshake.type eq 1) and !(ssdp)
I also inspected traffic using the following protocols:

DNS

HTTP

DHCP

🔎 Suspicious Domain Detection
While inspecting HTTP packets, I came across a suspicious URL that stood out due to its unusual format. Upon further inspection of the packet details, I extracted the domain name and ran a check on VirusTotal. The domain was flagged as malicious (Malware) by several engines.

🖥️ Identifying the Infected Client
By examining the packet source fields and DNS queries, I was able to gather the following information about the infected Windows client:

Indicator and	Value
IP Address :	10.6.13.133
MAC Address	: 24:77:03:ac:97:df (last part visible: ac:97:df)
Hostname : (GET packet)	event-time-microsoft.org
Hostname : (POST packet)	eventdata-microsoft.live
User Account Name	: Microsoft-CryptoAPI

📌 Key Findings
Unusual HTTP requests and TLS handshakes were observed.

The domain eventdata-microsoft.live was confirmed as malicious.

The infected machine was clearly identifiable through IP, MAC, and DNS queries.

Hostnames imitated Microsoft domains to avoid detection.

📁 File Summary
This analysis demonstrates a structured approach to identifying a compromised system using only PCAP data and open-source tools. It can serve as a blueprint for SOC analysts or students working in network security.

📂 Status: Completed
📅 Date: August 2025
✍️ Author: [albara alsadiq]





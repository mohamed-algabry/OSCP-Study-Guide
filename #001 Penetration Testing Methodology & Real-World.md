# OSCP Study Guide
#  Penetration Testing Methodology & Real-World Workflow

> **الموضوع:** Penetration Testing Methodology & Real-World Workflow  
> **المستوى:** Beginner → Intermediate  
> **التصنيف:** Offensive Security / Penetration Testing

---

# Table of Contents

1. Introduction to Penetration Testing Methodology
2. The Real Objective of a Penetration Test
3. The Penetration Tester Mindset
4. The Complete Penetration Testing Workflow
5. Phase 01 — Pre-Engagement & Planning
6. Phase 02 — Reconnaissance
7. Phase 03 — Scanning
8. Phase 04 — Enumeration
9. Phase 05 — Vulnerability Assessment
10. Phase 06 — Exploitation
11. Phase 07 — Post-Exploitation
12. Phase 08 — Privilege Escalation
13. Phase 09 — Lateral Movement
14. Phase 10 — Documentation & Evidence Collection
15. Phase 11 — Reporting & Remediation
16. Phase 12 — Retesting
17. How All Phases Work Together
18. Practical Pentesting Mindset
19. Professional Penetration Testing Checklist
20. Key Takeaways

---

# 01 — Introduction to Penetration Testing Methodology

## ما هي Penetration Testing Methodology؟

الـ Penetration Testing مش مجرد مجموعة Tools بنشغلها على Target ونستنى النتائج.

هي عملية منظمة (Structured Process) بنمشي فيها وفق مجموعة مراحل مترابطة، وكل مرحلة بتعتمد على المعلومات والنتائج اللي وصلنالها في المرحلة السابقة.

الفكرة الأساسية إننا مش بنستخدم الأدوات بشكل عشوائي، لكن بنبدأ بسؤال، ونختار الطريقة المناسبة للإجابة عليه.

مثلاً:

- هل يوجد Host متاح داخل الـ Network؟
- ما هي الـ Ports المفتوحة؟
- ما هي الخدمات (Services) التي تعمل على هذه المنافذ؟
- ما إصدار الخدمة؟
- هل توجد Configuration ضعيفة؟
- هل توجد Vulnerability قابلة للاستغلال؟
- ما التأثير الحقيقي لهذه الثغرة؟

كل إجابة بتساعدنا نحدد السؤال التالي.

## الفكرة الأساسية

تخيل إنك دخلت مبنى لأول مرة.

أنت لا تعرف:
- عدد الغرف.
- أماكن الأبواب.
- نوع الأقفال.
- الغرف المهمة.
- الأشخاص الذين يمتلكون صلاحيات الدخول.

مش منطقي تبدأ تكسر الأبواب بشكل عشوائي.

الأصح إنك تفهم المبنى الأول، وبعدها تحدد الأماكن اللي تستحق الفحص.

نفس الفكرة في الـ Penetration Testing.

## Core Principle

**Every action must have a reason.**

كل خطوة لازم يكون ليها هدف واضح، ومعلومة معينة عايز تحصل عليها، ونتيجة تساعدك في اتخاذ القرار التالي.


---

# 02 — The Real Objective of a Penetration Test

## ما الهدف الحقيقي من الـ Penetration Testing؟

الهدف مش إننا نلاقي أكبر عدد ممكن من الثغرات.

الهدف الحقيقي هو:

1. اكتشاف نقاط الضعف (Identify Vulnerabilities).
2. التأكد من وجودها فعلياً (Validate Findings).
3. إثبات إمكانية استغلالها (Demonstrate Exploitability).
4. تحديد تأثيرها على النظام أو المؤسسة (Assess Impact).
5. تقديم توصيات عملية لمعالجتها (Provide Remediation).

بمعنى إن اكتشاف Vulnerability مش معناه تلقائياً إننا نقدر نستغلها.

لازم نفهم ظروف وجودها، وهل هي قابلة للاستغلال بالفعل، وإيه النتائج اللي ممكن نوصل ليها.

## Example

افترض إننا اكتشفنا إن هناك SSH Service تعمل على Port 22.

المعلومة دي لوحدها مش Vulnerability.

لكن ممكن نكتشف لاحقاً:

- إصدار قديم من SSH.
- Weak Configuration.
- Password Authentication غير آمن.
- وجود حسابات ضعيفة الحماية.

بعد ذلك نبدأ نقيّم هل توجد مشكلة أمنية حقيقية، وما مدى تأثيرها.

## Four Fundamental Questions

| السؤال | المعنى |
|---|---|
| What is the weakness? | ما نقطة الضعف؟ |
| Can it be exploited? | هل يمكن استغلالها؟ |
| What is the impact? | ما تأثيرها؟ |
| How can it be fixed? | كيف يمكن معالجتها؟ |

## Important Note

مش كل Finding لازم تتحول إلى Exploit.

في بعض الحالات، وجود Evidence موثوق يثبت المشكلة وتأثيرها يكون كافياً، خصوصاً لو إثباتها عملياً قد يؤدي إلى تعطيل النظام أو كشف بيانات حقيقية.


---

# 03 — The Penetration Tester Mindset

## كيف يفكر الـ Penetration Tester؟

أهم حاجة لازم تتعلمها مش استخدام الأدوات، لكن طريقة التفكير.

الـ Professional Pentester مش بيبدأ بسؤال:

"What tool should I run?"

لكن بيسأل:

"What information am I missing?"

يعني إيه؟

أنت عندك معلومات محدودة عن Target، وعايز تبني صورة كاملة عنه تدريجياً.

كل معلومة جديدة بتفتح لك أسئلة جديدة.

## The Observe → Understand → Hypothesize → Test → Decide Model

### 1. Observe — الملاحظة

تبدأ بملاحظة المعلومات الموجودة أمامك.

مثال:

اكتشفت إن Port 22 مفتوح.

### 2. Understand — الفهم

تحاول تفهم المعلومة.

Port 22 غالباً مرتبط بخدمة SSH.

### 3. Hypothesize — وضع فرضية

تضع احتمالاً مبنياً على المعلومات.

مثلاً:

قد تكون الخدمة تستخدم إصداراً قديماً أو إعدادات Authentication ضعيفة.

### 4. Test — الاختبار

تختار وسيلة مناسبة للتحقق من الفرضية، ضمن الـ Scope المسموح.

### 5. Decide — اتخاذ القرار

بناءً على النتيجة، تقرر الخطوة التالية.

- لو الفرضية صحيحة: تكمل التحليل.
- لو غير صحيحة: تعدّل اتجاه البحث.
- لو المعلومات غير كافية: تجمع معلومات إضافية.

## Example

```text
Observation:
Port 22 is open.

Understanding:
SSH service may be running.

Hypothesis:
The SSH service may expose useful version information.

Test:
Perform service detection and safe enumeration.

Result:
OpenSSH version identified.

Decision:
Review version information, configuration, and relevant security issues.
```

## Golden Rule

لا تحفظ خطوات تنفيذية فقط.

افهم لماذا تنفذ كل خطوة، ومتى تحتاج إليها، وما المعلومات التي ستستفيد منها.

---

# 04 — The Complete Penetration Testing Workflow

قبل ما ندخل في تفاصيل كل مرحلة، لازم نفهم الصورة الكاملة.

الـ Penetration Testing بيتكون من مجموعة مراحل أساسية.

## Main Workflow

1. Pre-Engagement & Planning
2. Reconnaissance
3. Scanning
4. Enumeration
5. Vulnerability Assessment
6. Exploitation
7. Post-Exploitation
8. Privilege Escalation
9. Lateral Movement
10. Documentation
11. Reporting
12. Retesting

**ملاحظة:** المراحل دي مش دائماً Linear بشكل صارم. أحياناً نتيجة مرحلة ترجعك لمرحلة سابقة أو تفتح مسار اختبار جديد.

## Workflow Overview

```text
              PENETRATION TESTING
                       |
                       v
             PRE-ENGAGEMENT
                       |
                       v
                RECONNAISSANCE
                       |
                       v
                   SCANNING
                       |
                       v
                 ENUMERATION
                       |
                       v
            VULNERABILITY ASSESSMENT
                       |
                       v
                 EXPLOITATION
                       |
                       v
               POST-EXPLOITATION
                       |
                       v
              PRIVILEGE ESCALATION
                       |
                       v
                LATERAL MOVEMENT
                       |
                       v
                 DOCUMENTATION
                       |
                       v
                    REPORT
                       |
                       v
                    RETEST
```

## Understanding the Flow

- Planning: تحديد ما الذي سنختبره وما المسموح به.
- Recon: فهم Target وجمع المعلومات.
- Scanning: اكتشاف Hosts وPorts وServices.
- Enumeration: جمع تفاصيل الخدمات والموارد.
- Vulnerability Assessment: تحليل المعلومات وتحديد نقاط الضعف.
- Exploitation: التحقق من إمكانية استغلال الثغرات.
- Post-Exploitation: فهم قيمة الوصول الذي حصلنا عليه.
- Privilege Escalation: اختبار إمكانية الحصول على صلاحيات أعلى.
- Lateral Movement: اختبار إمكانية الانتقال إلى أنظمة أخرى.
- Documentation: تسجيل النتائج والأدلة.
- Reporting: تقديم النتائج والتوصيات.
- Retesting: التأكد من إصلاح المشكلات.


---

# 05 — Phase 01: Pre-Engagement & Planning

## ما هي مرحلة Pre-Engagement؟

دي أول وأهم مرحلة قبل ما نبدأ أي Testing Activity.

قبل ما تعمل Recon أو Scanning أو حتى تبعت Request واحدة للـ Target، لازم تعرف أنت مسموح لك تعمل إيه بالضبط.

مش معنى إنك تقدر توصل إلى Server إنه مسموح لك تختبره.

## 1. Define the Objective

لازم تحدد الهدف من الـ Penetration Test.

مثلاً:

- External Network Penetration Test.
- Internal Network Penetration Test.
- Web Application Penetration Test.
- API Security Assessment.
- Mobile Application Penetration Test.

كل نوع له طبيعة اختبار مختلفة.

## 2. Define the Scope

الـ Scope بيحدد الأنظمة والأصول المسموح باختبارها.

ممكن العميل يمتلك 10 Servers، لكن يسمح لك باختبار 3 فقط.

مثال:

```text
IN-SCOPE:
192.168.1.10
192.168.1.20
app.example.com

OUT-OF-SCOPE:
192.168.1.50
mail.example.com
third-party.example.net
```

لازم تلتزم بالـ Scope المحدد حتى لو اكتشفت أصولاً أخرى مرتبطة بالهدف.

## 3. Rules of Engagement (RoE)

الـ Rules of Engagement بتحدد القواعد اللي لازم تمشي عليها أثناء الاختبار.

من أمثلتها:

- هل مسموح باستخدام Automated Scanners؟
- هل مسموح باستخدام Exploitation؟
- هل مسموح باستخدام Password Attacks؟
- هل مسموح باختبارات DoS؟
- هل توجد أوقات محددة للاختبار؟
- هل توجد أنظمة حساسة ممنوع اختبارها؟
- هل توجد قيود على استخراج البيانات؟

## 4. Authorization

لازم يكون عندك تصريح واضح ومحدد قبل تنفيذ أي اختبار.

التصريح لازم يحدد الأنظمة والأنشطة والفترة الزمنية المسموح بها.

## 5. Communication Contacts

لازم تعرف الأشخاص المسؤولين عن التواصل في حالة حدوث مشكلة.

مثلاً:

- Technical Contact.
- Security Team.
- Emergency Contact.
- Project Manager.

## 6. Testing Constraints

حتى لو النظام داخل الـ Scope، ممكن تكون هناك أنشطة معينة ممنوعة عليه.

مثلاً:

Server موجود داخل النطاق، لكن ممنوع تنفيذ اختبارات قد تؤثر على Availability الخاصة به.

## Pre-Engagement Checklist

- [ ] Objective defined.
- [ ] Scope documented.
- [ ] Out-of-scope assets identified.
- [ ] Written authorization obtained.
- [ ] Rules of Engagement reviewed.
- [ ] Testing window confirmed.
- [ ] Restricted activities identified.
- [ ] Emergency contacts identified.

## Important Principle

**Never test what you are not authorized to test.**


---

# 06 — Phase 02: Reconnaissance

## ما هو Reconnaissance؟

Reconnaissance أو Recon هي مرحلة جمع المعلومات عن الـ Target قبل الدخول في الاختبارات التقنية المتعمقة.

الهدف إننا نبني صورة مبدئية عن البيئة المستهدفة.

بدل ما نبدأ نفحص Target بشكل عشوائي، نجمع معلومات تساعدنا نفهم:

- ما هي الـ Domains؟
- ما هي الـ Subdomains؟
- ما هي Public IP Addresses؟
- ما هي التقنيات المستخدمة؟
- هل توجد Mail Servers؟
- هل توجد VPN Services؟
- ما هي البنية التحتية الظاهرة للعامة؟

## Types of Reconnaissance

### 1. Passive Reconnaissance

في الـ Passive Recon بنجمع معلومات من مصادر عامة دون إجراء تفاعل تقني مباشر مع أنظمة الـ Target.

مصادر المعلومات ممكن تشمل:

- Search Engines.
- Public DNS Records.
- Certificate Transparency Logs.
- Public WHOIS Information.
- Public Code Repositories.
- Publicly Available Documents.
- Technology Fingerprinting Services.

### Example

لو عندك:

```text
example.com
```

ممكن تبدأ بجمع معلومات عامة عن:

```text
example.com
www.example.com
mail.example.com
dev.example.com
api.example.com
```

مع التأكد من إن أي معلومات أو أصول يتم التعامل معها تظل ضمن النطاق المصرح به.

### 2. Active Reconnaissance

في الـ Active Recon بنبدأ نتفاعل مباشرة مع الأنظمة الموجودة داخل الـ Scope.

ممكن يكون الهدف:

- التأكد من وجود Host.
- فحص DNS.
- إرسال Network Requests.
- جمع معلومات تقنية مباشرة.
- اختبار استجابة الخدمات.

الـ Active Recon بيقدم معلومات تقنية مباشرة، لكنه قد يترك آثاراً في سجلات الأنظمة.

## Reconnaissance vs Scanning

الفرق المهم:

Recon أوسع من مجرد فحص المنافذ.

Recon هدفه بناء صورة عامة عن الـ Target.

أما Scanning فهو أكثر تركيزاً على اكتشاف الأنظمة والخدمات المتاحة.

## Building a Target Profile

في نهاية المرحلة دي المفروض يكون عندك تصور مبدئي عن:

```text
Target: example.com

Domains:
- example.com
- dev.example.com
- api.example.com

Technologies:
- Web Server
- DNS
- Mail Infrastructure

Potential Assets:
- Web Applications
- API Endpoints
- Public Servers
```

المعلومات دي بتساعدك تحدد أين تركز جهودك في المرحلة التالية.

---

# 07 — Phase 03: Scanning

## ما هي مرحلة Scanning؟

بعد ما جمعنا المعلومات العامة عن Target، نبدأ نحول المعلومات دي إلى تفاصيل تقنية أكثر وضوحاً.

Scanning بيساعدنا نجاوب على مجموعة أسئلة:

- ما هي الأجهزة المتاحة؟
- ما هي الـ Hosts التي تستجيب؟
- ما هي الـ Ports المفتوحة؟
- ما هي الخدمات التي تعمل خلف هذه المنافذ؟

## 1. Host Discovery

الهدف هو تحديد الأجهزة المتاحة داخل النطاق.

مثلاً:

```text
192.168.1.10  → Host Responding
192.168.1.20  → Host Responding
192.168.1.30  → No Response
```

عدم وجود Response لا يعني بالضرورة أن الجهاز غير موجود، فقد تكون هناك Firewall Rules أو إعدادات تمنع الرد.

## 2. Port Scanning

بعد تحديد الأجهزة، نبدأ في معرفة المنافذ المفتوحة.

مثال:

```text
PORT     STATE     SERVICE

22/tcp   open      ssh
80/tcp   open      http
443/tcp  open      https
3306/tcp open      mysql
```

## 3. Service Detection

بعد اكتشاف Port مفتوح، نحتاج نعرف ما الخدمة التي تعمل عليه.

مثلاً:

```text
22/tcp → SSH
80/tcp → HTTP
443/tcp → HTTPS
3306/tcp → MySQL
```

## 4. Understanding Scan Results

وجود Port مفتوح لا يعني وجود Vulnerability.

مثلاً:

```text
22/tcp open ssh
```

المعلومة دي بتقول إن هناك خدمة تستقبل اتصالات على Port 22، لكنها لا تخبرنا وحدها:

- ما إصدار الخدمة؟
- ما نوع Authentication؟
- هل توجد إعدادات ضعيفة؟
- هل هناك مستخدمون أو موارد يمكن اكتشافها؟

دي أسئلة هنحتاج نجاوب عليها في Enumeration.

## Scanning vs Reconnaissance

| Reconnaissance | Scanning |
|---|---|
| بناء صورة عامة عن Target | اكتشاف التفاصيل التقنية |
| Domains & Subdomains | Hosts & Ports |
| Public Information | Technical Responses |
| Target Profile | Service Discovery |

## Example Output

```text
TARGET: 192.168.1.10

HOST:
Status: Up

OPEN PORTS:
22/tcp
80/tcp
443/tcp

DETECTED SERVICES:
SSH
HTTP
HTTPS
```

---

# 08 — Phase 04: Enumeration

## ما هي Enumeration؟

Enumeration هي مرحلة جمع معلومات تفصيلية عن الخدمات والأنظمة التي اكتشفناها أثناء Scanning.

هنا بننتقل من مجرد معرفة إن هناك Service شغالة إلى فهم تفاصيلها.

مثلاً:

في Scanning اكتشفنا:

```text
22/tcp open ssh
```

لكن المعلومات دي محدودة.

في Enumeration نبدأ نسأل:

- ما إصدار SSH؟
- ما نوع Authentication؟
- هل توجد معلومات عن Configuration؟
- هل هناك معلومات متاحة عن المستخدمين؟
- هل توجد خصائص أو موارد إضافية يمكن اكتشافها؟

## Enumeration Depends on the Service

كل Service لها طريقة مختلفة في Enumeration.

### SSH Enumeration

ممكن نبحث عن:

- SSH Version.
- Supported Authentication Methods.
- Host Key Information.
- Supported Algorithms.
- Security Configuration.

### HTTP/HTTPS Enumeration

ممكن نبحث عن:

- Web Server Technology.
- HTTP Headers.
- Server Information.
- Available Directories.
- Virtual Hosts.
- Application Framework.
- Publicly Accessible Resources.

### FTP Enumeration

ممكن نبحث عن:

- FTP Server Version.
- Anonymous Access Configuration.
- Available Directories.
- Supported FTP Features.
- Authentication Behavior.

### DNS Enumeration

ممكن نبحث عن:

- DNS Records.
- Nameservers.
- Mail Exchange Records.
- Subdomains.
- Zone Transfer Configuration.

### SMB Enumeration

ممكن نبحث عن:

- SMB Version.
- Available Shares.
- Share Permissions.
- Domain Information.
- Server Information.
- Authentication Requirements.

## Recon vs Scanning vs Enumeration

| Stage | Main Question | Example |
|---|---|---|
| Recon | What do we know about the target? | Domains |
| Scanning | What is available? | Port 22 |
| Enumeration | What can we learn about it? | SSH Version & Configuration |

## Example

```text
Stage 1 — Scanning:

22/tcp open ssh

Stage 2 — Enumeration:

Service: OpenSSH
Version: Identified
Authentication: Supported methods identified
Configuration: Additional details collected

Stage 3 — Next Decision:

Review the service configuration and relevant security issues.
```

**الفكرة:** Enumeration بتحول النتائج الأولية إلى معلومات تقنية تساعدنا نحدد نقاط الفحص المهمة.

---

# 09 — Phase 05: Vulnerability Assessment

## ما هي Vulnerability Assessment؟

بعد Recon وScanning وEnumeration أصبح عندنا كمية معلومات أكبر عن Target.

لكن هل كل المعلومات دي معناها إن عندنا Vulnerability؟

بالطبع لا.

هنا بنبدأ نحلل المعلومات ونحدد نقاط الضعف المحتملة.

## Vulnerability Identification

نبدأ بمراجعة النتائج التي جمعناها.

أمثلة:

- Outdated Software.
- Weak Security Configuration.
- Default Credentials.
- Insecure Permissions.
- Exposed Sensitive Information.
- Authentication Weaknesses.
- Access Control Issues.
- Known Vulnerabilities.

## Understanding a Potential Finding

افترض إننا اكتشفنا:

```text
Service: Apache HTTP Server
Version: X.Y.Z
```

الخطوة التالية مش إننا نفترض وجود ثغرة مباشرة.

لكن نبدأ نبحث:

1. هل الإصدار مرتبط بثغرات معروفة؟
2. هل الظروف المطلوبة للاستغلال متوفرة؟
3. هل المشكلة تنطبق على البيئة الفعلية؟
4. هل توجد Mitigations؟
5. هل يمكن التحقق من المشكلة بأمان؟

## False Positives

أحياناً الأدوات بتطلع نتائج غير دقيقة.

وده ممكن يحصل بسبب:

- Version Detection غير دقيق.
- Configuration مختلفة عن الافتراضات.
- وجود Security Patches.
- اختلاف بيئة التشغيل.
- وجود Mitigations.

عشان كده لازم نتحقق من كل Finding.

## Risk Assessment

بعد تحديد المشكلة، نحتاج نفهم مستوى خطورتها.

ممكن نستخدم:

- CVSS.
- Business Impact.
- Exploitability.
- Confidentiality Impact.
- Integrity Impact.
- Availability Impact.

## Example

```text
Finding:
Potentially outdated web component.

Validation:
Review the actual version and patch status.

Impact:
Determine whether sensitive information or
system functionality is exposed.

Priority:
Assess severity and business context.
```

## Important Distinction

مش كل Finding محتاجة Exploitation.

ممكن يكون عندك Evidence كافي لإثبات المشكلة وتقييم تأثيرها دون تنفيذ Exploit.


---

# 10 — Phase 06: Exploitation

## ما هي Exploitation؟

Exploitation هي المرحلة التي نحاول فيها إثبات إن Vulnerability معينة قابلة للاستغلال فعلياً، وإنها ممكن تؤدي إلى التأثير المتوقع.

لكن لازم نفهم إن Exploitation مش معناها تنفيذ أي Exploit وخلاص.

كل خطوة لازم يكون ليها سبب واضح.

## Before Exploitation

قبل ما تبدأ، اسأل نفسك:

1. ما المشكلة التي أحاول إثباتها؟
2. هل تم التأكد من وجودها؟
3. ما التأثير المتوقع؟
4. هل النشاط مسموح به؟
5. هل الطريقة المستخدمة قد تسبب تعطيل النظام؟
6. ما أقل إجراء يمكنه إثبات التأثير؟

## Controlled Exploitation

لازم تختار الطريقة الأقل تأثيراً على النظام.

مثلاً:

لو عندك ثغرة تسمح بالوصول إلى ملف حساس، مش مطلوب منك استخراج كل الملفات الموجودة على السيرفر.

ممكن تثبت التأثير باستخدام ملف اختبار غير حساس أو دليل محدود ومعتمد.

## Exploitation Objectives

الهدف ممكن يكون:

- إثبات Authentication Bypass.
- إثبات Unauthorized Access.
- إثبات Remote Code Execution في بيئة اختبار مناسبة.
- إثبات File Disclosure.
- إثبات SQL Injection.
- إثبات Access Control Weakness.

## Example

افترض إنك اكتشفت Broken Access Control.

التحليل أظهر إن User A ممكن يصل إلى Resource خاص بـ User B.

بعد التأكد من التصريح والبيئة المناسبة، ممكن تستخدم حسابين تجريبيين لإثبات إن الوصول غير المصرح به ممكن.

النتيجة:

```text
Finding:
Broken Access Control.

Expected Impact:
Unauthorized access to another user's resource.

Validation:
A test account accessed a resource
belonging to another test account.

Evidence:
Request and response showing unauthorized access.

Result:
Vulnerability confirmed.
```

## Proof of Concept (PoC)

الـ PoC هو دليل عملي يوضح إن المشكلة قابلة للتحقق أو الاستغلال.

لازم يكون:

- واضح.
- قابل لإعادة الاختبار.
- محدود التأثير.
- مرتبط مباشرة بالـ Finding.
- داخل نطاق التصريح.

## Important Principle

**Prove the impact, not maximize the damage.**

---

# 11 — Phase 07: Post-Exploitation

## ما هي Post-Exploitation؟

الحصول على Access مش معناه إن الاختبار انتهى.

بعد نجاح Exploitation، لازم نفهم قيمة الوصول اللي حصلنا عليه.

ممكن تكون وصلت إلى حساب عادي، أو جهاز محدود الصلاحيات، أو نظام يحتوي على موارد مهمة.

السؤال هنا:

**What can we actually do with the access we obtained?**

## 1. Understand the Current Environment

أول حاجة لازم تفهم البيئة اللي وصلت لها.

ممكن تجمع معلومات عن:

- Operating System.
- Hostname.
- Current User.
- Current Privileges.
- Running Processes.
- Network Interfaces.
- Available Resources.

## 2. Determine Access Level

لازم تعرف الصلاحيات الفعلية للحساب.

مثلاً:

```text
Current User: testuser

Operating System: Linux

Access Level: Standard User

Permissions: Limited
```

## 3. Assess the Value of Access

مش مهم بس إزاي دخلت.

المهم إيه اللي تقدر توصله بعد الدخول.

مثلاً:

- هل يمكن الوصول إلى ملفات حساسة؟
- هل توجد معلومات عن أنظمة أخرى؟
- هل هناك Resources مرتبطة بالحساب؟
- هل الحساب يمتلك صلاحيات إضافية؟
- هل توجد مسارات أخرى يمكن اختبارها؟

## 4. Decide Whether to Continue

ممكن يكون الوصول اللي حصلت عليه كافي لتحقيق الهدف.

وممكن تكتشف إن الوصول محدود وإن هناك اختباراً إضافياً ضرورياً ومسموحاً به.

مش مطلوب تكمل كل الاحتمالات لمجرد إنك قادر تعمل كده.

لازم كل خطوة يكون ليها هدف.

---

# 12 — Phase 08: Privilege Escalation

## ما هي Privilege Escalation؟

بعد الحصول على Access إلى النظام، ممكن تكتشف إن الحساب الحالي لا يمتلك صلاحيات كافية.

هنا نبدأ نقيّم هل هناك مسار يسمح بالحصول على صلاحيات أعلى.

Privilege Escalation هي عملية الانتقال من مستوى صلاحيات منخفض إلى مستوى أعلى.

## Two Main Types

### 1. Vertical Privilege Escalation

الانتقال من صلاحيات أقل إلى صلاحيات أعلى.

مثال:

```text
Standard User
      |
      v
Administrator / Root
```

في Linux ممكن يكون الهدف الوصول إلى Root.

وفي Windows ممكن يكون الهدف الوصول إلى Administrator أو SYSTEM.

### 2. Horizontal Privilege Escalation

الانتقال إلى حساب آخر بنفس مستوى الصلاحيات تقريباً، لكن الحساب الآخر يمتلك وصولاً مختلفاً إلى الموارد.

مثال:

```text
User A  ------>  User B
```

المشكلة هنا مش بالضرورة زيادة مستوى الصلاحيات، لكن تجاوز الحدود المفروض تكون موجودة بين الحسابات.

## Important Areas to Investigate

في بيئة Linux:

- File Permissions.
- SUID / SGID.
- Sudo Configuration.
- Scheduled Tasks.
- Services.
- Kernel Information.
- Credentials Exposure.
- Writable Files and Directories.

في بيئة Windows:

- User Privileges.
- Service Permissions.
- Scheduled Tasks.
- Unquoted Service Paths.
- Weak File Permissions.
- Credential Exposure.
- Misconfigured Services.
- Token Privileges.

كل نقطة لازم يتم تقييمها وفق طبيعة النظام والـ Scope والتصريح.

## Example

```text
Initial Access:
Standard Linux User.

Observation:
The user has limited permissions.

Hypothesis:
A misconfigured permission may allow
access to a privileged operation.

Validation:
Review the configuration and permitted behavior.

Result:
A privilege escalation path may be confirmed.
```

## Important Note

مش كل حساب محدود معناه إن فيه Privilege Escalation.

ممكن تبحث وماتلاقيش أي مسار منطقي.

توثيق عدم وجود مسار مؤكد ضمن حدود الاختبار يعتبر نتيجة مفيدة أيضاً.

---

# 13 — Phase 09: Lateral Movement

## ما هي Lateral Movement؟

أحياناً الجهاز اللي وصلت له مش هو الهدف النهائي.

ممكن يكون مجرد نقطة بداية داخل Network أكبر.

هنا بنبدأ نفهم العلاقات بين الأجهزة والأنظمة داخل البيئة.

Lateral Movement هو الانتقال من نظام إلى نظام آخر داخل نفس البيئة أو الشبكة باستخدام وصول أو علاقات ثقة موجودة.

## Understanding the Network

افترض إنك وصلت إلى جهاز داخل شبكة شركة.

الجهاز ده ممكن يكون مرتبطاً بـ:

- File Server.
- Database Server.
- Application Server.
- Domain Controller.
- Internal Management Systems.

مش معنى إنك وصلت إلى جهاز إنك تقدر توصل إلى باقي الأجهزة.

لازم تفهم:

- هل يوجد Network Connectivity؟
- هل توجد علاقات ثقة؟
- هل الحساب يمتلك صلاحيات على موارد أخرى؟
- هل توجد أنظمة مرتبطة بالحساب؟
- هل الانتقال مسموح ضمن الـ Scope؟

## Example

```text
Initial Access:

Workstation A
      |
      v
Limited User Access

Discovered Relationship:

Workstation A
      |
      +------ File Server
      |
      +------ Application Server
      |
      +------ Database Server
```

المخطط ده بيوضح علاقات محتملة تحتاج إلى تقييم، وليس دليلاً على إمكانية الوصول إليها.

## Lateral Movement vs Privilege Escalation

| Privilege Escalation | Lateral Movement |
|---|---|
| زيادة الصلاحيات | الانتقال بين الأنظمة |
| Standard User → Root | System A → System B |
| نفس النظام غالباً | نظام آخر أو سياق مختلف |
| Focus on Permissions | Focus on Access & Trust |

ممكن العمليتين يحصلوا مع بعض في سلسلة اختبار واحدة.

## Important Principle

مش الهدف إنك تتحرك لأكبر عدد ممكن من الأجهزة.

الهدف إنك تثبت التأثير الحقيقي للمسار المكتشف، بدون تجاوز حدود التصريح.

---

# 14 — Phase 10: Documentation & Evidence Collection

## لماذا Documentation مهمة؟

واحدة من أكبر الأخطاء اللي ممكن يقع فيها Pentester إنه يعتمد على ذاكرته.

أثناء الاختبار ممكن تنفذ عشرات الخطوات، وتكتشف نتائج مختلفة، وتتنقل بين أنظمة وخدمات كثيرة.

لو ما سجلتش النتائج أول بأول، هتواجه مشكلة كبيرة في نهاية الاختبار.

ممكن تنسى:

- إزاي وصلت للنتيجة؟
- ما هو الـ Request المستخدم؟
- ما هو الـ Response؟
- ما الحساب المستخدم؟
- ما مستوى الصلاحيات؟
- ما الدليل الذي يثبت المشكلة؟

## Document as You Go

لا تنتظر لنهاية الاختبار.

كلما اكتشفت معلومة مهمة، سجلها مباشرة.

## What Should You Document?

### 1. Target Information

```text
Target: 192.168.1.10
Hostname: server01
Operating System: Linux
```

### 2. Discovery Information

```text
Open Ports:
22/tcp
80/tcp
443/tcp
```

### 3. Commands and Actions

سجل الأوامر التي استخدمتها والهدف منها.

```bash
nmap -sV -p 22,80,443 192.168.1.10
```

### 4. Findings

سجل المشكلة التي اكتشفتها.

```text
Finding:
Broken Access Control.

Affected Component:
User Profile Endpoint.

Expected Behavior:
Users should only access their own profiles.

Observed Behavior:
A test user accessed another test user's profile.
```

### 5. Evidence

الأدلة ممكن تشمل:

- Screenshots.
- HTTP Requests.
- HTTP Responses.
- Terminal Output.
- Relevant Logs.
- Configuration Information.
- Proof of Concept.

## Evidence vs Finding

في فرق بين Evidence وFinding.

**Finding:** الاستنتاج أو المشكلة التي اكتشفتها.

**Evidence:** الدليل الذي يثبت هذا الاستنتاج.

مثال:

Finding:

Broken Access Control.

Evidence:

HTTP Request and Response demonstrating that an authorized test account accessed another test account's resource.

## Evidence Quality

الدليل الجيد لازم يكون:

- واضحاً.
- مرتبطاً مباشرة بالمشكلة.
- قابلًا لإعادة التحقق.
- لا يحتوي على بيانات حساسة غير ضرورية.
- كافياً لفهم النتيجة.

## Suggested Directory Structure

```text
Pentest-Project/
│
├── 01-Scope/
│   └── scope.md
│
├── 02-Recon/
│   ├── domains.txt
│   └── recon-notes.md
│
├── 03-Scanning/
│   └── scan-results.txt
│
├── 04-Enumeration/
│   └── enumeration.md
│
├── 05-Findings/
│   ├── finding-01.md
│   └── finding-02.md
│
├── 06-Evidence/
│   ├── screenshots/
│   ├── requests/
│   └── logs/
│
└── 07-Report/
    └── final-report.md
```


---

# 15 — Phase 11: Reporting & Remediation

## ما هو Penetration Testing Report؟

بعد انتهاء الاختبار وجمع النتائج والأدلة، لازم نحول كل ده إلى تقرير احترافي.

التقرير مش مجرد قائمة بالثغرات.

هو مستند يوضح:

- ماذا اختبرنا؟
- ماذا اكتشفنا؟
- كيف تم اكتشافه؟
- ما الدليل؟
- ما تأثير المشكلة؟
- ما الحل المقترح؟

## Two Main Report Sections

### 1. Executive Summary

ده الجزء الموجه للإدارة وأصحاب القرار.

مش بالضرورة يكون عندهم خلفية تقنية عميقة.

عشان كده لازم يكون واضح ومباشر.

يشمل:

- Overall Security Posture.
- Critical Findings.
- Business Impact.
- Major Risks.
- Recommended Actions.

مثال:

```text
The assessment identified multiple security weaknesses
that may expose sensitive user information.

The most significant issue involved improper access
control within the application.

Immediate remediation is recommended.
```

### 2. Technical Findings

ده الجزء الموجه للفريق التقني المسؤول عن معالجة المشكلات.

كل Finding لازم يكون لها تفاصيل واضحة.

## Recommended Finding Structure

```text
Finding ID:
PT-001

Title:
Broken Access Control

Severity:
High

Affected Asset:
Application API

Description:
A user can access another user's private resource.

Impact:
Unauthorized disclosure of sensitive information.

Evidence:
Request and response demonstrating the issue.

Reproduction Steps:
1. Authenticate as Test User A.
2. Access the relevant resource.
3. Use a test resource belonging to User B.
4. Observe the unauthorized response.

Remediation:
Implement server-side authorization checks
for every resource access operation.
```

## Severity Assessment

ممكن تستخدم:

| Severity | Description |
|---|---|
| Critical | تأثير شديد جداً على النظام أو البيانات |
| High | تأثير أمني كبير |
| Medium | تأثير متوسط |
| Low | تأثير محدود |
| Informational | ملاحظة أو معلومة أمنية |

لازم مستوى الخطورة يعكس التأثير الفعلي والسياق، مش مجرد اسم الثغرة.

## Remediation

مش كفاية تقول للعميل:

"Fix the vulnerability."

لازم تقدم توصيات قابلة للتنفيذ.

مثلاً في Broken Access Control:

- Implement server-side authorization.
- Validate ownership of requested resources.
- Apply least privilege.
- Enforce access checks on every sensitive endpoint.
- Add automated authorization tests.

## Report Quality

التقرير الاحترافي لازم يكون:

- Accurate.
- Clear.
- Reproducible.
- Evidence-based.
- Actionable.

---

# 16 — Phase 12: Retesting

## ما هو Retesting؟

بعد ما العميل يستلم التقرير ويبدأ في إصلاح الثغرات، ممكن تحتاج تعمل Retesting.

الهدف هو التأكد من إن المشكلة اتعالجت بالفعل.

مش كفاية إن الفريق التقني يقول إنه أصلح المشكلة.

لازم نتحقق من النتيجة.

## Retesting Workflow

1. Review the Original Finding.
2. Understand the Proposed Fix.
3. Repeat the Relevant Test.
4. Verify the Result.
5. Update the Finding Status.

## Possible Results

| Status | Meaning |
|---|---|
| Fixed | المشكلة تم إصلاحها |
| Partially Fixed | تم إصلاح جزء من المشكلة |
| Not Fixed | المشكلة ما زالت موجودة |
| Unable to Verify | تعذر التحقق |
| Regression | ظهرت مشكلة جديدة نتيجة التعديل |

## Example

Original Finding:

Broken Access Control.

Original Behavior:

User A could access User B's resource.

After Remediation:

The server checks resource ownership.

Retest:

Repeat the same authorized test using the test accounts.

Expected Result:

The server denies unauthorized access.

## Why Is Retesting Important?

لأنه بيربط عملية اكتشاف الثغرات بعملية تحسين الأمان الفعلية.

الهدف النهائي مش اكتشاف المشاكل فقط، لكن التأكد من إنها اتحلت.


---

# 17 — How All Phases Work Together

## The Complete Practical Example

خلينا نربط المراحل ببعض من خلال سيناريو افتراضي داخل Lab مصرح به.

عندنا Target:

```text
192.168.56.10
```

## Step 1 — Planning

حددنا:

- الهدف: Web Server Security Assessment.
- الـ Scope: الجهاز المحدد.
- الأنشطة المسموحة: Recon, Scanning, Enumeration, Safe Validation.
- الأنشطة الممنوعة: DoS وأي نشاط خارج التصريح.

## Step 2 — Reconnaissance

جمعنا معلومات عامة عن Target.

```text
Target:
192.168.56.10

Known Asset:
Web Server
```

## Step 3 — Scanning

اكتشفنا:

```text
PORT     STATE     SERVICE

22/tcp   open      ssh
80/tcp   open      http
443/tcp  open      https
```

## Step 4 — Enumeration

جمعنا معلومات عن الخدمات.

```text
22/tcp:
SSH Service

80/tcp:
HTTP Service

443/tcp:
HTTPS Service
```

## Step 5 — Vulnerability Assessment

أثناء فحص تطبيق الويب، لاحظنا احتمال وجود مشكلة في Access Control.

## Step 6 — Exploitation / Validation

استخدمنا حسابين تجريبيين داخل Lab لإثبات إمكانية الوصول غير المصرح به إلى Resource.

## Step 7 — Post-Exploitation

قيّمنا قيمة الوصول، وحددنا الموارد التي أصبحت متاحة للحساب.

## Step 8 — Privilege Escalation

راجعنا الصلاحيات وتأكدنا من وجود أو عدم وجود مسار تصعيد ضمن نطاق الاختبار.

## Step 9 — Lateral Movement

راجعنا إمكانية الوصول إلى أنظمة أخرى وفق حدود التصريح.

## Step 10 — Documentation

سجلنا:

- Requests.
- Responses.
- Screenshots.
- Commands.
- Findings.
- Evidence.

## Step 11 — Reporting

أنشأنا تقريراً يوضح:

- المشكلة.
- التأثير.
- الدليل.
- خطوات إعادة الاختبار.
- الحل المقترح.

## Step 12 — Retesting

بعد الإصلاح، أعدنا اختبار المشكلة وتحققنا من النتيجة.

## The Big Picture

كل مرحلة اعتمدت على نتيجة المرحلة السابقة.

لم نستخدم أي Tool بشكل عشوائي.


---

# 18 — Practical Pentesting Mindset

## Stop Thinking Like a Tool Operator

أهم فكرة في الدرس كله إنك ما تبقاش مجرد شخص بيشغل Tools.

في فرق كبير بين شخص بيستخدم Nmap وشخص فاهم ليه بيستخدم Nmap.

### Tool Operator

```text
Run Nmap.
Get Results.
Run Another Tool.
Get More Results.
```

المشكلة إن الشخص هنا بيجمع نتائج بدون ما يكون عنده تصور واضح.

### Methodology-Driven Pentester

```text
Question:
Which services are available?

Action:
Perform authorized port scanning.

Observation:
Ports 22 and 80 are open.

Question:
What services are running?

Action:
Perform service detection.

Observation:
SSH and HTTP identified.

Question:
What information can these services reveal?

Action:
Perform service-specific enumeration.

Decision:
Analyze the results and identify relevant weaknesses.
```

## Questions You Should Always Ask

قبل كل خطوة:

1. What do I know?
2. What information am I missing?
3. What do I want to discover?
4. Which method can answer this question?
5. What does the result mean?
6. What should I do next?

## The Decision-Based Workflow

```text
       Current Information
                |
                v
        Identify Knowledge Gap
                |
                v
          Ask a Question
                |
                v
        Select a Method / Tool
                |
                v
           Perform Test
                |
                v
          Analyze Results
                |
                v
         Make a Decision
                |
                v
         Next Investigation
```


---

# 19 — Professional Penetration Testing Checklist

استخدم الـ Checklist دي كمرجع أثناء أي اختبار مصرح به.

## Pre-Engagement

- [ ] Define the objective.
- [ ] Confirm written authorization.
- [ ] Identify in-scope assets.
- [ ] Identify out-of-scope assets.
- [ ] Review Rules of Engagement.
- [ ] Confirm testing window.
- [ ] Identify restricted activities.
- [ ] Confirm emergency contacts.

## Reconnaissance

- [ ] Collect public information.
- [ ] Identify domains.
- [ ] Identify subdomains.
- [ ] Review public DNS information.
- [ ] Identify publicly visible technologies.
- [ ] Build a target profile.
- [ ] Keep all activities within scope.

## Scanning

- [ ] Perform authorized host discovery.
- [ ] Identify open ports.
- [ ] Detect services.
- [ ] Identify possible operating systems.
- [ ] Save scan results.
- [ ] Review unexpected responses.

## Enumeration

- [ ] Identify service versions.
- [ ] Review service configurations.
- [ ] Identify available resources.
- [ ] Review authentication mechanisms.
- [ ] Identify relevant technologies.
- [ ] Document important observations.

## Vulnerability Assessment

- [ ] Analyze discovered technologies.
- [ ] Identify potential weaknesses.
- [ ] Review known vulnerabilities.
- [ ] Check configurations.
- [ ] Validate potential findings.
- [ ] Eliminate false positives.
- [ ] Assess risk and impact.

## Exploitation

- [ ] Confirm the vulnerability.
- [ ] Review authorization.
- [ ] Select a safe validation method.
- [ ] Minimize system impact.
- [ ] Capture evidence.
- [ ] Record the result.

## Post-Exploitation

- [ ] Identify the current environment.
- [ ] Identify the current user.
- [ ] Understand access permissions.
- [ ] Assess accessible resources.
- [ ] Evaluate the value of access.
- [ ] Decide whether further testing is necessary.

## Privilege Escalation

- [ ] Review current privileges.
- [ ] Identify potential privilege escalation paths.
- [ ] Review relevant configurations.
- [ ] Validate findings safely.
- [ ] Document the result.

## Lateral Movement

- [ ] Understand network relationships.
- [ ] Identify relevant trust boundaries.
- [ ] Review authorized access paths.
- [ ] Assess the impact of potential movement.
- [ ] Avoid unauthorized systems.

## Documentation

- [ ] Record commands.
- [ ] Record observations.
- [ ] Save relevant outputs.
- [ ] Capture screenshots.
- [ ] Record requests and responses.
- [ ] Document findings.
- [ ] Link evidence to findings.

## Reporting

- [ ] Prepare Executive Summary.
- [ ] Document Technical Findings.
- [ ] Assign appropriate severity.
- [ ] Explain business impact.
- [ ] Include evidence.
- [ ] Provide remediation recommendations.
- [ ] Review report quality.

## Retesting

- [ ] Review remediation changes.
- [ ] Repeat original tests.
- [ ] Verify the results.
- [ ] Update finding status.
- [ ] Document remaining risks.

---

# 20 — Key Takeaways

## أهم الأفكار اللي لازم تخرج بيها من الدرس

1. Penetration Testing مش مجموعة أوامر، لكنه عملية منظمة.
2. لازم تفهم الـ Scope والـ Authorization قبل أي Testing Activity.
3. Reconnaissance هدفه بناء صورة عامة عن Target.
4. Scanning بيكشف Hosts وPorts وServices.
5. Enumeration بيجمع تفاصيل أعمق عن الخدمات المكتشفة.
6. Vulnerability Assessment بيحدد نقاط الضعف المحتملة ويتحقق منها.
7. Exploitation هدفه إثبات التأثير، مش إحداث أكبر ضرر.
8. Post-Exploitation بيحدد قيمة الوصول اللي حصلنا عليه.
9. Privilege Escalation بيختبر إمكانية الوصول إلى صلاحيات أعلى أو تجاوز حدود الحسابات.
10. Lateral Movement بيختبر إمكانية الانتقال إلى أنظمة أخرى.
11. Documentation لازم تبدأ من أول يوم، مش في نهاية الاختبار.
12. Reporting لازم يكون واضحاً ومفيداً للإدارة والفريق التقني.
13. Retesting بيأكد إن الثغرات تم إصلاحها.
14. كل خطوة لازم يكون ليها سبب واضح ونتيجة تساعد في اتخاذ القرار التالي.

## The Ultimate Rule

> Don't just run tools. Ask questions, understand the results, validate your assumptions, and make evidence-based decisions.

**The goal is not to run more tools. The goal is to understand the target better.**

---

# Final Mind Map

```text
PENETRATION TESTING METHODOLOGY
│
├── 01. PRE-ENGAGEMENT
│   ├── Objective
│   ├── Scope
│   ├── Authorization
│   └── Rules of Engagement
│
├── 02. RECONNAISSANCE
│   ├── Passive Recon
│   └── Active Recon
│
├── 03. SCANNING
│   ├── Host Discovery
│   ├── Port Scanning
│   └── Service Detection
│
├── 04. ENUMERATION
│   ├── SSH
│   ├── HTTP
│   ├── FTP
│   ├── DNS
│   └── SMB
│
├── 05. VULNERABILITY ASSESSMENT
│   ├── Identification
│   ├── Validation
│   ├── Risk Assessment
│   └── Prioritization
│
├── 06. EXPLOITATION
│   ├── Controlled Testing
│   ├── Proof of Concept
│   └── Impact Validation
│
├── 07. POST-EXPLOITATION
│   ├── System Information
│   ├── Current User
│   └── Access Assessment
│
├── 08. PRIVILEGE ESCALATION
│   ├── Vertical
│   └── Horizontal
│
├── 09. LATERAL MOVEMENT
│   ├── Network Relationships
│   ├── Trust Boundaries
│   └── Authorized Access Paths
│
├── 10. DOCUMENTATION
│   ├── Commands
│   ├── Findings
│   └── Evidence
│
├── 11. REPORTING
│   ├── Executive Summary
│   ├── Technical Findings
│   └── Remediation
│
└── 12. RETESTING
    ├── Repeat Tests
    ├── Verify Fixes
    └── Update Results
```

---

**End of  — Penetration Testing Methodology & Real-World Workflow**

**Study Principle:** Understand → Observe → Hypothesize → Test → Analyze → Document → Decide.

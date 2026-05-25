# 🖥️ Windows PIN Disabled — সমস্যা ও সমাধান

---

## ⚠️ সমস্যা

Windows লগইন স্ক্রিনে নিচের বার্তা দেখা যায়:

> *"This sign-in option is disabled because of failed sign-in attempts or repeated shutdowns. Use a different sign-in option, or keep your device powered on for at least 2 hours and then try again."*

### কারণ
- বারবার ভুল PIN দেওয়া, অথবা
- বারবার হঠাৎ PC force shutdown হওয়া

---

## ✅ সমাধান

### ধাপ ১ — CMD Admin হিসেবে খুলুন
Start Menu তে Right-click করুন → **Terminal (Admin)** বা **Command Prompt (Admin)** সিলেক্ট করুন।

### ধাপ ২ — এই Command টি চালান

```cmd
certutil -deleteHelloContainer
```

সফল হলে নিচের message দেখাবে:
```
Sign out now to complete this task.
CertUtil: -DeleteHelloContainer command completed successfully.
```

### ধাপ ৩ — Sign out করুন
Start Menu → আপনার নাম → **Sign out**

### ধাপ ৪ — Password দিয়ে লগইন করুন
লগইন স্ক্রিনে **Microsoft Account Password** দিয়ে ঢুকুন।

> PIN আর থাকবে না। চাইলে পরে নতুন PIN সেট করতে পারবেন।

---

## 📖 এই Command কী করে?

`certutil -deleteHelloContainer` Windows Hello এর সব security data (PIN, Fingerprint, Face ID) সম্পূর্ণ মুছে দেয়, ফলে PIN এর বাধা আর থাকে না।

---

> 💡 **পরামর্শ:** Microsoft Account এর password সবসময় মনে রাখুন — PIN কাজ না করলে এটাই একমাত্র backup।

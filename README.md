🟧 #Dirb nima?

dirb — bu web content scanner, ya’ni saytning yashirin papka (directories) va fayllarini topish uchun ishlatiladigan URL bruteforce vositasi.

U quyidagilarni aniqlashga yordam beradi:
  - Yashirin admin panellari
  - Domen ichidagi kataloglar (/admin/, /uploads/, /backup/…)
  - Fayllar (config.php, login.php, .git, robots.txt, phpinfo.php)
  - Yangi joylangan yoki unutilgan test kataloglari

Dirb aslida dirbusterning CLI versiyasi deb qaraladi.

---

🟧 Qanday ishlaydi?

Dirb wordlist (so‘zlar ro‘yxati) asosida URL’larni tekshiradi.

Masalan:
  - http://example.com/admin → mavjudmi?
  - http://example.com/upload → mavjudmi?  
  - http://example.com/test/ → mavjudmi?
Sayt kod qaytarsa (200/301/302), dirb uni topilgan deb belgilaydi.

--- 

🟧 Oddiy foydalanish
```
dirb http://example.com
```

Natijada default wordlist bilan bruteforce qiladi.

---
🟧 Wordlist bilan ishlatish (tavsiya qilingan usul)

```
dirb http://example.com /usr/share/wordlists/dirb/common.txt
```
Yoki katta ro‘yxat:
```
dirb http://example.com /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
---

🟧 HTTPS saytlar uchun:
```
dirb https://example.com
```

---

🟧 Ko‘proq parametrlar (Amaliy)
1) Dirb’da “extensions” qo‘shish

Sayt PHP yoki ASP bo‘lsa, fayllarni topish oson bo‘ladi:
```
dirb http://example.com -X .php,.html,.bak,.txt
```
2) Proxy orqali ishlash (Burp bilan)
```
dirb http://example.com -p 127.0.0.1:8080
```
3) User-agentni o‘zgartirish
```
dirb http://example.com -a "Mozilla/5.0"
```
4) Faqat mavjud kataloglarni ko‘rsatish
```
dirb http://example.com -S
```
5) SSL sertifikatni tekshirmasdan HTTPS
```
dirb https://site.com -k
```

---

🟧 Dirb natijalarni qanday tahlil qiladi?

Dirb asosan quyidagi HTTP kodlarni ko‘rsatadi:
```
| Kod     | Ma'nosi       | Pentest uchun                              |
| ------- | ------------- | ------------------------------------------ |
| 200     | OK            | Katalog/fayl mavjud                        |
| 301/302 | Redirect      | Haqiqiy directory bo‘lishi mumkin          |
| 403     | Forbidden     | Mavjud, lekin yopilgan (bu juda qimmatli!) |
| 404     | Topilmadi     | Keraksiz, filtrlanadi                      |
| 500     | Server xatosi | Zararli konfiguratsiya bo‘lishi mumkin     |
```

Eng qimmatli joylar:
🔹 /admin/
🔹 /backup/
🔹 /test/
🔹 /old/
🔹 .git/
🔹 /dev/
🔹 /uploads/
🔹 /private/

---

🟧 Dirbning kuchli tomonlari

  - Juda tez ishlaydi
  - Kam resurs yeydi
  - CLI’dan boshqarish qulay
  - Wordlist’lar juda ko‘p
  - Bruteforce logikasi yaxshi

🟥 Dirbning cheklovlari

  - WAF (Cloudflare, ModSecurity) kuchli joylarda bloklanishi mumkin
  - Ko‘p redirect’lar bo‘lsa, chalg‘ib ketishi mumkin
  - Dinamik sayt strukturasini to‘liq topmaydi
  - Rate-limit bor joylarda blok hozir bo‘ladi
Shu sababli uni gobuster, feroxbuster, wfuzz bilan birga ishlatish optimal.

---

🟧 Real misol (amaliy)

Saytni common.txt bilan skan qilish:
```
dirb https://target.uz /usr/share/wordlists/dirb/common.txt -r
```

Natijalar:
```
==> DIRECTORY: https://target.uz/admin/
==> DIRECTORY: https://target.uz/uploads/
==> FILE: https://target.uz/robots.txt
==> CODE:403: https://target.uz/private/
```
👉 403 chiqsa ham katalog mavjud degani — bu juda muhim!

🟧 Dirb nima?

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

## **Node.js Modullar Tizimi Haqida ma’lumot**

### **1\. Bu nima?**

**Node.js modullari** — bu alohida funksionallikka ega va qayta ishlatilishi mumkin bo'lgan kod bloklari yoki fayllar. Tasavvur qiling, katta bir Lego konstruksiyasi bor: har bir g'ishtcha — bu bitta modul. Ular bir-biridan mustaqil, lekin birgalikda butun bir tizimni hosil qiladi. Texnik tilda, bu **Enkapsulyatsiya** (ma'lumotlarni yashirish va himoya qilish) prinsipini amalga oshirish usulidir.

### **2\. Nima uchun kerak?**

Agarda hamma kodni bitta index.js fayliga yozsangiz, loyiha kengaygan sari uni o'qish, test qilish va xatolarini tuzatish imkonsiz bo'lib qoladi. Modullar tizimi quyidagi muammolarni hal qiladi:

* **Tartibsizlik (Spaghetti code):** Kodni mantiqiy qismlarga ajratadi.  
* **Qayta ishlatish (Reusability):** Bir marta yozilgan modulni (masalan, parolni shifrlash moduli) loyihaning turli joylarida ishlatish mumkin.  
* **Nomlar to'qnashuvi:** Har bir modul o'zining shaxsiy doirasiga (scope) ega, shuning uchun bir xil o'zgaruvchi nomlari turli fayllarda bir-biriga xalaqit bermaydi.

### **3\. Qanday ishlaydi?**

Node.js'da har bir fayl alohida modul hisoblanadi. U yerda e'lon qilingan o'zgaruvchilar va funksiyalar "yopiq" bo'ladi. Ularni tashqariga chiqarish uchun bizga **Export** va **Import** mexanizmlari kerak.

* **CommonJS (CJS):** Node.js'ning an'anaviy usuli. module.exports orqali chiqariladi va require() orqali chaqiriladi.  
* **ES Modules (ESM):** Zamonaviy JavaScript standarti. export orqali chiqariladi va import orqali chaqiriladi.

### **4\. Qaysi paytda ishlatiladi?**

Real hayotda, masalan, **User Authentication** (Foydalanuvchini tizimga kirishi) tizimida:

* dbConnector.js: Bazaga ulanish uchun modul.  
* authController.js: Kirish/chiqish mantiqi uchun modul.  
* validation.js: Email va parolni tekshirish uchun modul.

### **5\. Loyiha arxitekturasida o'rni**

Modullar tizimi asosan **Backend (Server-side)** qismiga tegishli bo'lib, loyiha arxitekturasining **poydevorini** tashkil qiladi. U loyihaning boshqariluvchanligini (Maintainability) va testga chidamliligini ta'minlaydi.

---

## **Amaliy Misol (CommonJS usulida)**

Keling, oddiy kalkulyator moduli yaratamiz.

**1\. math.js (Modul yaratish va eksport qilish):**

const add \= (a, b) \=\> a \+ b;

const subtract \= (a, b) \=\> a \- b;

// Funksiyalarni tashqariga eksport qilamiz

module.exports \= {

    add,

    subtract

};

**2\. app.js (Moduldan foydalanish):**

const math \= require('./math'); // Local modulni chaqirish

console.log("Qo'shish:", math.add(10, 5));     // 15

console.log("Ayirish:", math.subtract(10, 5)); // 5

---

## **🛠 Vazifa**

**Mavzuni mustahkamlash uchun quyidagi vazifani bajaring:**

1. `logger.js` nomli fayl yarating.   
2. Uning ichida `info(message)` va `error(message)` funksiyalarini yozing.   
   * `info` funksiyasi xabarni: `[INFO]: <xabar>` ko'rinishida chiqarsin.   
   * `error` funksiyasi xabarni: `[ERROR]: <xabar>` ko'rinishida chiqarsin.   
3. Ushbu funksiyalarni `module.exports` orqali chiqaring.   
4. `index.js` faylida ushbu modulni `require` orqali chaqiring va ikkala funksiyani ham ishlatib ko'ring.  

---

**Node.js ning asosiy (Core) modullari**

Node.js o'rnatilgan holda juda ko'p foydali modullar bilan birga keladi:

* fs (**File System**): Fayllarni o'qish, yozish va boshqarish.  
* http / https: **HTTP** server yaratish va so'rovlar yuborish.  
* path: Fayl yo'llarini qayta ishlash.  
* os (**Operating System**): Operatsion tizim haqida ma'lumot olish (xotira, CPU).  
* events: Hodisalarni boshqarish (Event Emitter).  
* crypto: Shifrlash va xavfsizlik funksiyalari.  
* stream: Ma'lumotlar oqimini boshqarish.  
* util: Yordamchi funksiyalar.  
* net: Socket dasturlash (TCP serverlar).  
* url: URL manzillarni tahlil qilish.  
* querystring: So'rov satrlarini (query strings) ishlash.

**Modullar turlari**

1. **Core Modules:** Node.js o'rnatilganda avtomatik keladi.  
2. **Local Modules:** Dasturchining o'zi tomonidan yaratilgan fayllar (masalan, const myMod \= require('./myModule')).  
3. **NPM Modules (Third-party):** npm install orqali yuklanadigan tashqi kutubxonalar (masalan, express, mongoose).

**Modullarni yuklash usullari** 

* **CommonJS:** const fs \= require('fs');  
* **ES Modules:** import fs from 'fs';

## **Node.js Modullar Tizimi Strukturasi**

Node.js modullari arxitekturasini quyidagicha tasavvur qilish mumkin:

---

### **1\. Modullar bilan ishlashda muhim farqlar**

Siz aytib o'tgan **CommonJS** va **ES Modules** o'rtasidagi farq faqatgina sintaksisda emas, balki ularning ishlash mexanizmida hamdir:

| Xususiyat | CommonJS (require) | ES Modules (import) |
| :---- | :---- | :---- |
| **Yuklanishi** | Sinxron (ketma-ket) | Asinxron (parallel) |
| **Qayerda ishlatiladi** | Standart Node.js (eskiroq) | Zamonaviy JS (brauzer va Node.js) |
| **Fayl kengaytmasi** | .js yoki .cjs | .mjs yoki package.jsonda "type": "module" |

---

### **2\. Core Modullarga misol: fs va http**

Node.js'ning eng ko'p ishlatiladigan core modullaridan biri bu http moduli bo'lib, u orqali biz soniyalar ichida server yaratishimiz mumkin.

**3\. server.js**  **(Server yaratish):**

const http \= require('http');

const server \= http.createServer((req, res) \=\> {

    res.write('Salom, Node.js\!');

    res.end();

});

server.listen(3000);

---

### **3\. Local Modules: Eksport qilish usullari**

O'zingiz yaratgan modullarni (Local Modules) boshqa fayllarda ishlatish uchun ularni eksport qilishingiz kerak:

* **Bitta funksiyani eksport qilish:** module.exports \= myFunction;  
* **Obyekt sifatida eksport qilish:** module.exports \= { func1, func2 };

---

### **4\. NPM (Third-party) Modullar**

Bu modullar loyihangizdagi node\_modules papkasiga yuklanadi va ularni ishlatish uchun birinchi navbatda npm init orqali package.json faylini yaratib olish tavsiya etiladi.

**Eslatma:** Core modullarni chaqirganda yo'l ko'rsatish shart emas (require('fs')), lekin local modullarda albatta nuqta va slesh ishlatiladi (require('./myFile')).

**NodeJS Modules (Amali masalalar)**

* fs (**File System**): Fayllarni o'qish, yozish va boshqarish.

NodeJS'ning fs (File System) moduli kompyuter fayl tizimi bilan ishlash uchun o'rnatilgan kuchli vosita bo'lib, fayllarni o'qish, yozish, yaratish, o'chirish, papkalar bilan ishlash va ularning ruxsatnomalarini boshqarish imkonini beradi. U asinxron (bloklamaydigan) va sinxron (bloklaydigan) usullarni qo'llab-quvvatlaydi, bu esa ma'lumotlar bilan ishlashda moslashuvchanlikni ta'minlaydi.

fs modulining asosiy vazifalari:

* Fayllarni o'qish va yozish: fs.readFile() orqali fayl tarkibini o'qish, fs.writeFile() orqali yangi fayl yaratish yoki mavjudini ustidan yozish.  
* Fayllarni yangilash (Append): fs.appendFile() orqali mavjud fayl oxiriga ma'lumot qo'shish.  
* Fayllarni boshqarish: fs.unlink() bilan fayllarni o'chirish, fs.rename() bilan nomini o'zgartirish yoki ko'chirish.  
* Kataloglar (Papkalar) bilan ishlash: fs.mkdir() bilan yangi papka yaratish, fs.readdir() bilan papka tarkibini o'qish va fs.rmdir() bilan o'chirish.  
* Fayl ma'lumotlari (Metadata): fs.stat() orqali fayl hajmi, yaratilgan vaqti va ruxsatnomalari haqida ma'lumot olish.  
* Fayllarni kuzatish: fs.watchFile() orqali fayldagi o'zgarishlarni real vaqt rejimida kuzatish.

Modul sinxron (masalan, readFileSync), asinxron callback (masalan, readFile) va Promise (fs.promises) usullarini taqdim etadi.

Node.js ning fs moduli bilan ishlashda eng mukammal real keys — bu "Log-fayllarni boshqarish va tahlil qilish tizimi"dir. Bu backend dasturchining kundalik ishida eng ko'p duch keladigan holatlaridan biri: tizimdagi xatoliklarni faylga yozish va keyinchalik ularni o'qib, tahlil qilish.

Keling, ushbu masalani Senior darajasida, amaliy misol bilan ko'rib chiqamiz.

---

### **🚀 Real Masala: "Logger & Stats System"**

**Vazifa:** Loyihamizda sodir bo'layotgan muhim hodisalarni logs.txt fayliga yozib boradigan, mavjud loglarni o'qib bera oladigan va fayl hajmini nazorat qiladigan tizim yaratish.

### **1\. Bu nima?**

fs (File System) — bu kompyuteringizning xotirasidagi fayllar va papkalar bilan to'g'ridan-to'g'ri muloqot qiluvchi modul. U orqali dasturimiz tashqi dunyoda iz qoldiradi.

### **2\. Nima uchun kerak?**

Ma'lumotlar bazasi (Database) har doim ham mavjud bo'lmasligi mumkin yoki juda kichik ma'lumotlar (sozlamalar, loglar) uchun bazani yuklantirish shart emas. fs quyidagilar uchun kerak:

* Foydalanuvchi yuklagan rasmlarni saqlash.  
* Konfiguratsiya fayllarini (.json, .env) o'qish.  
* Tizim xatoliklarini arxivlash.

### **3\. Qanday ishlaydi?**

fs moduli uch xil usulda ishlaydi:

1. **Sync (Sinxron):** Kod to'xtab turadi (bloklanadi), fayl bilan ish bitguncha kutadi.  
2. **Callback (Asinxron):** Kod davom etaveradi, ish bitgach funksiya chaqiriladi.  
3. **Promises (Modern asinxron):** async/await yordamida zamonaviy va toza kod yozish imkonini beradi (Tavsiya etiladi).

---

### **🛠 Amaliy Kod (Advanced Solution)**

Keling, xatolarni yozuvchi va fayl statistikasini ko'rsatuvchi kichik tizim yozamiz:

fs.js

const fs \= require('fs').promises; // Promises versiyasidan foydalanamiz

const path \= require('path');

const logFilePath \= path.join(\_\_dirname, 'system.log');

async function manageLogs() {

    try {

        // 1\. Faylga log yozish (Agar fayl yo'q bo'lsa yaratadi, bor bo'lsa davomidan qo'shadi)

        const timestamp \= new Date().toISOString();

        const logEntry \= \`\[${timestamp}\] ERROR: Ma'lumotlar bazasiga ulanib bo'lmadi.\\n\`;

        

        await fs.appendFile(logFilePath, logEntry, 'utf8');

        console.log("✅ Log muvaffaqiyatli yozildi.");

        // 2\. Faylni o'qish

        const data \= await fs.readFile(logFilePath, 'utf8');

        console.log("📖 Fayl mazmuni:\\n", data);

        // 3\. Fayl statistikasini olish (Hajmi, yaratilgan vaqti)

        const stats \= await fs.stat(logFilePath);

        console.log(\`📊 Fayl hajmi: ${stats.size} bytes\`);

        if (stats.size \> 1024 \* 1024) { // Agar fayl 1MB dan oshsa

            console.log("⚠️ Fayl hajmi juda katta, uni arxivlash tavsiya etiladi.");

        }

    } catch (err) {

        console.error("❌ Xatolik yuz berdi:", err.message);

    }

}

manageLogs();

---

### **4\. Qaysi paytda ishlatiladi?**

* **Backend:** Foydalanuvchi profil rasmini yuklaganda (fs.rename).  
* **DevOps:** Server sozlamalarini avtomatik o'zgartirish.  
* **Database:** Local JSON bazalar bilan ishlash (masalan, kichik loyihalarda db.json).

### **5\. Qaysi bo'limlar uchun muhim?**

Bu asosan **Backend** va **Infrastruktura** uchun muhim. Xavfsizlik nuqtai nazaridan juda nozik bo'lim, chunki fayl tizimiga noto'g'ri ruxsat berish (permissions) butun serverni xavf ostiga qo'yishi mumkin.

---

### **🧠 Mustahkamlash uchun vazifa:**

**"Secret Note" (Maxfiy eslatma) dasturini yarating:**

1. secret.txt degan fayl yarating va ichiga biror matn yozing.  
2. Dasturingiz ishga tushganda o'sha faylni o'qisin.  
3. Faylni o'qib bo'lgach, xavfsizlik yuzasidan o'sha faylni **o'chirib tashlasin** (fs.unlink).

**Maslahat:** fs.unlink(path) metodi faylni o'chirish uchun ishlatiladi. Omad\!


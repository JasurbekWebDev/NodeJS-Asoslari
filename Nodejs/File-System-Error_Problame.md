```javascript

const fs = require('fs');
const path = require('path');

const fileNmePath = path.join(__dirname, 'data_text.txt');

//Fayl yaratish va unga ma'lumot yozish 
fs.writeFile(fileNmePath, "Salom, bu NodeJS File System modulining misoli!", (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})

//Fayl yaratish vaqidagi xatolik turlari:
//1. Ruxsat etilmagan joyda fayl yaratishga harakat qilish (Permission Denied)
//2. Fayl nomida noto'g'ri belgilar ishlatish (Invalid File Name)
//3. Diskda joy yetishmasligi (Disk Full)
//4. Fayl tizimi bilan bog'liq xatoliklar (File System Errors)
//5. Fayl nomining uzunligi cheklovidan oshishi (File Name Too Long)
//6. Fayl tizimi ruxsatlari bilan bog'liq muammolar (File System Permissions Issues)
//7. Fayl tizimi bilan bog'liq boshqa xatoliklar (Other File System Errors)

// Xatoliklarni boshqarish uchun try-catch blokidan foydalanish mumkin, lekin fs.writeFile asinxron funksiya bo'lgani uchun, xatolikni callback funksiyasida tekshirish kerak.

// Fayl yaratishda xatolik uchun misol:
fs.writeFile('/restricted/data_text.txt', "Bu fayl yaratilmadi!", (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})
/*
Tushuntrish:
Yuqoridagi kodda, biz '/restricted/data_text.txt' nomli fayl yaratishga harakat qildik. Agar bu joyda fayl yaratish uchun ruxsat etilmagan bo'lsa, fs.writeFile funksiyasi xatolikni callback funksiyasiga uzatadi. Biz bu xatolikni tekshirib, konsolga chiqaramiz. Agar fayl muvaffaqiyatli yaratilsa, muvaffaqiyatli xabar chiqariladi.

Bu qanday xatolik yuz berishi mumkin:
1. Agar '/restricted' katalogi mavjud bo'lmasa yoki unga yozish ruxsati bo'lmasa, "EACCES: permission denied" yoki "ENOENT: no such file or directory" xatoliklari yuz berishi mumkin.
2. Agar diskda joy yetishmasa, "ENOSPC: no space left on device" xatoligi yuz berishi mumkin.
3. Agar fayl nomida noto'g'ri belgilar bo'lsa, "EINVAL: invalid argument" xatoligi yuz berishi mumkin.

Biz bu yerda qanday xatoga duch keldik:
- "EACCES: permission denied" - Bu xatolik, '/restricted' katalogiga yozish ruxsati yo'qligini bildiradi. Bu katalogga yozish uchun kerakli ruxsatlar bo'lishi kerak.
- "ENOENT: no such file or directory" - Bu xatolik, '/restricted' katalogi mavjud emasligini bildiradi. Fayl yaratish uchun katalog mavjud bo'lishи kerak.
- "ENOSPC: no space left on device" - Bu xatolik, diskda joy yetishmasligini bildiradi. Fayl yaratish uchun diskda yetarli joy bo'lishi kerak.
- "EINVAL: invalid argument" - Bu xatolik, fayl nomida noto'g'ri belgilar ishlatilganligini bildiradi. Fayl nomi uchun ruxsat etilgan belgilarni ishlatish kerak.
- "EISDIR: illegal operation on a directory" - Bu xatolik, fayl yaratmay harakat qilayotgan joyda katalog mavjud bo'lsa yuz berishi mumkin. Fayl yaratish uchun katalog o'rniga fayl nomi ko'rsatilishi kerak.
- "EEXIST: file already exists" - Bu xatolik, yaratmay harakat qilayotgan fayl allaqachon mavjud bo'lsa yuz berishi mumkin. Fayl yaratish uchun yangi va mavjud bo'lmagan nom ishlatish kerak.
*/


// "EACCES: permission denied" ga misol:
fs.writeFile('/root/data_text.txt', "Bu fayl yaratilmadi!", (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
        fs.writeFile('error.json', `${err}`, (err) => {
            if (err) {
                console.log("Xato......");
            } else {
                console.log("Yuborildi.....");
                
            }
            
        })
    }
    else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})

// "ENOENT: no such file or directory" ga misol:
fs.writeFile('/nonexistent/data_text.txt', "Bu fayl yaratilmadi!", (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})

// "ENOSPC: no space left on device" ga misol:
// Bu xatolikni simulyatsiya qilish uchun, diskda yer kalmaydigan bir joyda fayl yaratishga harakat qilish mumkin. Misol uchun, /dev/null kabi maxsus faylga yozishga harakat qilish mumkin:
fs.writeFile('/dev/null/data_text.txt', "Bu fayl yaratilmadi!", (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})

// "EINVAL: invalid argument" ga misol:
fs.writeFile('/invalid|name.txt', "Bu fayl yaratilmadi!", (err) => {
    if (err) { 
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})

// // "EISDIR: illegal operation on a directory" ga misol:
fs.writeFile('/tmp', "Bu fayl yaratilmadi!", (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})

// // "EEXIST: file already exists" ga misol:
fs.writeFile(fileNmePath, "Bu fayl yaratilmadi!", { flag: 'wx' }, (err) => {
    if (err) {
        console.error("Fayl yaratishda xatolik yuz berdi:", err);
    } else {
        console.log("Fayl muvaffaqiyatli yaratildi va ma'lumot yozildi.")
    }
})
```
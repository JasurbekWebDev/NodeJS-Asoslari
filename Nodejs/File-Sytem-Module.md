```javascript


const fs = require('fs');
// fs nima? => fs (File System): Fayllarni o'qish, yozish va boshqarish.
// fs - bu Node.js ning fayl tizimi modulidir. Bu modul yordamida siz fayllar bilan ishlashingiz mumkin, masalan, fayllarni o'qish, yozish, o'chirish va boshqalar. fs moduli asosan asinxron va sinxron usullarni taqdim etadi, shuning uchun siz o'zingizning ehtiyojlaringizga mos ravishda tanlashingiz mumkin.

// Asinxron va Sinxron nima?
// Asinxron - bu fayl tizimi operatsiyalarini bajarishda bloklanmaydigan usullardir. Bu usullar callback funksiyalarini qabul qiladi va operatsiya tugagach, natijani callback orqali qaytaradi. Masalan, fs.readFile() asinxron usuldir.
// Sinxron - bu fayl tizimi operatsiyalarini bajarishda bloklanadigan usullardir. Bu usullar natijani to'g'ridan-to'g'ri qaytaradi va operatsiya tugaguncha kodning keyingi qismi bajarilmaydi. Masalan, fs.readFileSync() sinxron usuldir.

// fs modulidan foydalanish uchun uni require() yordamida import qilishingiz kerak. Keyin siz fs modulining metodlarini chaqirishingiz mumkin, masalan, fs.readFile() yoki fs.writeFile().

// 1. Asinxron Fayl yaratish
fs.writeFile('example.txt', 'Hello, World!', (err) => {
    if (err) throw err;
    console.log('Fayl yaratildi!');
});

// 1.2 Sinxron Fayl yaratish
try {
    fs.writeFileSync('example_sync.txt', 'Hello, World!');
    console.log('Fayl yaratildi!');
} catch (err) {
    console.error(err);
}

// 2. Asinxron Fayl o'qish
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log('Fayl mazmuni:', data);
});

// 2.2 Sinxron Fayl o'qish
try { 
    const data = fs.readFileSync('example_sync.txt', 'utf8');
    console.log('Fayl mazmuni:', data);
} catch (err) {
    console.error(err);
}

// 3. Asinxron Fayl qo'shish
fs.appendFile('example.txt', '\nQo\'shimcha matn.', (err) => {
    if (err) throw err;
    console.log('Faylga matn qo\'shildi!');
});

// 3.2 Sinxron Fayl qo'shish
try {
    fs.appendFileSync('example_sync.txt', '\nQo\'shimcha matn.');
    console.log('Faylga matn qo\'shildi!');
} catch (err) {
    console.error(err);
}

// 4. Asinxron Fayl o'chirish
fs.unlink('example.txt', (err) => {
    if (err) throw err;
    console.log('Fayl o\'chirildi!');
});

// 4.2 Sinxron Fayl o'chirish
try {
    fs.unlinkSync('example_sync.txt');
    console.log('Fayl o\'chirildi!');
} catch (err) {
    console.error(err);
}

// 5. Asinxron Fayl nomini o'zgartirish
fs.rename('example.txt', 'renamed_example.txt', (err) => {
    if (err) throw err;
    console.log('Fayl nomi o\'zgartirildi!');
});

// 5.2 Sinxron Fayl nomini o'zgartirish
try {
    fs.renameSync('example_sync.txt', 'renamed_example_sync.txt');
    console.log('Fayl nomi o\'zgartirildi!');
} catch (err) {
    console.error(err);
}

// 6. Asinxron Fayl mavjudligini tekshirish
fs.access('renamed_example.txt', fs.constants.F_OK, (err) => {
    if (err) {
        console.log('Asinxron fayl mavjud emas!');
    } else {
        console.log('Asinxron fayl mavjud!');
    }
});

// 6.2 Sinxron Fayl mavjudligini tekshirish
try {
    fs.accessSync('renamed_example_sync.txt', fs.constants.F_OK);
    console.log('Sinxron fayl mavjud!');
} catch (err) {
    console.error('Sinxron fayl mavjud emas!');
}

// 7. Asinxron Fayl ma'lumotlarini o'qish
fs.stat('renamed_example.txt', (err, stats) => {
    if (err) throw err;
    console.log('Fayl ma\'lumotlari:', stats);
});

// 7.2 Sinxron Fayl ma'lumotlarini o'qish
try {
    const stats = fs.statSync('renamed_example_sync.txt');
    console.log('Sinxron fayl ma\'lumotlari:', stats);
} catch (err) {
    console.error('Sinxron fayl ma\'lumotlarini o\'qishda xatolik:', err);
}

// 8. Asinxron Fayl ma'lumotlarini o'qish (stats)
fs.stat('renamed_example.txt', (err, stats) => {
    if (err) throw err; 
    console.log('Fayl turi:', stats.isFile() ? 'Fayl' : 'Katalog');
});

// 8.2 Sinxron Fayl ma'lumotlarini o'qish (stats)
try {
    const stats = fs.statSync('renamed_example_sync.txt');
    console.log('Fayl turi:', stats.isFile() ? 'Fayl' : 'Katalog');
} catch (err) {
    console.error('Sinxron fayl ma\'lumotlarini o\'qishda xatolik:', err);
}
```
Mana, so‘ralgan kod va ma'lumotlar o‘zgartirilmagan holda, ammo eng muhim metodlar yulduzcha bilan belgilangan formatda:

```javascript
/*
NodeJS File System Module va Module Methods: - Qiladigan ishlar:
1. File System modulini o'rnatish va import qilish
2. File System modulining asosiy metodlarini o'rganish
*/

// 1. File System modulini import qilish
const fs = require('fs');

// 2. File System modulining asosiy metodlarini o'rganish

// Fayl yaratish va unga ma'lumot yozish
fs.writeFile('example.txt', 'Salom, bu NodeJS File System modulining misoli!', (err) => {
    if (err) {
        console.error('Fayl yaratishda xatolik yuz berdi:', err);
    } else {
        console.log('Fayl muvaffaqiyatli yaratildi va ma\'lumot yozildi.'); 
    }
});

// Faylni o'qish
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Faylni o\'qishda xatolik yuz berdi:', err);
    } else {
        console.log('Fayl mazmuni:', data); 
    }
});

// Faylga ma'lumot qo'shish
fs.appendFile('example.txt', '\nBu ma\'lumot faylga qo\'shildi.', (err) => {
    if (err) {
        console.error('Faylga ma\'lumot qo\'shishda xatolik yuz berdi:', err);
    } else {
        console.log('Ma\'lumot muvaffaqiyatli qo\'shildi.'); 
    }   
});

// Faylni o'chirish
fs.unlink('example.txt', (err) => {
    if (err) {
        console.error('Faylni o\'chirishda xatolik yuz berdi:', err);
    } else {
        console.log('Fayl muvaffaqiyatli o\'chirildi.'); 
    }
});

// Fayl mavjudligini tekshirish
fs.access('example.txt', fs.constants.F_OK, (err) => {
    if (err) {
        console.log('Fayl mavjud emas.');
    } else {
        console.log('Fayl mavjud.');
    }
});

// Faylni nomini o'zgartirish
fs.rename('example.txt', 'renamed_example.txt', (err) => {
    if (err) {
        console.error('Faylni nomini o\'zgartirishda xatolik yuz berdi:', err);
    } else {
        console.log('Fayl nomi muvaffaqiyatli o\'zgartirildi.'); 
    }
});


// Faylni nusxalash
fs.copyFile('example.txt', 'copy_of_example.txt', (err) => {
    if (err) {  
        console.error('Faylni nusxalashda xatolik yuz berdi:', err);
    } else {
        console.log('Fayl muvaffaqiyatli nusxalandi.'); 
    }   
});

// Faylni o'qish va konsolga chiqarish (stream usuli)
const readStream = fs.createReadStream('example.txt', 'utf8');
readStream.on('data', (chunk) => {
    console.log('Fayl bo\'lagi:', chunk);
});
readStream.on('error', (err) => {
    console.error('Faylni o\'qishda xatolik yuz berdi:', err);
});

// Faylga ma'lumot yozish (stream usuli)
const writeStream = fs.createWriteStream('stream_example.txt');
writeStream.write('Bu ma\'lumot stream orqali yozilmoqda.\n');
writeStream.write('NodeJS File System modulining yana bir misoli.\n');
writeStream.end();

writeStream.on('finish', () => {
    console.log('Ma\'lumot muvaffaqiyatli stream orqali yozildi.'); 
});
writeStream.on('error', (err) => {
    console.error('Faylga ma\'lumot yozishda xatolik yuz berdi:', err);
});

// Faylni o'qish va yozish (async/await usuli)
async function readAndWriteFile() {
    try {
        const data = await fs.promises.readFile('example.txt', 'utf8');
        console.log('Fayl mazmuni (async/await):', data);
        await fs.promises.writeFile('async_example.txt', data);
        console.log('Fayl muvaffaqiyatli yaratildi (async/await).');
    } catch (err) {
        console.error('Xatolik yuz berdi (async/await):', err);
    }
}
readAndWriteFile();

// Faylni o'qish va yozish (synchronous usuli)
try {
    const data = fs.readFileSync('example.txt', 'utf8');
    console.log('Fayl mazmuni (synchronous):', data);
    fs.writeFileSync('sync_example.txt', data);
    console.log('Fayl muvaffaqiyatli yaratildi (synchronous).');
} catch (err) {
    console.error('Xatolik yuz berdi (synchronous):', err);
}

// Faylni o'qish va yozish (promise usuli)
fs.promises.readFile('example.txt', 'utf8')
    .then((data) => {
        console.log('Fayl mazmuni (promise):', data);
        return fs.promises.writeFile('promise_example.txt', data);
    })
    .then(() => {
        console.log('Fayl muvaffaqiyatli yaratildi (promise).');
    })
    .catch((err) => {
        console.error('Xatolik yuz berdi (promise):', err);
    });

// Faylni o'qish va yozish (callback usuli)
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Faylni o\'qishda xatolik yuz berdi (callback):', err);
    } else {
        console.log('Fayl mazmuni (callback):', data);
        fs.writeFile('callback_example.txt', data, (err) => {
            if (err) {
                console.error('Faylga yozishda xatolik yuz berdi (callback):', err);
            } else {
                console.log('Fayl muvaffaqiyatli yaratildi (callback).');
            }
        });
    }
});

// Faylni o'qish va yozish (stream usuli)
const readStream2 = fs.createReadStream('example.txt', 'utf8');
const writeStream2 = fs.createWriteStream('stream_copy_example.txt');
readStream2.pipe(writeStream2);
writeStream2.on('finish', () => {
    console.log('Fayl muvaffaqiyatli nusxalandi (stream).'); 
});
writeStream2.on('error', (err) => {
    console.error('Faylni nusxalashda xatolik yuz berdi (stream):', err);
});

// Faylni yaratish, yozish, o'qish, o'chirish (async/await usuli)
async function fileOperations() {
    try {
        await fs.promises.writeFile('full_example.txt', 'Bu fayl async/await usuli bilan yaratildi.');
        console.log('Fayl muvaffaqiyatli yaratildi (async/await).');
        const data = await fs.promises.readFile('full_example.txt', 'utf8');
        console.log('Fayl mazmuni (async/await):', data);
        await fs.promises.unlink('full_example.txt');
        console.log('Fayl muvaffaqiyatli o\'chirildi (async/await).');
    } catch (err) {
        console.error('Xatolik yuz berdi (async/await):', err);
    }
}
fileOperations();

// Faylni yaratish, yozish, o'qish, o'chirish (synchronous usuli)
try {
    fs.writeFileSync('full_example_sync.txt', 'Bu fayl synchronous usuli bilan yaratildi.');
    console.log('Fayl muvaffaqiyatli yaratildi (synchronous).');
    const data = fs.readFileSync('full_example_sync.txt', 'utf8');
    console.log('Fayl mazmuni (synchronous):', data);
    fs.unlinkSync('full_example_sync.txt');
    console.log('Fayl muvaffaqiyatli o\'chirildi (synchronous).');
} catch (err) {
    console.error('Xatolik yuz berdi (synchronous):', err);
}

// Faylni yaratish, yozish, o'qish, o'chirish (promise usuli)
fs.promises.writeFile('full_example_promise.txt', 'Bu fayl promise usuli bilan yaratildi.')
    .then(() => {
        console.log('Fayl muvaffaqiyatli yaratildi (promise).');
        return fs.promises.readFile('full_example_promise.txt', 'utf8');
    })
    .then((data) => {
        console.log('Fayl mazmuni (promise):', data);
        return fs.promises.unlink('full_example_promise.txt');
    })
    .then(() => {
        console.log('Fayl muvaffaqiyatli o\'chirildi (promise).');
    })
    .catch((err) => {
        console.error('Xatolik yuz berdi (promise):', err);
    });

// Faylni yaratish, yozish, o'qish, o'chirish (callback usuli)
fs.writeFile('full_example_callback.txt', 'Bu fayl callback usuli bilan yaratildi.', (err) => {
    if (err) {
        console.error('Fayl yaratishda xatolik yuz berdi (callback):', err);
    } else {
        console.log('Fayl muvaffaqiyatli yaratildi (callback).');
        fs.readFile('full_example_callback.txt', 'utf8', (err, data) => {
            if (err) {
                console.error('Faylni o\'qishda xatolik yuz berdi (callback):', err);
            } else {
                console.log('Fayl mazmuni (callback):', data);
                fs.unlink('full_example_callback.txt', (err) => {
                    if (err) {
                        console.error('Fayl o\'chirishda xatolik yuz berdi (callback):', err);
                    } else {
                        console.log('Fayl muvaffaqiyatli o\'chirildi (callback).');
                    }
                });
            }
        });
    }
});


/*
Eslatma: Ushbu kod snippet'lari NodeJS File System modulining turli metodlarini ko'rsatadi. Har bir metod uchun xatoliklarni tekshirish va natijalarni konsolga chiqarish uchun callback, async/await, promise va synchronous usullaridan foydalanilgan. Fayl yaratish, o'qish, yozish, o'chirish, nusxalash va boshqa operatsiyalarni amalga oshirish mumkin. Har bir operatsiya uchun alohida kod bloklari mavjud.

Eng muhim File System metodlari:
- fs.writeFile() * - Fayl yaratish va unga ma'lumot yozish
- fs.readFile() * - Faylni o'qish
- fs.appendFile() * - Faylga ma'lumot qo'shish
- fs.unlink() * - Faylni o'chirish
- fs.access() - Fayl mavjudligini tekshirish
- fs.rename() - Fayl nomini o'zgartirish
- fs.copyFile() - Faylni nusxalash
- fs.createReadStream() * - Faylni o'qish uchun stream yaratish
- fs.createWriteStream() * - Faylga ma'lumot yozish uchun stream yaratish
- fs.promises * - Promise asosida ishlaydigan metodlar to'plami
- fs.readFileSync() - Faylni synchronous usulda o'qish
- fs.writeFileSync() - Faylni synchronous usulda yaratish va unga ma'lumot yozish
- fs.unlinkSync() - Faylni synchronous usulda o'chirish
- fs.renameSync() - Fayl nomini synchronous usulda o'zgartirish
- fs.copyFileSync() - Faylni synchronous usulda nusxalash
- fs.promises.readFile() * - Faylni promise usulida o'qish
- fs.promises.writeFile() * - Faylni promise usulida yaratish va unga ma'lumot yozish
- fs.promises.unlink() - Faylni promise usulida o'chirish
- fs.promises.rename() - Fayl nomini promise usulida o'zgartirish
- fs.promises.copyFile() - Faylni promise usulida nusxalash
- fs.promises.access() - Fayl mavjudligini promise usulida tekshirish
- fs.promises.stat() * - Fayl haqida ma'lumot olish
- fs.promises.readdir() * - Katalog ichidagi fayllarni o'qish
- fs.promises.mkdir() * - Katalog yaratish
- fs.promises.rmdir() - Katalogni o'chirish
- fs.promises.rm() * - Fayl yoki katalogni o'chirish
*/
```
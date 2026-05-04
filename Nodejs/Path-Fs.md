```javascript
// NodeJS orqali JSON faylini yaratish, o'qish, yozish, qo'shish va o'chirish
// 1. Oddiy usul:
// 2. O'rta usul:
// 3. Yuqori usul:
// 4. Eng yaxshi usul:

const fs = require('fs');
const path = require('path'); 
// path modulidan foydalanib, fayl yo'lini to'g'ri ko'rsatish
const filePath = path.join(__dirname, 'data.json');

// 1. Oddiy usul: Callback funksiyalar bilan
const data = { ID: 1, name: "John", age: 30, city: "New York" };
const jsonData = JSON.stringify(data, null, 2); // JSON formatiga o'tkazish
fs.writeFile(filePath, jsonData, (err) => {
    if (err) {
        console.error('Xatolik yuz berdi:', err);
    } else {
        console.log('Fayl muvaffaqiyatli yaratildi.');
    }
});

// 2. O'rta usul: Promises bilan
const data2 = { ID: 2, name: "Alice", age: 25, city: "Los Angeles" };
const jsonData2 = JSON.stringify(data2, null, 2);
fs.promises.writeFile('data2.json', jsonData2)
    .then(() => {
        console.log('Fayl muvaffaqiyatli yaratildi (Promise).');
    })
    .catch((err) => {
        console.error('Xatolik yuz berdi:', err);
    });

// 3. Yuqori usul: Async/Await bilan
async function createJsonFile() {
    const data3 = { ID: 3, name: "Bob", age: 40, city: "Chicago" };
    const jsonData3 = JSON.stringify(data3, null, 2);
    try {
        await fs.promises.writeFile('data3.json', jsonData3);
        console.log('Fayl muvaffaqiyatli yaratildi (Async/Await).');
    } catch (err) {
        console.error('Xatolik yuz berdi:', err);
    }
}
createJsonFile();

// 4. Eng yaxshi usul: Error-first callback va Promises kombinatsiyasi
function createJsonFileBest(data, fileName) {
    const jsonData = JSON.stringify(data, null, 2);
    return fs.promises.writeFile(fileName, jsonData)
        .then(() => {
            console.log(`Fayl ${fileName} muvaffaqiyatli yaratildi.`);
        })
        .catch((err) => {
            console.error(`Fayl yaratishda xatolik yuz berdi (${fileName}):`, err);
        }); 
}

createJsonFileBest({ ID: 4, name: "Eve", age: 35, city: "Miami" }, 'data4.json'); 

// Faylni o'qish
fs.readFile('data.json', 'utf-8', (err, data) => {
    if (err) {
        console.error('Faylni o\'qishda xatolik yuz berdi:', err);
    } else {
        const jsonData = JSON.parse(data);
        console.log('Fayl mazmuni:', jsonData);
    }   
});

// Faylga ma'lumot qo'shish
fs.readFile('data.json', 'utf-8', (err, data) => {
    if (err) {
        console.error('Faylni o\'qishda xatolik yuz berdi:', err);
    } else {
        const jsonData = JSON.parse(data);
        jsonData.city = "San Francisco"; // Ma'lumotni yangilash
        const updatedJsonData = JSON.stringify(jsonData, null, 2);
        fs.writeFile('data.json', updatedJsonData, (err) => {
            if (err) {
                console.error('Faylni yozishda xatolik yuz berdi:', err);
            } else {
                console.log('Fayl muvaffaqiyatli yangilandi.');
            }
        });
    }
});

// // Faylga yangi ma'lumot qo'shish
fs.readFile('data.json', 'utf-8', (err, data) => {
    if (err) {
        console.error('Faylni o\'qishda xatolik yuz berdi:', err);
    } else {
        const jsonData = JSON.parse(data);
        jsonData.city = "San Francisco"; // Mavjud Ma'lumotni yangilash
        jsonData.email = "john@example.com"; // Yangi ma'lumot qo'shish
        const updatedJsonData = JSON.stringify(jsonData, null, 2);
        fs.writeFile('data.json', updatedJsonData, (err) => {
            if (err) {
                console.error('Faylni yozishda xatolik yuz berdi:', err);
            } else {
                console.log('Fayl muvaffaqiyatli yangilandi.');
            }
        });
    }
});

// Faylni o'chirish
fs.unlink('data3.json', (err) => {
    if (err) {
        console.error('Faylni o\'chirishda xatolik yuz berdi:', err);
    } else {
        console.log('Fayl muvaffaqiyatli o\'chirildi.');
    }
});

// Faylni o'chirish (Promise usuli)
fs.promises.unlink('data4.json')
    .then(() => {
        console.log('Fayl muvaffaqiyatli o\'chirildi (Promise).');
    })
    .catch((err) => {
        console.error('Faylni o\'chirishda xatolik yuz berdi:', err);
    });


    // Faylni o'chirish (Async/Await usuli)
async function deleteJsonFile(fileName) {
    try {
        await fs.promises.unlink(fileName);
        console.log(`Fayl ${fileName} muvaffaqiyatli o\'chirildi (Async/Await).`);
    } catch (err) {
        console.error(`Faylni o\'chirishda xatolik yuz berdi (${fileName}):`, err);
    }
}
deleteJsonFile('data4.json');

// Faylni o'chirish (Error-first callback va Promises kombinatsiyasi)
function deleteJsonFileBest(fileName) {
    return fs.promises.unlink(fileName)
        .then(() => {
            console.log(`Fayl ${fileName} muvaffaqiyatli o\'chirildi (Best).`);
        })
        .catch((err) => {
            console.error(`Faylni o\'chirishda xatolik yuz berdi (${fileName}):`, err);
        }); 
}
deleteJsonFileBest('data4.json');

// Faylni o'qish (Async/Await usuli)
async function readJsonFile(fileName) {
    try {
        const data = await fs.promises.readFile(fileName, 'utf-8');
        const jsonData = JSON.parse(data);
        console.log(`Fayl ${fileName} mazmuni:`, jsonData);
    } catch (err) {
        console.error(`Faylni o\'qishda xatolik yuz berdi (${fileName}):`, err);
    }
}
readJsonFile('data.json');

// Faylga ma'lumot qo'shish (Async/Await usuli)
async function updateJsonFile(fileName, newData) {
    try {
        const data = await fs.promises.readFile(fileName, 'utf-8');
        const jsonData = JSON.parse(data);
        const updatedData = { ...jsonData, ...newData };
        const updatedJsonData = JSON.stringify(updatedData, null, 2);
        await fs.promises.writeFile(fileName, updatedJsonData);
        console.log(`Fayl ${fileName} muvaffaqiyatli yangilandi (Async/Await).`);
    } catch (err) {
        console.error(`Faylni yangilashda xatolik yuz berdi (${fileName}):`, err);
    }   
}
updateJsonFile('data.json', { city: "San Francisco", email: "john123@example.com" });

/*
Bu kodda NodeJS orqali JSON faylini yaratish, o'qish, yozish, qo'shish va o'chirishning turli usullari ko'rsatilgan. Har bir usul uchun oddiy, o'rta, yuqori va eng yaxshi variantlar mavjud. Fayl yo'lini to'g'ri ko'rsatish uchun path modulidan foydalanilgan. Har bir operatsiya uchun xatoliklarni boshqarish ham amalga oshirilgan.

Bu amaliyotlar NodeJS'da fayl tizimi bilan ishlashning asosiy konseptlarini o'rganishga yordam beradi va real dunyo dasturlarida JSON fayllarini qanday boshqarish mumkinligini ko'rsatadi.

Biz endi JSON fayllarini yaratish, o'qish, yangilash va o'chirishni o'rgandik, bu esa ko'plab NodeJS ilovalarida foydali bo'ladi. Har bir usulning afzalliklari va kamchiliklarini tushunish, sizga eng mos keladigan usulni tanlashda yordam beradi.

Bular real dunyoda qaysi halatda kerak:
- Oddiy usul: Kichik va oddiy fayllar bilan ishlashda, yoki tez-tez o'zgarishlar kiritilmaydigan statik ma'lumotlar uchun.
- O'rta usul: Katta fayllar yoki ko'p ma'lumotlar bilan ishlashda, yoki fayl operatsiyalarini ketma-ket bajarishda.
- Yuqori usul: Asinxron operatsiyalarni boshqarish va kodni o'qilishi oson qilishda, ayniqsa ko'p fayl operatsiyalari mavjud bo'lsa.
- Eng yaxshi usul: Katta va murakkab loyihalarda, yoki kodning barqarorligi va xatoliklarni boshqarish muhim bo'lgan hollarda.

Eng yaxshi usul, odatda, asinxron operatsiyalarni boshqarish va xatoliklarni samarali tarzda boshqarish imkonini beradigan Async/Await yoki Promises kombinatsiyasidir. Bu usullar kodni o'qilishi oson va samarali qiladi, ayniqsa ko'p fayl operatsiyalari mavjud bo'lsa.

Eslatma: Fayl operatsiyalarini bajarishda, ayniqsa katta fayllar bilan ishlashda, xatoliklarni boshqarish va resurslarni to'g'ri boshqarish muhimdir. Har doim fayl operatsiyalarini bajarishda xatoliklarni tekshirish va kerak bo'lsa, resurslarni tozalashni unutmang.

Real dunyo loyihalari: (path va fs modullarini birgalikda ishlatish)
- Fayl yuklash tizimlari: Foydalanuvchilar fayllarni yuklash va boshqarish imkoniyatiga ega bo'lishi uchun path va fs modullaridan foydalanish.
- Ma'lumotlar bazasi sifatida JSON fayllar: Kichik loyihalarda yoki prototip yaratishda, ma'lumotlarni saqlash uchun JSON fayllaridan foydalanish.
- Log fayllari: Ilovaning ishlashini kuzatish uchun log fayllarini yaratish va boshqarish.
- Konfiguratsiya fayllari: Ilovaning sozlamalarini saqlash va boshqarish uchun JSON konfiguratsiya fayllaridan foydalanish.
- Fayl tizimi monitoringi: Fayl tizimidagi o'zgarishlarni kuzatish va kerakli harakatlarni bajarish uchun fs.watch yoki fs.watchFile funksiyalaridan foydalanish.
- Faylni zaxiralash va tiklash tizimlari: Muhim fayllarni zaxiralash va kerak bo'lganda tiklash uchun fs moduli yordamida fayl operatsiyalarini bajarish.
- Faylni o'qish va tahlil qilish: Katta JSON fayllarini o'qish va tahlil qilish uchun stream usullaridan foydalanish, bu esa xotira samaradorligini oshiradi.
- Faylni o'chirish va yangilash: Eski ma'lumotlarni o'chirish va yangi ma'lumotlarni qo'shish uchun fs.unlink va fs.writeFile funksiyalaridan foydalanish.
- Faylni ko'chirish va nomini o'zgartirish: fs.rename funksiyasidan foydalanib, fayllarni ko'chirish yoki nomini o'zgartirish.
- Faylni tekshirish: fs.access funksiyasidan foydalanib, fayl mavjudligini yoki unga kirish huquqini tekshirish.
- Faylni yaratish va boshqarish: fs.mkdir va fs.rmdir funksiyalaridan foydalanib, kataloglar yaratish va o'chirish.
*/
```
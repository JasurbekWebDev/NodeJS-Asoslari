
```javascript
/*
NodeJS Path Module va Module Methods: - Qiladigan ishlar:
1. Path modulini o'rnatish va import qilish
2. Path modulining asosiy metodlarini o'rganish
*/

// 1. Path modulini o'rnatish va import qilish
const path = require('path');

// 2. Path modulining asosiy metodlarini o'rganish

// a) path.basename() - Fayl nomini olish
const filePath = 'uploads//users/./images/profile.PNG';
const fileName = path.basename(filePath);
console.log('Fayl nomi:', fileName); // Output: profile.PNG

// b) path.dirname() - Fayl yo'lini olish
const dirName = path.dirname(filePath);
console.log('Fayl yo\'li:', dirName); // Output: uploads/users/images

// c) path.extname() - Fayl kengaytmasini olish
const fileExt = path.extname(filePath);
console.log('Fayl kengaytmasi:', fileExt); // Output: .PNG

// d) path.join() - Yo'llarni birlashtirish
const joinedPath = path.join('uploads', 'users', 'images', 'profile.PNG');
console.log('Birlashtirilgan yo\'l:', joinedPath); // Output: uploads/users/images/profile.PNG

// e) path.resolve() - Absolyut yo'lni olish
const absolutePath = path.resolve('uploads', 'users', 'images', 'profile.PNG');
console.log('Absolyut yo\'l:', absolutePath); // Output: /current/working/directory/uploads/users/images/profile.PNG

// f) path.normalize() - Yo'lni normalizatsiya qilish
const normalizedPath = path.normalize('uploads//users/./images/profile.PNG');
console.log('Normalizatsiya qilingan yo\'l:', normalizedPath); // Output: uploads/users/images/profile.PNG

// g) path.isAbsolute() - Yo'lning absolyut yoki nisbiy ekanligini tekshirish 
const isAbsolutePath = path.isAbsolute(filePath);
console.log('Yo\'l absolyutmi?:', isAbsolutePath); // Output: false

// h) path.parse() - Yo'lni ob'ektga ajratish
const parsedPath = path.parse(filePath);
console.log('Parsed Path:', parsedPath); 
/* Output:
{
  root: '',
  dir: 'uploads/users/images',
  base: 'profile.PNG',
  ext: '.PNG',
  name: 'profile'
}
*/

// i) path.format() - Ob'ektni yo'lga aylantirish
const formattedPath = path.format(parsedPath);
console.log('Formatted Path:', formattedPath); // Output: uploads/users/images/profile.PNG

// j) path.relative() - Ikki yo'l orasidagi nisbiy yo'lni olish
const relativePath = path.relative('uploads/users', 'uploads/users/images/profile.PNG');
console.log('Nisbiy yo\'l:', relativePath); // Output: images/profile.PNG

// k) path.sep - Operatsion tizimga mos yo'l ajratuvchisi
console.log('Yo\'l ajratuvchisi:', path.sep); // Output: / (Linux/Mac) or \ (Windows)

// l) path.delimiter - Operatsion tizimga mos yo'l ajratuvchisi (PATH muhit o'zgaruvchilari uchun)
console.log('Muqobil yo\'l ajratuvchisi:', path.delimiter); // Output: : (Linux/Mac) or ; (Windows)

// m) path.win32 - Windows uslubidagi yo'l metodlari
const winPath = path.win32.join('C:\\', 'Users', 'John', 'Documents');
console.log('Windows uslubidagi yo\'l:', winPath); // Output: C:\Users\John\Documents

// n) path.posix - POSIX uslubidagi yo'l metodlari
const posixPath = path.posix.join('/home', 'john', 'documents');
console.log('POSIX uslubidagi yo\'l:', posixPath); // Output: /home/john/documents

// o) path.parse() va path.format() metodlarini birgalikda ishlatish
const originalPath = 'uploads/users/images/profile.PNG';
const parsed = path.parse(originalPath);
const formatted = path.format(parsed);
console.log('Original Path:', originalPath);
console.log('Formatted Path:', formatted); // Output: Original Path: uploads/users/images/profile.PNG

// p) path.parse() metodining root, dir, base, ext, name xususiyatlarini o'rganish
console.log('Root:', parsed.root); // Output: ''
console.log('Dir:', parsed.dir); // Output: uploads/users/images
console.log('Base:', parsed.base); // Output: profile.PNG
console.log('Ext:', parsed.ext); // Output: .PNG
console.log('Name:', parsed.name); // Output: profile 

// q) path.join() metodining platformaga mos yo'l yaratish xususiyatini o'rganish
const platformPath = path.join('folder', 'subfolder', 'file.txt');
console.log('Platformaga mos yo\'l:', platformPath); // Output: folder/subfolder/file.txt (Linux/Mac) or folder\subfolder\file.txt (Windows)

// r) path.resolve() metodining hozirgi ishchi katalogga nisbatan absolyut yo'l yaratish xususiyatini o'rganish
const resolvedPath = path.resolve('folder', 'subfolder', 'file.txt');
console.log('Absolyut yo\'l:', resolvedPath); // Output: /current/working/directory/folder/subfolder/file.txt

// s) path.normalize() metodining yo'lni normalizatsiya qilish xususiyatini o'rganish
const messyPath = 'folder//subfolder/../file.txt';
const normalizedMessyPath = path.normalize(messyPath);
console.log('Normalizatsiya qilingan yo\'l:', normalizedMessyPath); // Output: folder/file.txt

// t) path.isAbsolute() metodining absolyut va nisbiy yo'llarni tekshirish xususiyatini o'rganish
console.log('Absolyut yo\'lmi?:', path.isAbsolute('/folder/subfolder/file.txt')); // Output: true
console.log('Absolyut yo\'lmi?:', path.isAbsolute('folder/subfolder/file.txt')); // Output: false

// u) path.relative() metodining ikki yo'l orasidagi nisbiy yo'lni olish xususiyatini o'rganish
const relativePathExample = path.relative('/folder/subfolder', '/folder/subfolder/file.txt');
console.log('Nisbiy yo\'l:', relativePathExample); // Output: file.txt  

// v) path.sep va path.delimiter xususiyatlarini o'rganish
console.log('Yo\'l ajratuvchisi:', path.sep); // Output: / (Linux/Mac) or \ (Windows)
console.log('Muqobil yo\'l ajratuvchisi:', path.delimiter); // Output: : (Linux/Mac) or ; (Windows)



```
title: 'Node API Tutorial-01- Introduction '
tags: []
categories: []
date: 2017-04-01 05:45:00
---
# بسم الله الرحمن الرحيم

 أول مجموعة دروس سيتم نشرها علي المدونة سنتكلم فيها عن كيفية  برمجة  restful-api  باستخدام  nodejs و express , لكن في مقالاتي هذه لن استخدم mongodb وهو المتبع في أغلب دروس  node لكني سأعمل علي واحدة من SQL Databases وهي PostgreSQL

 لا يتسع المجال هنا للمقارنة بين أنواع قواعد البيانات المختلفة  SQL Vs NoSQL  كذلك إختياري  لـ PostgreSQL ماهو إلا تفضيل شخصي ولكن يمكنك إستخدام  MySQL أو حتي SQlite3 , أو أي قاعدة بيانات مدعومة من مكتبة Knex وهي اللتي وقع عليها إختياري لبساطتها و في نفس الوقت إمكانياتها المتقدمة
تجربة english 


# 1- إنشاء ملف packages.json وتثبيت متطلبات المشروع
 أول شئ نقوم بعمل مجلد جديد للمشروع وليكن بإسم `api-demo` ومن داخله يتم إنشاء ملف `packages.json` ولاحظ أننا غيرنا إسم الملف الافتراضي من `index.js` إلي `server.js`

~~~bash
ahmed ~ [06:03:55]
$ cd api-demo/
ahmed ~/api-demo [06:03:57]
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (api-demo)
version: (1.0.0)
description: create restful api with nodejs
entry point: (index.js) server.js
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to /home/ahmed/api-demo/package.json:

{
  "name": "api-demo",
  "version": "1.0.0",
  "description": "create restful api with nodejs",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this ok? (yes) yes
ahmed ~/api-demo [06:04:32]
$
~~~

الخطوة التالية هي تثبيت الـ packages اللازمة لبرمجة سيرفر nodejs


~~~bash
npm install --save nodemon express  morgan 
~~~

1- الموديول nodemon يستخدم لتشغيل السيرفر بدلا من node بحيث يتابع  أي تغيير في الملفات ويعيد تشغيل السيرفر تلقائيا مما يسرع من عملية التطوير 
2- الموديول express هو web framework لبناء تطبيقات الويب بـ nodejs
3- الموديول morgan  يضيف logs مفيدة جدا لـ express , توضح لك أي request يستقبله السيرفر هكذا

~~~bash
GET / 200 4959.142 ms - 197
GET /stylesheets/style.css 200 50.222 ms - 111
Error
GET /favicon.ico 404 567.070 ms - 1121
Error
GET /user 404 25.021 ms - 1121
GET /stylesheets/style.css 304 3.451 ms - -
GET /users 200 19.906 ms - 23
~~~

ننشئ ملف جافاسكربت جديد في نفس المجلد بإسم server.js وليكن محتواه كالتالي

~~~javascript
const express = require('express');
const logger = require('morgan');

// Initializing the App
const app = express();

app.use(logger('dev'));

// Routes
app.get('/', (req, res)=>{
  res.json({"success": true, 'message': 'Welcome to express server'});
});

// Starting the server
app.listen(3000, ()=>{
  console.log("Server is running at http://127.0.0.1:3000")
})
~~~

هذا السيرفر يتضمن route واحد فقط وهو الرئيسي / ويكون الرد برسالة ترحيب

أخيرا نعدل ملف packages.json عن طريق إضافة start script لتشغيل السيرفر

~~~javascript
{
  "name": "api-demo",
  "version": "1.0.0",
  "description": "create restful api with nodejs",
  "main": "server.js",
  "scripts": {
    "start": "nodemon server.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
~~~

ثم نقوم بتشغيل السيرفر 

~~~bash
npm start
~~~

يمكنك الآن فتح المتصفح علي العنوان  http://127.0.0.1:3000 لتري النتيجة

{% asset_img "img/basic_server.png"  Basic Node Server %}

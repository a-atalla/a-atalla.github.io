---
title:  "Node API Tutorial-01- Introduction "
---
# بسم الله الرحمن الرحيم

 أول مجموعة دروسة سيتم نشرها علي المدونة سنتكلم فيها عن كيفية  برمجة  restful-api  باستخدام  nodejs و express , لكن في مقالاتي هذه لن استخدم mongodb وهو المتبع في أغلب دروس  node لكني سأعمل علي واحدة من SQL Databases وهي PostgreSQL

 لا يتسع المجال هنا للمقارنة بين أنواع قواعد البيانات المختلفة  SQL Vs NoSQL  كذلك إختياري  لـ PostgreSQL ماهو إلا تفضيل شخصي ولكن يمكنك إستخدام  MySQL أو حتي SQlite3 , أو أي قاعدة بيانات مدعومة من مكتبة Knex وهي اللتي وقع عليها إختياري لبساطتها و في نفس الوقت إمكانياتها المتقدمة


 كذلك سأستخدم مدير حزم Yarn بدلا من  npm  , يمكنك معرفة كيفية تثبيته من الموقع الخاص به .


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
yarn add nodemon express body-parser morgan express-validator
~~~

ثم ننشئ ملف جافاسكربت جديد في نفس المجلد بإسم server.js وليكن محتواه كالتالي

~~~javascript
const express = require('express');
const logger = require('morgan');
const bodyParser = require('body-parser');
const expressValidator = require('express-validator');

// Initializing the App
const app = express();

app.use(logger('dev'));
app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());
app.use(expressValidator());

// Routes
app.get('/', (req, res)=>{
  res.json({"success": true, 'message': 'Welcome to express server'});
});


// Starting the server
app.listen(3000, ()=>{
  console.log("Server is running at http://127.0.0.1:3000")
})

~~~

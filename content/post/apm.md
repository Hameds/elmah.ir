---
title: "چطور به کمک APM نرم‌افزارهامون رو بهتر کنیم؟"
cover: "/img/apm_dashboard.png"
date: 2019-01-29T22:10:23+03:30
draft: false
---

### داستان چیه؟

نرم‌افزار رو آماده می‌کنیم. براش تست می‌نویسیم، همه چیز مرتبه اما روی سرور اصلی کاربرها از عملکردش راضی نیستند. فکر می‌کنیم منابع سرور کم باشه، منابع رو بیشتر می‌کنیم اما نتیجه خیلی خیره‌کننده نیست. مشکل کجاست؟

ممکنه حدس زده باشید که کجای کد مشکل داره، اما چطور دقیق متوجه بشیم؟ اینجا لازم میشه به استفاده از **APM** فکر کنیم. به کمک APM ها می‌تونیم Performance نرم‌افزارمون رو مانیتور کنیم و میزان در دسترس بودن بخش‌های مختلف رو بسنجیم و کارهای دیگه‌ای که در مجموع به ما این امکان رو میده که ضعف‌های نرم‌افزارمون رو شناسایی و برطرف کنیم.

### APM ها چه قابلیت‌هایی دارند؟

این خیلی بستگی داره به نرم‌افزاری که استفاده می‌کنید. بعضی از APM ها همه این ویژگی‌ها رو دارند و بعضی بخشی از اون‌ها رو ولی به طور کلی می‌تونید این نوع امکانات رو در APM ها ببینید:

{{< img src="/img/apm_dashboard.png" title="نمونه‌ای از یک داشبورد APM" >}}

- بررسی بخش‌های کند نرم‌افزار اعم از کوئری‌های SQL یا درخواست‌های http یا مشکلات در Redis
- مشخص کردن Request های پربازدید و میزان زمان Response به اون‌ها
- پشتیبانی برای مانیتور ابزارهای مختلف اعم از سرویس‌های cloud یا دیتابیس‌های مختلف
- مانیتور وضعیت ابزارهای مختلف در stack شما 
- مانیتور کردن وضعیت منابع سرور مثل CPU, Memory, Network یا زمان uptime سرور
- مشاهده مجتمع لاگ‌های نرم‌افزارهای مختلف
- دیدن وضعیت شاخص‌های مختلف کارآیی که به صورت دلخواه هم می‌شه تعریفشون کرد
- امکان ارسال نوتیفیکیشن برای رویدادهای خاص مثلاً وقتی سرویسی قطع می‌شه ایمیل بفرسته
- امکان یکپارچه شدن با نرم‌افزارهای Bug Tracker برای گزارش خطاها

موارد دیگری هم ممکنه باشه،‌ اما مهمترین و کاربردی‌ترین قابلیت‌های APM ها این‌ها هستند. نکته دیگه‌ای که هست اینه که ممکنه همه این قابلیت‌ها رو توسط یک نرم‌افزار نتونید داشته باشید مثلاً ممکنه برای Alerting یا ارسال نوتیفیکیشن‌ها از یک نرم‌افزار مجزا استفاده بشه. 

### چطور APM مناسب پیدا کنیم؟

بر خلاف اون چیزی که ممکنه به نظرتون بیاد، بازار APM ها شلوغه و محصولات زیادی هستند. اما چطور یک APM مناسب پیدا کنیم؟

من مدتیه دنبال پیدا کردن راهکار APM هستم، اما نمی‌خوام برای پیدا کردن این راهکار، همه نرم‌افزارها رو با هم تست کنم. دوستانی زحمت کشیدند و سایت ساختند که ابزارهای مختلف که در حوزه APM به کار میان رو لیست کرده اما نکته جالب این لیست اینه که سازگاری هر کدام رو هم بهتون میگه. مثلاً اگر شما برای Agent جمع‌آوری اطلاعات از یک نرم‌افزار استفاده می‌کنید برای Dashboard از چه نرم‌افزاری می‌تونید استفاده کنید.
این دسته‌بندی‌ها در لیست APM‌ها وجود داره:

- Agent
- Libraries
- Collector
- Pipeline
- Storage
- Visualization
- Dashboarding
- Alerting

پروژه تحت نام Open APM اینجاست: [https://openapm.io/landscape](https://openapm.io/landscape) 
اصل پروژه هم روی [گیت‌هاب قرار داره](https://github.com/openapm) و مرتب با ابزارهای جدید بروز می‌شه.

من هنوز به راهکار نهایی نرسیدم اما به محض اینکه استفاده از ابزاری رو شروع کردم شما رو در جریان پیشرفت کار قرار خواهم داد.
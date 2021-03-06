---
title: "آیا کدهای شما به کامنت نیاز دارند؟"
cover: "/img/comment-c.jpg"
date: 2019-03-28T19:02:50+04:30
draft: false
---

تا به حال شده کامنت‌های یک کد دیگر را بخوانید و به این فکر کنید که اصلاً چرا نوشته شدند؟ بعضی معتقدند کدها نیاز به کامنت ندارند و باید آنقدر خوانا باشند که بدون توضیحات اضافه بتوان آن‌ها را فهمید. اما آیا همیشه امکان‌پذیر است؟

### کامنت‌های بد

یکی از رایج‌ترین نوع کامنت‌های بد، کامنت‌هایی هستند که یک موضوع واضح را توضیح می‌دهند. تصور کنید نام یک متغیر `productPrice` باشد. حالا اگر کامنتی ببینید که توضیح داده _قیمت محصول_ به خوانایی کد چیزی اضافه نشده. در حقیقت این کامنت چیزی که از روی اسم متغیر می‌شد حدس زد را تایید کرده است. اگر انتخاب نام متدها و متغیرها و کلاس‌ها را به خوبی انجام دهیم عملاً نیازی به این مدل از کامنت‌ها نخواهد بود.

{{< img src="/img/comment-c.jpg" title="مستندسازی برای رفع تکلیف، کمکی نمی‌کند!" >}}

یک مثال دیگر از کامنت‌های بد، کامنت‌های غیر مرتبط به برنامه هستند. مثلاً اینکه چه کسی روی این فایل کار کرده است یا در چه زمانی این فایل تغییر داده شده است. اطلاعاتی که با استفاده از یک نرم‌افزار Source Control به راحتی و خیلی غنی‌تر می‌توان دریافتشان کرد.

به صورت کلی پیشنهاد می‌شود به جای کامنت نوشتن برای توضیح یک کد بد، کد را بهتر و خواناتر کنیم تا نیازی به این شکل از کامنت نباشد.

### پس چه زمانی کامنت بنویسیم؟

هر زمان می‌خواهید **چرایی** انتخاب یک روش را توضیح دهید باید از کامنت استفاده کنید. چند سناریو زیر را در نظر بگیرید:

- کتابخانه‌ای که از آن استفاده می‌کنید باگی دارد. مشکل را جستجو می‌کنید و به ترفندی برای دور زدن خطا می‌رسید.
- برای اجرای یک کار، چند راه مختلف وجود دارد اما شما به دلایل فنی مجبور به استفاده از یک روش خاص هستید.
- برای اینکه بتوان از داده‌ها در نرم‌افزار دیگری استفاده شود، یک ماژول برای ایجاد فایل اکسل می‌نویسید. اما روی داده‌ها پردازش خاصی انجام می‌دهید تا منطبق بر نیاز ورودی نرم‌افزارهای هدف باشد.

برای همه موارد بالا، نوشتن کامنت ضرورت دارد. چون [کد به شما می‌گوید «چگونه» و کامنت به شما خواهد گفت «چرا»](https://blog.codinghorror.com/code-tells-you-how-comments-tell-you-why/) و موارد بالا از موقعیت‌هایی هستند که باید **چرا** را توضیح دهیم.

### نکته کنکوری

یکی از مثال‌های کامنت‌های بد که اشاره کردم نوشتن کامنت برای توضیح دادن موارد واضح بود، اما گاهی وقت‌ها لازم می‌شود این کار را انجام دهیم. آن هم زمانی است که از روی این کامنت‌ها، مستندات اتوماتیک ایجاد می‌شود به عنوان مثال توضیحات مربوط به مدل‌ها و متدهای APIها که قرار است با swagger نمایش داده شوند.

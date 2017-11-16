---
 title: "بچه‌ها، Glimpse. Glimpse، بچه‌ها!" 
 date: 2013-08-11T22:35:39+03:30
 draft: false 
 categories: ["Software Development"]
 cover: "/oldimg/glimpse2.png"
---



این نوشته یک مطلب کوتاه تخصصی در معرفی [Glimpse](http://getglimpse.com/) برای ASP.NET MVC است. در نوشته‌های دیگری درباره استفاده‌های glimpse بیشتر صحبت خواهم کرد.



### Glimpse چیست؟



به زبان خیلی ساده Glimpse یک چارچوب diagnostic‌ تحت وب است. رایگان و اپن سورس است و خیلی خوب با ASP.NET MVC کار می‌کند، البته نسخه‌هایی از آن برای [PHP](https://github.com/Glimpse/Glimpse.PHP) و [Python](https://github.com/Glimpse/Glimpse.WSGI) نیز وجود دارد. به کمک Glimpse می‌توانید ببینید برای صفحه جاری چه اتفاقاتی در سمت سرور رخ می‌دهد، مثلاً اطلاعاتی در مورد زمان اجرا، تنظیمات سرور، داده‌های request و ... را می‌توانید مشاهده کنید. Glimpse مشابه Firebug روی مرورگر اجرا می‌شود.


{{< img src="/oldimg/glimpse1.png" title="در روایاتی از علمای دات نت آمده برنامه‌نویسی ASP.NET MVC که از glimpse استفاده نکند، بیشتر عمرشان بر فناست!" >}}










### چطور Glimpse را به پروژه ASP.NET MVC خودم اضافه کنم؟



خیلی ساده، بسته nuget آن را دریافت کنید، برای این کار در پنجره Package Manager Console بنویسید:


`Install-Package Glimpse.Mvc4`



با اجرای دستور فوق، کتابخانه‌های مربوط به Glimpse به پروژه شما اضافه شده و خود Glimpse تغییراتی هم در web.config‌ پروژه شما می‌دهد. اگر در نصب glimpse به مشکلی برخورد کردید [این راهنمای نصب](http://getglimpse.com/Help/Installation) را مطالعه کنید.



بعد از نصب Glimpse‌ نوبت فعال کردن آن است. پروژه خودتان را run کنید و در انتهای آدرس آن عبارت Glimpse.axd را اضافه کنید تا آدرس شما به صورت زیر درآید: `http://your-application-url/Glimpse.axd` که به جای your-application-url آدرس برنامه ASP.NET MVC ای شما قرار می‌گیرد. با رفتن به این آدرس صفحه‌ای مطابق شکل زیر ظاهر می‌شود. در این صفحه روی دکمه Turn Glimpse On کلیک کنید تا glimpse برای وب اپلکیشن شما فعال شود.



![](/oldimg/glimpse2.png)



بعد از فعال کردن glimpse به هر صفحه‌ای در برنامه‌تان که بروید یک نوار در بخش پایین صفحه ظاهر می‌شود که اطلاعات مختصری درباره آن صفحه و سرعت لود و تعداد درخواست‌های ajax آن صفحه را به شما نشان می‌دهد. این نوار، مربوط به glimpse است و با کلیک بر روی آن می‌توانید جزئیات بیشتری را مشاهده کنید.



![](/oldimg/glimpse3.png)



### خب من یک سری عدد درباره سرعت لود صفحه دیدم، همین بود؟



خیر، می‌توانید پلاگین‌های مختلف را به Glimpse اضافه کنید. مثلاً اگر [پلاگین Entity Framework](https://www.nuget.org/packages/Glimpse.EF5/1.3.1) را اضافه کنید، می‌توانید در tab های Glimpse کد SQL تولید شده برای نمایش دیتا مدل صفحه را ببینید! به همراه زمانی که برای دریافت اطلاعات صرف شده است.



لیستی از پلاگین‌های مختلف Glimpse‌ را در [این آدرس](http://getglimpse.com/Packages) می‌توانید مشاهده کنید. در نوشته دیگری به موضوع نوشتن پلاگین برای glimpse خواهم پرداخت.


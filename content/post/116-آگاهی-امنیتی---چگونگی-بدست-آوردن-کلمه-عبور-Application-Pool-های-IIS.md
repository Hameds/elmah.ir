---
 title: "آگاهی امنیتی : چگونگی بدست آوردن کلمه عبور Application Pool های IIS" 
 date: 2015-04-07T00:00:00+03:30
 draft: false 
 categories: ["SharePoint Development"]
 cover: "/img/iis_applicaitonpool.png"
---



این نوشته را در دسته‌بندی برنامه‌نویسی شیرپوینت قرار دادم چرا که بیشترین زمانی که با Application Pool ها سر و کار داشتم زمان نصب و تنظیم شیرپوینت بوده است.



کد اصلی مربوط به نوشته آقای Sahil Malik[ است](http://blah.winsmarts.com/2014-5-Find_an_Application_Pool-and-rsquo;s_password.aspx). در شیرپوینت ۲۰۰۷ می‌توانستیم با استفاده از SPApplicationPool.Password کلمه عبور Application Pool را بدست آوریم که در نسخه‌های بعدی دیگر استفاده نمی‌شود. برنامه‌ای به نام appcmd در آدرس c:\windows\system32\inetsrv وجود دارد که با استفاده از دستور زیر کلمه عبور Application Pool را به شما نمایش می‌دهد. کافی است به جای Your\_ApplicationPool\_Name نام ApplicationPool‌ مورد نظر را قرار دهید.



`appcmd.exe list apppool "Your_ApplicationPool_Name" /text:ProcessModel.Password`



پی نوشت: دستور بالا کلمه عبور را به صورت plain text نمایش می‌دهد. مایکروسافت جهت تنظیم Application Pool ‌های شیرپوینت راهنماهایی دارد. کاری که عموماً به مظور تسریع در نصب و راه‌اندازی در سرورهای توسعه (development) انجام می‌دهیم استفاده از کاربرانی با حداکثر سطح دسترسی در اکتیو دایرکتوری (بعضاً domain admin) است. این کار به هیچ وجه برای محیط‌ مشتری توصیه نمی‌شود.


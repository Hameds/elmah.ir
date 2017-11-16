---
 title: "رفع خطاهای معمول و تکمیل راه‌اندازی Build Server برای TFS 2013" 
 date: 2014-09-19T00:00:00+03:30
 draft: false 
 categories: ["Software Development"]
 cover: "/img/TFS-large.png"
---


### Build به کمک  TFS
 

اگر سری نوشته‌های تست جوئل را دنبال کرده باشید، حتماً درباره اهمیت **build روزانه**[ خوانده‌اید](/post/23-تست-جوئل-قسمت-سوم--build-روزانه/). برای داشتن یک روال build خوب ابتدا باید یک build serer داشته باشید. خوشبختانه TFS به خصوص در نسخه‌های جدید، کار build را برای پروژه‌های تیمی بسیار ساده کرده است. در این نوشته درباره خطاهایی که پس از نصب سرویس build در TFS ممکن است با آن‌ها برخورد داشته باشید و راه حل آن‌ها صحبت می‌کنیم.


در توسعه نرم‌افزار آرایه، ما به صورت گسترده از TFS 2013 استفاده می‌‌کنیم. از میان ویژگی‌های اصلی TFS در حوزه Source Control پیشتر از نرم‌افزار داخلی TFS و به تازگی از Git بر روی TFS استفاده می‌کنیم. در حوزه برنامه‌ریزی کارها، از نسخه سفارشی شده‌‌ای از فرم‌های TFS برای ایجاد و رهگیری وظایف برنامه‌نویسی استفاده می‌کنیم که به زودی از آن خواهیم نوشت. در حوزه build نیز از امکان سرویس build موجود در TFS بهره می‌گیریم. به کمک این سرویس انجام آزمون‌های واحد را نیز در هر build کنترل می‌کنیم. در شش ماه دوم سال ۹۳ همچنین برنامه گسترده‌ای برای استفاده از قابلیت‌های Test (به جز اجرای اتوماتیک آزمون‌ها در هنگام build) و Microsoft Test Manager داریم.



در این نوشته درباره خطاها و هشدارهایی که پس از نصب سرویس build به آن‌ها برخورد کردیم و روش حل آن‌ها می‌نویسیم. لازم به ذکر است پیش‌فرض این نوشته این است که شما TFS و Build Controller و Build Agent مورد نظر را نصب و تنظیم کرده‌اید. build server ما بر روی ویندوز سرور ۲۰۱۲ ایجاد شده است و بر مبنای TFS 2013 می‌باشد.



### رفع خطای WebApplication.Targets



پس از نصب و تنظیم build service نخستین خطایی که به خصوص هنگام build کردن پروژه‌های تحت وب ممکن است به آن برخورد داشته باشید، خطای WebApplication.Targets به شرح زیر است:





`error MSB4019: The imported project “C:\Program Files (x86)\MSBuild\Microsoft\VisualStudio\v12.0\WebApplications\Microsoft.WebApplication.targets” was not found. Confirm that the path in the declaration is correct, and that the file exists on disk.`






برای رفع این خطا، از روی سیستم برنامه‌نویسی که در آن Visual Studio 2013 نصب شده است پوشه موجود در مسیر زیر را به مسیر مشابه در مسیر build server کپی کنید.


`C:\Program Files(x86)\MSBuild\Microsoft\VisualStudio\v12.0`

پیشنهاد آرایه: همان‌طور که در ادامه این نوشته می‌آید، پیشنهاد می‌کنیم بر روی build server خود Visual Studio 2013 را نصب کنید.





### رفع هشدار نصب دات نت فریمورک ۴.۵



یکی دیگر از مواردی که موقع build پروژه‌های تحت وب به آن برخورد می‌کنید، هشدار زیر است.






`warning MSB3644: The reference assemblies for framework “.NETFramework,Version=v4.5″ were not found.`






برای رفع این هشدار همانطور که مشخص است باید دات نت فریمورک ۴.۵ را نصب کنید. البته در حقیقت باید  .NET Framework 4.5.1 SDK را نصب نمایید. برای نصب آن به [صفحه دانلود Windows Software Development Kit (SDK) for Windows 8](http://msdn.microsoft.com/en-US/windows/desktop/hh852363.aspx) بروید و پس از دانلود فایل و اجرای آن SDK اشاره شده را نصب نمایید. البته این SDK برای ویندوز ۸.۱ را هم می‌توانید از این صفحه [دانلود کنید](http://msdn.microsoft.com/en-us/windows/desktop/bg162891). SDK نصب شده برای ویندوز سرور ۲۰۱۲ نیز معتبر است.



### رفع خطای Visual Studio Test Runner



اگر build خود را برای اجرای تست‌ها تنظیم کرده باشید، ممکن است به خطای زیر برخورد کنید.






`TF900547: The directory containing the assemblies for the Visual Studio Test Runner is not valid ''`






برای رفع این خطا دو راه حل وجود دارد. راه ساده‌تر نصب Visual Studio 2013 بر روی سرور build است. این کار مشکل خطای اول اشاره شده در این نوشته را نیز برطرف می‌کند. راه دیگر تغییر template مربوط به گردش کار build برای استفاده از نسخه قدیمی‌تر مربوط به VS 2012 است.



### رفع هشدار عدم شناسایی آزمون‌های NUnit



اگر مثل ما از NUnit برای مبحث آزمون‌ها استفاده می‌کنید، ممکن است علیرغم build موفق با هشدار زیر مواجه شوید.






`No test found. Make sure that installed test discoverers & executors, platform & framework version settings are appropriate and try again.`






برای اینکه پروژه‌های حاوی آزمون‌ها شناسایی شوند، [NUnit Test Adapter for VS2012 and VS2013](https://www.nuget.org/packages/NUnitTestAdapter/) را از طریق nuget به پروژه حاوی آزمون‌های نرم‌افزاری اضافه کنید.



**رفع خطای Timeout برای drop folder**



به دلایل مختلف ممکن است با خطای timeout زیر مواجه شوید.






`Exception Message: The HTTP request timed out after 00:01:40. (type TimeoutException)Exception Stack Trace:    at Microsoft.TeamFoundation.Build.Workflow.Activities.FileContainerDropProvider.EndCopyDirectory(IAsyncResult result)`






یک راه خوب برای برطرف کردن آن، تغییر اندازه timeout است. برای این کار به مسیر زیر بروید و فایل tfsbuildservicehost.exe.config را پیدا کنید.







`C:\Program Files\Microsoft Team Foundation Server 12.0\Tools`



در این فایل کدهای زیر را برای تغییر مقدار زمان timeout اضافه کنید. به عنوان مثال کد زیر زمان ۵ دقیقه را برای این timeout تنظیم می‌کند که زمان مناسبی محسوب می‌شود.

{{< gist hameds 6b55fa33993b3da4265164f92553dcb3 >}}

با اجرای دستورالعمل‌های فوق در آرایه موفق شدیم build روزانه و انواع build های مورد نیاز برای پروژه‌ها را با استفاده از TFS ایجاد کنیم. به زودی درباره استفاده از TFS در حوزه برنامه‌‌ریزی کارها و سفارشی‌کردن آن بر اساس نیاز تیم خواهیم نوشت.


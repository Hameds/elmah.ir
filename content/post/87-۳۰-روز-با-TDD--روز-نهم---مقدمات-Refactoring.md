---
 title: "۳۰ روز با TDD: روز نهم - مقدمات Refactoring" 
 date: 2014-04-29T17:52:36+03:30
 draft: false 
 categories: ["Test Driven Development"]
 cover: "/oldimg/tdd_cycle.jpg"
---




نوشته زبان انگلیسی مربوط به روز نهم را از [این آدرس](http://blogs.telerik.com/james-bender/posts.aspx/13-09-27/30-days-of-tdd-day-nine-refactoring-basics) می‌توانید مطالعه کنید. درباره مفهوم Refactoring در ادامه توضیح خواهم داد.



### زمانی برای بازبینی کد (Code Review)



درنوشته قبلی از این سری نوشته‌ها درباره defect ها [صحبت کردیم](/post/85-۳۰-روز-با-tdd--روز-هشتم--برخورد-با-defect-ها/). آخرین کدی که نوشتیم این بود:

{{< gist hameds 9bb4fa64ff48c56b452de5ced736b2b0 >}}

نقصی که برطرفش کردیم این بود که کاربر می‌توانست یک رشته دو حرفی را به عنوان پارامتر دوم به تابع FindNumberOfOccurences ارسال کند و exception ای از نوع FormatException بگیرد. رفتار مورد انتظار در این شرایط این بود که متد exception از نوع ArgumentException را throw (پرتاب) کند.



راه حل من برای رفع این نقص این بود که خیلی ساده کل بدنه تابع را داخل یک try/catch قرار بدهم و اگر خطایی رخ داد یک ArgumentException را throw کنم. این نیاز مربوط به رفع نقص کد را برآورده می‌کند اما اگر به دنبال کد خوب باشیم نیاز به کار بیشتری دارد و اینجاست که می‌توانیم کمی Refactor انجام بدهیم.



مارتین فولر Refactoring را این‌طور تعریف می‌کند: «... یک تکنیک کنترل‌شده برای بهبود طراحی کد موجود». اساساً Refactoring درباره یافتن راه‌هایی است که کدمان را بهتر کنیم. «بهتر» ممکن است معانی زیادی داشته باشد. بعضی مواقع به این معنی است که کد را تغییر بدهیم تا خوانایی بیشتری داشته باشد. بعضی اوقات به معنی حذف کردن کدها یا logic تکراری است. بعضی اوقات به معنی جدا کردن متدها یا کلاس‌های بزرگ برای مدیریت بهتر آن‌هاست. دلایل زیادی برای Refactor کردن کدها وجود دارد. در نوشته‌های بعدی درباره بعضی از مشکلات مشترک کدها و نحوه برخورد با آن‌ها صحبت خواهم کرد.



TDD به سادگی امکان Refactor را فراهم می‌کند. بدون آزمون‌های واحد من باید نگران تغییر کدهایی بودم که کار می‌کنند. چون از Unit Test ها استفاده می‌کنم می‌توانم تا هر جا که مایل باشم کدهایم را Refactor کنم و تا زمانی که تست‌ها pass می‌شوند، صرفنظر از تغییراتی که در کد دادم، مطمئن هستم که نیازمندی‌ها همچنان رعایت شده‌اند.



موقع Refactor کردن شما تغییرات کوچکی ایجاد کرده و بعد آزمون‌های واحد را اجرا می‌کنید تا مطمئن شوید که به برنامه آسیبی وارد نشده است. تغییرات کوچک باعث می‌شوند اگر به هر دلیل آن تغییرات کار نکردند (در واقع آزمون‌های واحد fail شدند) بتوانیم به سادگی به عقب برگردیم.



در پیاده‌سازی جاری متد FindNumberOfOccurences روشی که برای رفع نقص در نظر گرفتیم احتمالاً بهترین راه نبود. چیزی که در واقع احتمالاً به آن نیاز داریم این است که یک قانون اعتبارسنجی برای تعیین تعداد کاراکترهای پارامتر characterToScanFor داشته باشیم و اگر تعداد کاراکترها برابر یک نبود آنگاه یک exception را throw کنیم. من کد متد FindNumberOfOccurences را برای پیاده‌سازی این روش تغییر می‌دهم:

{{< gist hameds 64ceca1a109dcb456f2ddb9033410405 >}}

به جای اینکه کل بدنه متد را در یک try/catch قرار دهم، طول رشته characterToScanFor را چک می‌کنم. اگر طول رشته برابر یک نبود، آنگاه یک exception از نوع AgurmentException را throw می‌کنم. در مقایسه با روش قبل این روش بسیار بهتری است («کار کردن بر حسب تصادف» یکی از مشکلات کد است که در نوشته‌های بعدی درباره‌اش توضیح خواهم داد) این روش همچنین باعث می‌شود که نقایص احتمالی که به قانون اعتبارسنجی (همان قانون یک کاراکتری بودن پارامتر دوم) مرتبط نیستند فراموش نشوند. در هر حال این روش بهتری است اما آیا درست کار می‌کند. راه فهمیدن این موضوع اجرا کردن آزمون‌های واحد است.



![](/oldimg/TDD/9/image_thumb1C38E05DC5B75.png)



چون unit test ها هنوز هم pass می‌شوند، متوجه می‌شویم که صرفنظر از تغییری که در کد دادیم، برنامه و منطق تجاری آن هنوز کار می‌کند. ممکن است defect ها یا نیازمندی‌های دیگری در آینده به وجود آیند اما در حال حاضر کد ما تمام نیازمندهای تجاری برنامه را پوشش می‌دهد.



Refactoring یک گام مهم در TDD است. در TDD شما معمولاً عبارت "Red,Green,Refactor" را می‌شنوید. Red اشاره به این ایده دارد که تستی را می‌نویسیم و fail شدنش را برای اولین بار می‌بینیم. به محض اینکه کد لازم برای pass کردن تست نوشته شد ما به بخش Green در چرخه کاری TDD می‌رسیم. Refactoring آخرین مرحله است: بهتر کردن کد به صورت مداوم برای اینکه خواناتر و بهینه‌تر و انعطاف‌پذیرتر باشد.



ادامه دارد...


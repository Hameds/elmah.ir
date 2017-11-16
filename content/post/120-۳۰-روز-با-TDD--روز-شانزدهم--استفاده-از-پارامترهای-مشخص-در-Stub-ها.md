---
 title: "۳۰ روز با TDD: روز شانزدهم- استفاده از پارامترهای مشخص در Stub ها" 
 date: 2015-12-14T00:00:00+03:30
 draft: false 
 categories: ["Test Driven Development"]
 cover: "/oldimg/tdd_cycle.jpg"
---
ما مثال چند نوشته قبلی این سری نوشته‌ها را پی خواهیم گرفت. نیازمندی نرم‌افزاری را در [روز دوازدهم](/post/107-۳۰-روز-با-tdd--روز-دوازدهم---کار-با-stub-ها/) از Stub بیان کردیم. به عنوان بخشی از این نیازمندی، ما باید با یک سیستم ثبت سفارش خارجی ارتباط برقرار کنیم. تست کیس بعدی که می‌خواهم به آن بپردازم مربوط به همین ارتباط با سیستم خارجی ثبت سفارش است. به جای اینکه خودمان بخش ثبت سفارش را بنویسیم، مدیریت تصمیم گرفته که آن را برون‌سپاری (outsource) کنیم. این تصمیم به آن معنی است که برای بخش ثبت سفارش باید با یک وب سرویس خارج از نرم‌افزار اصلی ارتباط برقرار کنیم. همچنین برای این ارتباط باید بخشی از اطلاعات مشتری (حداقل نام و آدرس) را آماده کنیم.



برای ارائه اطلاعات مشتری (اعم از نام و آدرس) CustomerService می‌بایست تغییر کند.


{{< gist hameds 2551998cd8b80242bded70b1e9fd0a42 >}}

سپس به یک Interface برای Customer Service نیاز داریم

{{< gist hameds 9a6db0a5779c72288e63c7cab6539968>}}

هم تعریف Entity و هم Interface مربوط به Customer Service را به پروژه TddStore.Core اضافه می‌کنیم.



در این قسمت باید از اولین تست کیس مربوط به تعامل با OrderFulfillment Service صحبت کنم که جالب است بدانید هیچ ارتباطی با خود OrderFulfillment ندارد! در این مورد می‌خواهم مطمئن شوم که OrderService به درستی از CustomerService استفاده می‌کند.



صورت مساله تست: وقتی یک مشتری معتبر سفارشی را ثبت می‌کند (که اعتبارسنجی آن انجام شده) این سفارش ثبت شده و یک شناسه سفارش برگردانده می‌شود

به یک تست جدید نیاز دارم:


{{< gist hameds 53af128f910502dd5aff1ccc60426f6d >}}

بلی! این شبیه شروع تست WhenUserPlacesACorrectOrderThenAnOrderNumberShouldBeReturned  به نظر می‌رسد و خیر! نباید WhenUserPlacesACorrectOrderThenAnOrderNumberShouldBeReturned را تغییر دهیم که در کنار تست اصلی، تعامل با CustomService را نیز تست کند.



هدف تست اصلی این است که تعامل با OrderDataSevice به درستی کار می‌کند. جزئیات این تعامل بسته به اینکه متد چطور با CustomerService کار می‌کند ممکن است متفاوت باشد. با تکامل این تست‌ها، نیاز به mock‌های بیشتر OrderDataService حس می‌شود. این باعث می‌شود که هر دو تعامل (از OrderService به OrderDataService و از OrderService به CustomerService) تقریباً مستقل از هم تغییر کنند که باعث تولید تست‌های شکننده کمتری می‌شود. همچنین با استفاده از این روش، چنانچه تستی fail شود دقیقاً خواهم دانست که آیا ارتباط بین OrderDataService و CustomerService باعث این fail شده یا خیر.



قبل از اینکه جلوتر برویم، لازم است وهله (instance) از mock مربوط به CustomerService را در کلاس OrderServiceTests معرفی کنم. همچنین باید از SetupTestFixture نیز استفاده کنم.


{{< gist hameds 9ac4961d45cbbee46d7df92455ad810b >}}

می‌دانم که برای نیازمندی مطرح شده در OrderFultillment باید مشتری را از CustomerService بازیابی (retrieve) کنم. در حال حاضر mock مربوط به CustomerService را تعریف کرده‌ام، پس حالا باید arrange انجام شود. در این مورد می‌خواهم stub من یک مشتری مشخص را وقتی که GetCustomer با پارامتر خاصی فراخوانی می‌شود برگرداند.


{{< gist hameds 4b2a8a57688e2f0210f90ad0d889e0a6 >}}


در ایجاد شی customerToReturn من شی Customer را با Id و نام و نام خانوادگی پر کردم. از نظر فنی در حال حاضر نیازی به نام و نام خانوادگی در این شی ندارم، اما می‌خواهم تا جای ممکن فیلدهای بیشتری را برای تست پر کنم. حالا که ورودی و خروجی تعریف شده‌اند، می‌توانم stub را arrange کنم. در این مورد فقط می‌خوام تا stub مربوط به CustomerService مقدار cutsomterToReturn را وقتی که GetCustomer با پارامتر CustomerId فراخوانی می‌شود برگرداند. همچنین انتظار دارم این متد تنها یک بار فراخوانی شود

{{< gist hameds 37898dd20a015f5daf83c902b501d46d >}}

در پایان لازم است فراخوانی صحیح mock جدید را با assert چک کنم. این کار را با فراخوانی Mock.Assert و پاس دادن mock مربوط به CustomerService می‌توانم انجام بدهم.


{{< gist hameds c7ef02374018b2160a050a1c92b4af2e >}}

همانطور که انتظار داریم تست هنگام اجرا fail می‌شود







![](/oldimg/image_thumb10f068238bf23-png.png)

کد stub‌ مربوط به CustomerService من فراخوانی نشده. باید به متد PlaceOrder در کلاس OrderService بروم و منطق فراخوانی CustomerService را پیاده سازی کنم.


{{< gist hameds 692b7c41f82a6ad1f2cb9486851ae3d5 >}}

در این قسمت نمی‌توانم کدم را اجرا کنم چون کامپایل نمی‌شود. ارجاع (reference) به CustomerService در کلاس OrderService ندارم. پس گام بعدی تغییر OrderService برای پذیرش ICustomerService به عنوان یک وابستگی است که از طریق سازنده (constructor) آن را تزریق می‌کنم (برای این تغییر کد راحت‌تر باشد متد PlaceOrder را از نمونه کد زیر برداشتم)



{{< gist hameds 6e031a2d866c0666b4b3966798a1fe8d >}}

اجرای مجدد تست‌ها نشان می‌دهد که کد همچنان کامپایل نمی‌شود. دلیلش این است که در متد SetupTestFixture کلاس OrderServiceTests تلاش می‌کنیم وهله (instance) از OrderService بدون پاس دادن ICustomerService به سازنده (constrcutor) کلاس بسازیم. برای این کار متد را برای تامین mock در سازنده OrderService تغییر دادم (برای مشاهده راحت‌تر تغییر کد، using ها و متدهای تست را از کلاس برداشتم)

{{< gist hameds 357e6bd138c9c50c9e078e07d936ba43 >}}

حالا تست آماده اجراست و همانطور که در تصویر زیر مشخص است، pass می‌شود.



![](/oldimg/image_thumb3d3df4781c285-png.png)

چیزی که ممکن است سوال کنید این است که چرا مشابه تست اصلی، نتیجه فراخوانی PlaceOrder را دریافت و آزمایش نکردیم. دلیلش این است که در این تست، ما اهمیتی به شماره سفارش نمی‌دهیم و فقط تعامل با CustomerService را مورد آزمایش قرار می‌دهیم.





ادامه دارد....


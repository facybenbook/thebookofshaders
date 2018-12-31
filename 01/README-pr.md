<div dir="rtl"> <h1> مقدمه </h1> </div> 
<div dir="rtl"> <b> فرگمنت شیدر چیست؟ </b> </div> 


<div dir="rtl"> در فصل قبل ما شیدرها را به عنوان معادل دستگاه چاپ گوتنبرگ برای گرافیک معرفی کردیم. چرا؟ و از همه چیز مهمتر شیدر چیست؟ </div> 

![From Letter-by-Letter, Right: William Blades (1891). To Page-by-page, Left: Rolt-Wheeler (1920).](print.png)

<div dir="rtl"> اگر شما تجربه نقاشی با کامپیوتر را دارید.می‌دانید که در این فرایند شما یک دایره، سپس یک مستطیل، یک خط، چندتا مثلث را تا زمانی رسم می کنید تا تصویری که می خواهید ایجاد کنید. این فرایند بسیار شبیه به نوشتن یک نامه یا یک کتاب دستی است که شامل مجموعه دستورالعمل‌هایی است که یک کار را بعد از دیگری انجام می‌دهند. </div> 


<div dir="rtl"> شیدرها مجموعه‌ای از دستورالعمل‌ها هستند با این تفاوت که دستورالعمل‌ها برای هر پیکسل صفحه نمایش به طور همزمان اجرا می شوند.این بدین معنی است که کدی که نوشته‌اید، بسته به موقعیت پیکسل بر روی صفحه نمایش باید به طور متفاوتی رفتار کند؛ مانند قالب پرسی متون)که در گذشته استفاده می‌شد (برنامه شما همانند یک تابع که یک موقعیت را دریافت کرده و یک رنگ را بر می‌گرداند کار می‌کند و وقتی آن کامپایل می شود این کار فوق‌العاده سریع انجام خواهد شد. </div> 


![Chinese movable type](typepress.jpg)

<div dir="rtl"> <h1> چرا شیدر‌ها سریع هستند؟ </h1> </div> 


<div dir="rtl"> برای پاسخ دادن به این سوال، بهتر است شگفتی‌های پردازش موازی را با ذکر یک مثال بررسی کنیم: تصور کنید CPU کامپیوتر شما به عنوان یک لوله صنعتی بزرگ و هر کار به عنوان چیزی است که از آن عبور می‌کند - درست مثل یک خط لوله. </div> 
<div dir="rtl"> برخی از وظایف بزرگ‌تر از دیگر وظایف هستند، به این معنی که آن‌ها نیاز به زمان و انرژی بیشتر برای مقابله با آن را دارند. بهتر است بگوییم که آن کار ها نیاز به قدرت پردازش بیشتری دارند. </div> 
<div dir="rtl"> به دلیل معماری کامپیوترها، هر یک از کارها باید یک بار در یک زمان انجام شود. کامپیوترهای مدرن معمولا دارای گروهی از چهار پردازنده هستند که مانند این لوله‌ها کار می‌کنند. تکمیل وظایف یکی پس از دیگری، برای روان نگه داشتن هر چیزی که در حال اجرا است کاربرد دارد. هر لوله به عنوان یک Thread شناخته شده است. </div> 


![CPU](00.jpeg)

<div dir="rtl">  بازی‌های ویدئویی و سایر برنامه‌های گرافیکی نیاز به قدرت پردازش بیش از برنامه‌های دیگر دارند و به دلیل محتوای گرافیکی، آنها باید تعداد زیادی از عملیات Pixel-by-Pixel را انجام دهند. هر پیکسل روی صفحه نمایش باید محاسبه شود و در بازی‌های سه‌بعدی، شکل‌های هندسی و پرسپکتیو نیاز به محاسبه دارند. </div> 
<div dir="rtl"> بیایید به استعاره لوله‌ها و وظایف‌مان بازگردیم. هر پیکسل روی صفحه‌نمایش نشان‌دهنده‌ی یک کار ساده است. به طور جداگانه هر یک از کارهای پیکسل مسئله ای برای CPU نیست، اما (اینجا مشکل است) کار کوچک باید به هر پیکسل روی صفحه اعمال شود! </div> 
<div dir="rtl"> این بدان معنی است که در صفحه نمایش 800x600 قدیمی، 480،000 پیکسل باید در هر فریم پردازش شود که به معنی 14،400،000 محاسبات در ثانیه است. بله این مسئله به اندازه‌ای بزرگ است که میکروپروسسور را بیش از حد بارگذاری می‌کند. در یک صفحه نمایش شبکیه 2880x1800 مدرن که در محدوده 60 فریم در ثانیه اجرا می‌شود، محسابات تا 311،040،000 در ثانیه افزایش پیدا می‌کند. مهندسان گرافیک چگونه این مشکل را حل کردند؟ </div> 


![](03.jpeg)

This is when parallel processing becomes a good solution. Instead of having a couple of big and powerful microprocessors, or *pipes*, it is smarter to have lots of tiny microprocessors running in parallel at the same time. That’s what a Graphic Processor Unit (GPU) is.

![GPU](04.jpeg)

Picture the tiny microprocessors as a table of pipes, and the data of each pixel as a ping pong ball. 14,400,000 ping pong balls a second can obstruct almost any pipe. But a table of 800x600 tiny pipes receiving 30 waves of 480,000 pixels a second can be handled smoothly. This works the same at higher resolutions - the more parallel hardware you have, the bigger the stream it can manage.

Another “super power” of the GPU is special math functions accelerated via hardware, so complicated math operations are resolved directly by the microchips instead of by software. That means extra fast trigonometrical and matrix operations - as fast as electricity can go.

## What is GLSL?

GLSL stands for openGL Shading Language, which is the specific standard of shader programs you'll see in the following chapters. There are other types of shaders depending on hardware and Operating Systems. Here we will work with the openGL specs regulated by [Khronos Group](https://www.khronos.org/opengl/). Understanding the history of OpenGL can be helpful for understanding most of its weird conventions, for that I recommend taking a look at: [openglbook.com/chapter-0-preface-what-is-opengl.html](http://openglbook.com/chapter-0-preface-what-is-opengl.html)

## Why are Shaders famously painful?

As Uncle Ben said “with great power comes great responsibility,” and parallel computation follows this rule; the powerful architectural design of the GPU comes with its own constraints and restrictions.

In order to run in parallel every pipe, or thread, has to be independent from every other thread. We say the threads are *blind* to what the rest of the threads are doing. This restriction implies that all data must flow in the same direction. So it’s impossible to check the result of another thread, modify the input data, or pass the outcome of a thread into another thread. Allowing thread-to-thread communications puts the integrity of the data at risk.

Also the GPU keeps the parallel micro-processor (the pipes) constantly busy; as soon as they get free they receive new information to process. It's impossible for a thread to know what it was doing in the previous moment. It could be drawing a button from the UI of the operating system, then rendering a portion of sky in a game, then displaying the text of an email. Each thread is not just **blind** but also **memoryless**. Besides the abstraction required to code a general function that changes the result pixel by pixel depending on its position, the blind and memoryless constraints make shaders not very popular among beginning programmers.

Don't worry! In the following chapters, we will learn step-by-step how to go from simple to advanced shading computations. If you are reading this with a modern browser, you will appreciate playing with the interactive examples. So let's not delay the fun any longer and press *Next >>* to jump into the code!



---
title: تأیید کردن قراردادهای هوشمند
description: نگاهی بر تائید کردن کد قراردادهای هوشمند اتریوم
lang: fa
---

[قراردادهای هوشمند](/developers/docs/smart-contracts/) به گونه ای طراحی شده اند که بی نیاز از اطمینان باشند، به این معنی که کاربرها پیش از برقراری ارتباط با یک کانترکت، نیازی نباشد به شخص یا اشخاص سوم شخص(خواه توسعه دهنده و خواه شرکت ها) اعتماد کنند. به عنوان یکی از نیازمندی های بی نیازی از اعتماد، کاربران و همینطور سایر توسعه دهنده باید بتوانند به راحتی به کدهای قراردادهای هوشمند دسترسی داشته باشند تا عملکرد آنها را بررسی و تائید کنند. وریفای یا تائید کد قرارداد هوشمند، این اطمینان خاطر را به کاربران و توسعه دهندگان میدهد که کد منتشر شده از قرارداد هوشمند، دقیقاً همان کدی است که در آدرس آن قرارداد بر بستر بلاکچین اتریوم وجود دارد.

نکته مهمی که وجود دارد این است که باید بین تائید کردن کد و [تائید رسمی](/developers/docs/smart-contracts/formal-verification/) تمایز قائل شد. تائید کردن کد، که در ادامه به تفصیل آن را شرح خواهیم داد، به عملیاتی اطلاق میشود که کدهای یک قرارداد هوشمند در یک زبان سطح بالا (مثل سالیدیتی) دقیقاً به همان بایت کد اجرایی قرارداد هوشمند کامپایل شود. ولی تائید رسمی به توضیح صحیح بودن قرارداد هوشمند مطابق با عملکرد مورد انتظار میپردازد. اگرچه در مفاهیمی که در حال صحبت از آن هستیم، وریفای یا تائید کردن قرارداد عموماً به تائید کدها اطلاق میشود.

## تائید کد چیست؟ {#what-is-source-code-verification}

پیش از دیپلوی یک قرارداد هوشمند در [ماشین مجازی اتریوم (EVM)](/developers/docs/evm/)، توسعه دهنده ها کد قرارداد-دستورالعملهای [نوشته شده به زبان سالیدیتی](/developers/docs/smart-contracts/compiling/) یا سایر زبان های سطح بالا- را به بایت کد [کامپایل](/developers/docs/smart-contracts/languages/) می کنند. از آنجایی که EVM توانایی تفسیر دستورات سطح بالا را ندارد، به منظور اجرای منطق قرارداد بر روی EVM، کامپایل کردن کدها به بایت کد(دستورات سطح پایین و قابل درک برای ماشین) ضروری است.

تائید کردن کد به معنای مقایسه ی کد قرارداد هوشمند و بایت کد کامپایل شده ای که در زمان ساخته شدن قرارداد استفاده میشود، و به منظور شناسایی هرگونه تفاوت می باشد. تائید کردن قرارداد هوشمند از این جهت حائز اهمیت است که کد قرارداد تبلیغ شده، ممکن است با آنچه که در حال اجرا بر روی بلاکچین است متفاوت باشد.

تائید قرارداد هوشمند امکان بررسی و تحقیق کاری که قرارداد انجام می دهد را از طریق خواندن کدهای سطح بالا و بدون نیاز به خواندن کدهای ماشین فراهم می سازد. توابع، مقادیر، و عموماً اسامی متغیرها و کامنت ها عیناً مطابق کد اصلی ای هستند که قرارداد با آنها کامپایل و دیپلوی شده است. این موضوع، خواندن کد را بسیار راحت تر می کند. تائید کد، همچنین مستندات کد را فراهم آوری می کند و باعث میشود تا کاربران نهایی بتوانند متوجه شوند که قرارداد هوشمند مربوطه برای چه کاری طراحی شده است.

### تائید کامل چیست؟ {#full-verification}

بخش هایی از قرارداد هوشمند، از جمله کامنت ها یا اسامی متغیرها بر روی بایت کدهای کامپایل شده تاثیری ندارند. این موضوع بدین معناست که دو کد مختلف، با اسامی متغیر و همینطور کامنت های متفاوت، می توانند توسط یک قرارداد یکسان تائید شوند. با استفاده از این مسئله، یک کاربر بداندیش، می تواند با افزودن کامنت های فریبنده و یا نام گذاری گمراه کننده نام متغیرها در کد، کدی متفاوت از کد اصلی را تائید کند.

به منظور جلوگیری از این اتفاق، می توان با افزودن یک داده اضافه به بایت کد که در حکم یک _تضمین رمزنگاری_ و به عنوان _ اثر انگشت_ عملیات کامپایل برای همسان بودن کد می باشد اقدام نمود. اطلاعات ضروری در [داده های متای قرارداد سالیدیتی](https://docs.soliditylang.org/en/v0.8.15/metadata.html) قابل دستیابی است، همچنین هش این فایل نیز به بایت کد قرارداد الحاق میشود. این مورد را می توانید به طور عملیاتی در [فضای بازی داده های متا](https://playground.sourcify.dev) مشاهده کنید

فایل داده های متا یا متادیتا، حاوی اطلاعاتی در خصوص کامپایل شدن قرارداد هوشمند و شامل کدها و هش آنها می باشد. این بدین معناست که در صورت رخ دادن کوچک‌ترین تغییری در تنظیمات کامپایل و یا حتی تغییر در یک بایت از کدها، فایل متادیتا تغییر خواهد کرد. همچنین متعاقباً، هش فایل متادیتا که به بایت کد الحاق شده است نیز تغییر خواهد کرد. این بدین معناست که اگر بایت کد یک قرارداد + هش متادیتای الحاص شده به آن، با کد داده شده و تنظیمات کامپایل یکسان باشد، می توانیم کاملاً مطمئن باشیم که حتی یک بایت نیز تغییری نکرده و این کد، کد اصلی کامپایل شده می باشد.

به این نوع از تائید که از هش متادیتا بهره می برد، اصطلاحاً **[تائید کامل](https://docs.sourcify.dev/docs/full-vs-partial-match/)** (همچنین "تائید بی نقص") گفته می شود. اگر هش های متادیتا یکسان نبوده و یا به عنوان تائید شده نباشند، به آن "تطابق جزئی" گفته می شود، که در حال حاضر رایج ترین شیوه در تائید قراردادهاست. در صورتی که عملیات تائید کردن به صورت کامل نباشد، این امکان وجود دارد که [کد مخربی به قرارداد وارد شود](https://samczsun.com/hiding-in-plain-sight/) که در کد تائید شده قابل مشاهده نباشد. بیشتر توسعه دهنده ها از وجود تائیدیه کامل بی اطلاع اند و فایل متادیتای کامپایل خود را نگهداری نمی کنند، از این رو، عملاً تاکنون تائید جزئی به عنوان روش تائید قراردادها مورد استفاده قرار میگیرد.

## چرا تائید کد مهم است؟ {#importance-of-source-code-verification}

### بی نیازی از اعتماد {#trustlessness}

بدون شک، بی نیازی از اعتماد یکی از بزرگترین وعده های قراردادهای هوشمند و [اپلیکیشن های غیرمتمرکز(dappها)](/developers/docs/dapps/) است. قراردادهای هوشمند "تغییر ناپذیر" بوده و امکان عوض کردن ندارند؛ یک قرارداد، تنها مسئول اجرای منطق کاری است که در زمان دیپلوی شدن، در کدش تعریف شده است. این موضوع به این معناست که توسعه دهنده‌ها و شرکت‌ها(و البته قابل بسط به سایر افراد نیز می باشد)، پس از دیپلوی(استقرار) بر روی شبکه اتریوم، نمیتوانند تغییری در کد قرارداد ایجاد کنند.

به منظور بی نیاز بودن از اعتماد در یک قرارداد هوشمند، کد قرارداد باید جهت تائید شدن به صورت مستقل، قابل دسترس باشد. اگرچه بایت‌کد کامپایل شده ی قراردادهای هوشمند به‌صورت عمومی بر روی بلاکچین قابل دسترسی است، اما درک زبان سطح پایین، هم برای توسعه دهنده ها و هم کاربران عادی سخت است.

به منظور کاهش گمانه زنی ها در خصوص اعتمادپذیری، پروژه ها کد قراردادهای خود را منتشر می کنند. اما همین موضوع، باعث ایجاد یک مشکل دیگر می شود: تائید همسان بودن کد منتشر شده با بایت کدهای قرارداد مربوطه، سخت است. در این سناریو، بدلیل اینکه کاربران باید به توسعه دهنده اعتماد کنند که منطق کاری قرارداد (با تغییر دادن بایت‌کد) را پیش از دیپلوی بر روی بلاکچین تغییر نمیدهد، ارزش بی نیازی از اعتماد، در عمل از بین می رود.

ابزارهای تائید کد، ضمانت می کنند که کد قرارداد هوشمند دقیقاً منطبق بر کد اسمبلی آن قرارداد باشد. نتیجه این امر، پدید آمدن یک اکوسیستم بی نیاز از اعتماد است، جایی که کاربران، چشم و گوش بسته به افراد یا نهادهای سوم شخص اعتماد نکرده و به جای آن، پیش از انجام هرگونه واریز دارایی به یک قرارداد، کدهای آن قرارداد را تائید می کنند.

### امنیت کاربر {#user-safety}

معمولاً هر جا که قراردادهای هوشمند باشند، پول زیادی نیز سپرده گذاری شده است. به همین خاطر پیش از استفاده از قراردادهای هوشمند، نیاز بیشتری به تضمین امنیت و تائید بودن منطق آن قرارداد بوجود می آید. مشکلی که در این‌جا وجود دارد این است که توسعه دهنده های بی اخلاق و شرور، می توانند کاربران را با وارد کردن کدهای مخرب به قرارداد هوشمند، فریب دهند. بدون انجام تائیدیه، قراردادهای هوشمند مخرب میتوانند شامل کدهای مخربی از جمله: [در پشتی](https://www.trustnodes.com/2018/11/10/concerns-rise-over-backdoored-smart-contracts)، مکانیزم‌های کنترل دسترسی ناجور، آسیب‌پذیری‌های قابل سوء استفاده، و سایر مخاطراتی که امنیت کاربر را به خطر می اندازند بوده که این کدها قابل شناسایی نباشند.

انتشار فایل کدهای قرارداد هوشمند، دسترسی به نواحی ای از قرارداد که پتانسیل مورد حمله واقع شدن را دارند را برای علاقه مندانی مثل حسابرسان کد تسهیل می کند. وجود اشخاص مستقل از هم که عملیات تائید قرارداد هوشمند را انجام دهند، تضمینی قوی تر برای امنیت کاربران به حساب می آید.

## نحوه تائید کد قراردادهای هوشمند اتریومی {#source-code-verification-for-ethereum-smart-contracts}

[استقرار قرارداد هوشمند بر روی اتریوم](/developers/docs/smart-contracts/deploying/) نیازمند ارسال یک تراکنش با پی لود حاوی داده(بایت کد کامپایل شده) به یک آدرس خاص است. پی لود داده، با کامپایل شدن کد قرارداد، به علاوه ی [آرگومان‌های کانستراکتور](https://docs.soliditylang.org/en/v0.8.14/contracts.html#constructor) قرارداد که به پی لود داده در تراکنش الحاق شده است ساخته می شود. عملیات کامپایل قطعی است، به این معنا که اگر فایل کدها و تنظیمات کامپایل(از جمله نسخه کامپایلر، اپتیمایز، و ...) یکسان باشند، همیشه یک خروجی یکسان(بایت‌کد قرارداد) ایجاد خواهد شد.

![دیاگرامی که نمایش دهنده کد وریفای شده قرارداد هوشمند میباشد](./source-code-verification.png)

وریفای کردن یک قرارداد هوشمند اساساً شامل مراحل زیر می باشد:

1. وارد کردن فایل کدها و تنظیمات کامپایل به یک کامپایلر.

2. کامپایلر، بایت‌کد قرارداد را به عنوان خروجی بر میگرداند

3. بایت‌کد قرارداد دیپلوی شده در یک آدرس مشخص شده قابل دستیابی است

4. بایت‌کد دیپلوی شده با بایت‌کد حاصله از دیپلوی مجدد مقایسه می شود. در صورت تصاطبق کدها، قرارداد با کد داده شده و تنظیمات کامپایل مشخص شده تائید و وریفای می شود.

5. علاوه بر این، در صورتی که هش داده های اضافی یا همان متا دیتای در انتهای بایت‌کد، منطبق باشند، یک تطابق کامل خواهیم داشت.

توجه داشته باشید که در اینجا توضیح ساده ای از تائید کردن را به میان آورده ایم، و در این پروسه استثناهای بسیاری وجود دارند که ممکن است توضیحات متفاوتی با آنچه که در حال صحبت در اینجا هستیم داشته باشند، مثلاً در زمانی که

متغیرهای از نوع immutable" داشته باشیم.



## ابزارهای وریفای کد {#source-code-verification-tools}

پروسه مرسوم وریفای کردن قراردادها می توانند پیچیده باشند. به همین علت است که ابزارهایی برای وریفای کد قراردادهای هوشمند مستفر شده بر روی اتریوم داریم. این ابزارها به‌طور اتوماتیک بخش های بزرگی از کد را تائید و وریفای کرده و همچنین می توانند کدهای وریفای شده را برای انتفاع کاربرها گلچین کنند.



### Etherscan {#etherscan}

اگرچه اکثراً آنرا به عنوان [مرورگر بلاکچین اتریوم](/developers/docs/data-and-analytics/block-explorers/) می شناسند، اتراسکن همچنین [سرویس تائید کد](https://etherscan.io/verifyContract) برای توسعه دهنده‌های قراردادهای هوشمند و کاربران عادی را ارائه می دهد.

اتراسکن اجازه کامپایل مجدد بایت‌کد قرارداد از پی لود داده اصلی (کد، آدرس کتابخانه، تنظیمات کامپایلر، آدرس قرارداد، و ...) را به شما می دهد در صورتی که بایت‌کد مجدد کامپایل شده، با بایت‌کد (و پارامترهای کانستراکتور) قراردادی بر روی بلاکچین (آن-چین) منطبق باشد، سپس [قرارداد وریفای می شود](https://info.etherscan.com/types-of-contract-verification/).

هنگامی که قرارداد وریفای شود، کد قرارداد شما برچسب "verified" دریافت کرده و به منظور حسابرسی و آدیت شدن سایرین، بر روی اتراسکن منتشر می شود. همچنین به قسمت قراردادهای وریفای شده یا همان verified contracts -که مخزنی از قراردادهای هوشمند با کدهای وریفای شده است- اضافه می شود.

اتر اسکن، پر استفاده ترین ابزار وریفای و تائید قراردادهای هوشمند است. هرچند، سرویس وریفای قراردادهای اتراسکن نواقصی نیز دارد: از جمله این نواقص می توان به ناتوانی در مقایسه **هش متادیتا**ی بایت‌کد آن-چین و بایت‌کد مجدد کامپایل شده اشاره کرد. بنابراین می توان گفت که تطابق‌های اتراسکن از نوع تطابق جزئی است.

[مطالب بیشتر در خصوص وریفای قراردادهای هوشمند در اتراسکن](https://medium.com/etherscan-blog/verifying-contracts-on-etherscan-f995ab772327).



### Sourcify {#sourcify}

ابزار دیگری که متن باز و غیرمتمرکز بوده و برای وریفای قراردادهای هوشمند به کار میرود، [Sourcify](https://sourcify.dev/#/verifier) میباشد. این ابزار، مرورگر بلاک ها نیست و فقط قراردادها را بر روی [انواع شبکه های منطبق بر ماشین مجازی اتریوم](https://docs.sourcify.dev/docs/chains) وریفای می کند. این ابزار به عنوان یک زیرساخت عمومی برای سایر ابزارها عمل می کند، و هدفش این است که ارتباط گیری با قراردادهای هوشمند را با استفاده از [ABI](/developers/docs/smart-contracts/compiling/#web-applications) و کامنت‌های از نوع [NatSpec](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html) که در فایل متادیتا یافت می شود، کاربر پسند تر کند.

بر خلاف اتراسکن، Sourcify از تطابق کامل با هش متادیتا پشتیبانی می کند. قراردادهای تائید شده، در [مخزن عمومی](https://docs.sourcify.dev/docs/repository/) یا HTTP و [IPFS](https://docs.ipfs.io/concepts/what-is-ipfs/#what-is-ipfs) که یک فضای ذخیره‌سازی غیر متمرکز [مبتنی بر آدرس](https://web3.storage/docs/concepts/content-addressing/) است قرار می‌گیرند. از آنجایی که هش متادیتای الحاق شده، یک هش IPFS است، این امر اجازه ی واکشی فایل متادیتای یک قرارداد از بستر IPFS را فراهم می‌آورد.

به علاوه، از آنجایی که هش IPFS این فایل‌ها همچنین در متادیتا نیز یافت می‌شود، هر کسی این امکان را دارد که فایل کد را از طریق IPFS دریافت کند. با فراهم‌سازی فایل متادیتا و فایل کدها از طریق API و یا [رابط کاربری](https://sourcify.dev/#/verifier)، و یا استفاده از پلاگین‌های آن، می توان قرارداد را وریفای کرد. همچنین ابزار مانیتورینگ و رصد Sourcify گوش به زنگ ساخته شدن قراردادها در بلوک‌های جدید بوده و اگر متادیتا و فایل کد قراردادی در IPFS منتشر شده است، سعی می‌کند آنرا وریفای کند.

[مطالب بیشتر در خصوص وریفای قراردادها بر روی Sourcify](https://blog.soliditylang.org/2020/06/25/sourcify-faq/).



### Tenderly {#tenderly}

پلتفرم [Tenderly](https://tenderly.co/) به توسعه‌دهنده‌های وب3 قابلیت ساخت، تست، مانیتور کردن، و اجرای قراردادهای هوشمند را می‌دهد. تندرلی، با مجموعه ای از ابزارهای اشکال‌زدایی، با ابزارهای قابل مشاهده پذیری و زیرساخت ساخته شدن بلوک‌ها، در مسیر توسعه قرارداد هوشمند، به توسعه دهنده ها سرعت می‌بخشد. به منظور بهره‌مندی از تمامی امکانات تندرلی، توسعه‌دهنده‌ها نیاز به [وریفای کردن کدقرارداد](https://docs.tenderly.co/monitoring/contract-verification) دارند.

امکان وریفای عمومی یا خصوصی یک قرارداد وجود دارد. در صورت وریفای به‌صورت خصوصی، قرارداد هوشمند فقط برای شما (و افراد تیم پروژه‌ی شما) قابل مشاهده است. وریفای کردن عمومی قرارداد، آنرا برای تمامی کاربران پلتفرم تندرلی قرار میدهد.

شما می ‌توانید با استفاده از [داشبورد کاربری](https://docs.tenderly.co/monitoring/smart-contract-verification/verifying-a-smart-contract)، [پلاگین هاردهت تندرلی](https://docs.tenderly.co/monitoring/smart-contract-verification/verifying-contracts-using-the-tenderly-hardhat-plugin)، و یا [CLI](https://docs.tenderly.co/monitoring/smart-contract-verification/verifying-contracts-using-cli) قراردادهای خود را وریفای کنید.

در صورتی که قرارداد خود را از طریق داشبورد کاربری وریفای کنید نیاز دارید که فایل کد یا فایل متادیتای ساخته شده توسط کامپایلر سالیدیتی، آدرس/شبکه، و تنظیمات کامپایلر را ایمپورت کنید.

با استفاده از پلاگین هاردهت تندرلی، می توانید دسترسی های بیشتر با سختی کمتری در خلال پروسه وریفای کردن داشته باشید، و این باعث فعال‌سازی امکان انتخاب وریفای بین روش اتوماتیک (بدون کد) و دستی (نیازمند کدنویسی) می‌شود.



## بیشتر بخوانید {#further-reading}

- [وریفای کردن کد منبع قرارداد](https://programtheblockchain.com/posts/2018/01/16/verifying-contract-source-code/)

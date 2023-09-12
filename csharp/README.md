<div dir=rtl>

![messageWay](../assets/logo-fa.png)

# راه‌پیام

این راهنما برای کار با سامانه راه‌پیام (MessageWay) و با استفاده از زبان `C#`نوشته شده است. سعی شده که مثال‌ها کاملا شفاف و ساده باشد تا امکان استفاده از آن‌ها برای افراد مبتدی هم وجود داشته باشد.


## نکات ضروری

> برای ثبت نام در **سامانه راه‌پیام** حساب کاربری شما نیاز به تایید دارد و برای تایید باید تصویر کارت ملی و یا پاسپورت خود را بارگزاری نمایید. تا قبل از تایید حساب کاربری، شما فقط امکان ارسال پیام به شماره‌ای که با آن در سامانه ثبت نام کرده‌اید را دارید.
 
> به دلیل اینکه از ارسال پیامک‌های آزاردهنده برای افراد جلوگیری شود، الگوهایی که ایجاد می‌کنید نیاز به تایید دارند. و تا زمانی که الگو تایید نشده امکان استفاده از آن وجود ندارد و فقط می‌توانید از الگوهای پیشفرض سامانه استفاده کنید.

> امکان ارسال پیامک بین المللی، به همه کشورهای جهان از طریق این سامانه وجود دارد، بصورت کلی اگر شماره موردنظر،‌ با پیش شماره‌ای غیر از ایران باشد، پیامک شما از طریق اپراتورهای بین المللی ارسال می‌شود.

> **توجه! هدف از نوشتن این مستند، نمایش نحوه استفاده از api های سامانه راه پیام است و بهتر است که از کپی کدهای نوشته شده در این مثال‌ها در پروژه‌های تجاری، خودداری کنید.**

---

## مثال‌ها

برای راحتی کار، هر مثال به صورت مستقل نوشته شده است. شما می‌توانید هرآنچه را که در هر مثال مشاهده می‌کنید به صورت کامل کپی کرده و در هاست یا کامپیوتر شخصی خود اجرا کنید.


### ارسال پیامکی  OTP  ![ico-sms]

در این مثال فقط یک کد OTP که توسط خود سامانه راه‌پیام تولید می‌شود را برای شماره موبایل موردنظر و با استفاده از الگوهای پیشفرض سامانه راه پیام، و از طریق پیام کوتاه (SMS) ارسال می‌کنیم.

</div>

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://api.msgway.com/send");
request.Headers.Add("apiKey", "XXXXXXXXXXXXXXXXXXXX");
request.Headers.Add("accept-language", "fa");
var content = new StringContent("{\"mobile\": \"+98935XXXXXXX\",\"method\": \"sms\",\"templateID\": 3}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

---

<div dir=rtl>

### ارسال پیامکی  OTP با کد سفارشی ![ico-sms]

در این مثال کد OTP که خودمون تولیدش کردیم را برای شماره موبایل موردنظر از طریق پیام کوتاه (SMS) ارسال می‌کنیم.

</div>

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://api.msgway.com/send");
request.Headers.Add("apiKey", "XXXXXXXXXXXXXXXXXXXX");
request.Headers.Add("accept-language", "fa");
var content = new StringContent("{\"mobile\": \"+98935XXXXXXX\",\"method\": \"sms\",\"templateID\": 3,\"code\": \"123456\"}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

---
<div dir=rtl>

### ارسال پیامکی  OTP به همراه پارامترهای دیگر ![ico-sms]

در این مثال کد OTP را به همراه یک پارامتر دیگر که در برخی الگو وجود دارد به صورت پیام کوتاه (SMS)  ارسال می‌کنیم. مثلا الگو پیشفرض شماره 6 امکان ارسال 2 پارامتر را دارد. شما می‌توانید تا حداکثر 10 پارامتر را در الگوهای خود درج کنید و هنگام ارسال از آن‌ها استفاده کنید.

</div>

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://api.msgway.com/send");
request.Headers.Add("apiKey", "XXXXXXXXXXXXXXXXXXXX");
request.Headers.Add("accept-language", "fa");
var content = new StringContent("{\"mobile\": \"+98935XXXXXXX\",\"method\": \"sms\",\"templateID\": 6, \"params\":[\"راه پیام\", \"msgway.com\"]}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

---
<div dir=rtl>

### ارسال OTP از طریق تماس صوتی با کد سفارشی ![ico-ivr]

در این مثال کد OTP که خودمون تولیدش کردیم را برای شماره موبایل موردنظر از طریق تماس صوتی (IVR) ارسال می‌کنیم.
* کد `templateID` تماس صوتی (IVR) در حال حاضر فقط `2` می‌باشد و امکان استفاده از فایل صوتی شخصی سازی شده وجود ندارد.

</div>

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://api.msgway.com/send");
request.Headers.Add("apiKey", "XXXXXXXXXXXXXXXXXXXX");
request.Headers.Add("accept-language", "fa");
var content = new StringContent("{\"mobile\": \"+98935XXXXXXX\",\"method\": \"ivr\",\"templateID\": 2,\"code\":\"123456\"}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

---
<div dir=rtl>

### ارسال پیامک با الگوی شخصی ![ico-sms]

برای تعریف الگو شخصی باید وارد سامانه راه‌پیام شده و از طریق منو الگوها، الگو موردنظر خود را درج کنید. به طور مثال من این الگو را تعریف می‌کنم:
> سلام [param1] عزیز،‌ خیلی وقته که به ما سر نزدی!
> 
> کد تخفیف اختصاصی شما: [param2]
> 
> فروشگاه بزرگ راه پیام
> 
> www.msgway.com

*  امکان نوشتن url در پارامترها وجود ندارد و شما باید url موردنظر را داخل متن الگو بنویسید تا بعد از تایید و بررسی امکان ارسالش را داشته باشید.
* بعد از ایجاد الگو،  کد الگو ساخته شده که یک عدد چند رقمی است، به شما نمایش داده می‌شود که می‌توانید آن را در پارامتر `templateID` ارسال کنید. مثلا کد الگویی که من تعریف کردم `12345` می‌باشد.
* شما فقط امکان استفاده از الگوهای پیشفرض سیستم و الگوهای مخصوص به خودتان را دارید و اگر شما کد الگویی که من ساختم را ارسال کنید، سیستم خطا می‌دهد.
* هنگام تعریف الگو، اگر برای استفاده‌ای غیر از کد OTP باشه، لازمه که عبارت `لغو11` به انتهای پیام اضافه کنید. در غیر اینصورت بصورت اتوماتیک توسط سیستم اضافه می‌شود.
</div>

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://api.msgway.com/send");
request.Headers.Add("apiKey", "XXXXXXXXXXXXXXXXXXXX");
request.Headers.Add("accept-language", "fa");
var content = new StringContent("{\"mobile\": \"+98935XXXXXXX\",\"method\": \"sms\",\"templateID\": 12345,\"params\":[\"احسان\",\"xyz123mxb\"]}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

---
<div dir=rtl>

### ارسال OTP از طریق پیام‌رسان گپ ![ico-messenger]

در این مثال کد OTP را برای شماره موبایل موردنظر از طریق پیام‌رسان ایرانی گپ ([Gap Messenger](https://gap.im)) ارسال می‌کنیم.

</div>

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://api.msgway.com/send");
request.Headers.Add("apiKey", "XXXXXXXXXXXXXXXXXXXX");
request.Headers.Add("accept-language", "fa");
var content = new StringContent("{\"mobile\": \"+98935XXXXXXX\",\"method\": \"messenger\",\"templateID\": 10,\"provider\":2, \"code\":\"123456\",\"params\":[\"پارامتر تست\"]}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

---


[ico-sms]: https://img.shields.io/badge/SMS-085400

[ico-ivr]: https://img.shields.io/badge/IVR-0e08bf

[ico-messenger]: https://img.shields.io/badge/MESSENGER-3c0054

[link-messageWay]: https://MSGWay.com/
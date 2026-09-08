# 📘 راهنمای استقرار EdgePanel (فارسی)

پنل انگلیسی **VLESS / Trojan / Shadowsocks** روی Cloudflare Workers یا Pages.

**دموی رابط:**
- ورود: https://shahzad55.github.io/EDT-Pages.github.io/login/
- ادمین: https://shahzad55.github.io/EDT-Pages.github.io/admin/

**کد پروژه:** https://github.com/Shahzad55/edgetunnel

---

## پیش‌نیازها

1. حساب [Cloudflare](https://dash.cloudflare.com) (رایگان کافی است)
2. (اختیاری) یک دامنه که روی Cloudflare باشد
3. حدود ۱۰ دقیقه وقت

---

## روش ۱: Workers (ساده و سریع)

### مرحله ۱ — ساخت Worker

1. وارد [Cloudflare Dashboard](https://dash.cloudflare.com) شو.
2. از منوی سمت چپ **Workers & Pages** را باز کن.
3. **Create application** → **Create Worker** → یک نام بگذار (مثلاً `edgepanel`) → **Deploy**.

### مرحله ۲ — قرار دادن کد

1. روی Worker ساخته‌شده کلیک کن → **Edit code**.
2. همهٔ محتوای پیش‌فرض را پاک کن.
3. محتوای فایل [`_worker.js`](https://raw.githubusercontent.com/Shahzad55/edgetunnel/main/_worker.js) را کپی و پیست کن.
4. **Save and Deploy**.

### مرحله ۳ — رمز ادمین (ADMIN)

1. **Settings** → **Variables and Secrets**.
2. **Add** → نوع **Secret** (یا Variable):
   - Name: `ADMIN`
   - Value: یک رمز قوی (مثلاً `MyPass123!`)
3. **Save** → در صورت نیاز دوباره Deploy.

### مرحله ۴ — اتصال KV

1. از منوی Cloudflare برو به **Storage & Databases** → **KV**.
2. **Create a namespace** → نام مثلاً `edgepanel-kv` → Create.
3. برگرد به Worker → **Settings** → **Bindings** → **Add** → **KV Namespace**:
   - Variable name: `KV`  ← دقیقاً همین کلمه
   - KV namespace: همان namespace که ساختی
4. **Save** و در صورت نیاز Redeploy.

### مرحله ۵ — دامنه (اختیاری ولی توصیه‌شده)

1. Worker → **Settings** → **Domains & Routes** → **Add** → **Custom domain**.
2. زیر‌دامنه‌ای مثل `vless.yourdomain.com` وارد کن (دامنه باید روی Cloudflare باشد).
3. صبر کن تا SSL فعال شود.

### مرحله ۶ — ورود به پنل

آدرس را باز کن:

```
https://آدرس-worker-یا-دامنه‌ات/admin
```

با رمزی که در `ADMIN` گذاشتی وارد شو.

---

## روش ۲: Pages با آپلود ZIP (پیشنهادی)

### مرحله ۱ — دانلود پروژه

از این لینک فایل را دانلود کن:

https://github.com/Shahzad55/edgetunnel/archive/refs/heads/main.zip

### مرحله ۲ — ساخت پروژه Pages

1. Cloudflare → **Workers & Pages** → **Create** → **Pages** → **Upload assets**.
2. نام پروژه را بگذار (مثلاً `edgepanel`).
3. فایل `main.zip` را آپلود کن → **Deploy site**.

### مرحله ۳ — متغیر ADMIN

1. پروژه Pages → **Settings** → **Environment variables**.
2. برای **Production** متغیر اضافه کن:
   - Name: `ADMIN`
   - Value: رمز دلخواه
3. **Save**.

### مرحله ۴ — Deploy دوباره

1. تب **Deployments** → **Create new deployment**.
2. همان zip را دوباره آپلود کن → **Save and Deploy**.

### مرحله ۵ — اتصال KV

1. **Settings** → **Bindings** → **Add** → **KV Namespace**.
2. Variable name: `KV`
3. Namespace را انتخاب یا بساز → **Save**.
4. یک Deploy دیگر بزن تا Binding اعمال شود.

### مرحله ۶ — ورود

```
https://نام-پروژه.pages.dev/admin
```

یا اگر Custom Domain وصل کردی:

```
https://زیر-دامنه‌ات/admin
```

---

## روش ۳: Pages + GitHub

1. ریپوی https://github.com/Shahzad55/edgetunnel را **Fork** کن.
2. Cloudflare Pages → **Connect to Git** → همان Fork را انتخاب کن.
3. در تنظیمات Build، متغیر `ADMIN` را اضافه کن و Deploy بزن.
4. مثل روش قبل، Binding با نام `KV` را وصل کن و Redeploy کن.

---

## متغیرهای مهم

| نام | اجباری | توضیح |
|-----|--------|--------|
| `ADMIN` | ✅ بله | رمز ورود پنل ادمین |
| `UUID` | خیر | UUID ثابت (فرمت v4) |
| `KEY` | خیر | کلید مسیر اشتراک سریع |
| `HOST` | خیر | دامنهٔ نمایش داده‌شده در نود |
| `PATH` | خیر | مسیر نود |
| `PROXYIP` | خیر | آی‌پی/هاست ProxyIP |
| `GO2SOCKS5` | خیر | دامنه‌هایی که از SOCKS5 رد شوند |
| `DEBUG` | خیر | با `1` یا `true` لاگ دیباگ روشن می‌شود |

---

## بعد از ورود به پنل

1. تنظیمات نود (پروتکل، UUID، مسیر و …) را بررسی کن.
2. لینک **Subscription** را کپی کن و در کلاینت (v2rayNG، Streisand، Hiddify، Clash و …) اضافه کن.
3. در صورت نیاز از بخش Preferred / ProxyIP برای بهبود کیفیت استفاده کن.

---

## خطاهای رایج

| مشکل | راه‌حل |
|------|--------|
| صفحه `Admin password not set` | متغیر `ADMIN` را ست نکرده‌ای یا Deploy بعد از آن نزده‌ای |
| صفحه `KV not bound` | Binding با نام دقیق `KV` را وصل کن و Redeploy کن |
| Error 1101 | معمولاً موقتی است؛ چند دقیقه بعد یا با دامنهٔ دیگر امتحان کن |
| پنل هنوز چینی است | Hard Refresh: `Ctrl+Shift+R` — Worker باید به UI انگلیسی اشاره کند |
| اشتراک کار نمی‌کند | UUID و دامنه را در پنل چک کن؛ کلاینت را به‌روز کن |

---

## کلاینت‌های پیشنهادی

| پلتفرم | کلاینت |
|--------|--------|
| اندروید | v2rayNG، Hiddify، Clash Meta |
| ویندوز | v2rayN، Hiddify، Clash Verge |
| آیفون | Streisand، Shadowrocket، Hiddify |
| مک | Hiddify، Clash Verge |

---

## سلب مسئولیت

این پروژه برای یادگیری و استفادهٔ شخصی است. مسئولیت رعایت قوانین کشور و قوانین Cloudflare با خود کاربر است.

---

## لینک‌های مفید

- پروژه: https://github.com/Shahzad55/edgetunnel
- UI انگلیسی: https://github.com/Shahzad55/EDT-Pages.github.io
- پروژه اصلی (چینی): https://github.com/cmliu/edgetunnel

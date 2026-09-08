# 🚀 EdgePanel

**English UI fork of edgetunnel** — VLESS / Trojan / Shadowsocks panel on Cloudflare Workers & Pages.

[![English](https://img.shields.io/badge/lang-English-blue)](#-english)
[![فارسی](https://img.shields.io/badge/lang-فارسی-green)](#-فارسی)
[![License](https://img.shields.io/github/license/Shahzad55/edgetunnel?style=flat-square)](LICENSE)

> Based on [cmliu/edgetunnel](https://github.com/cmliu/edgetunnel) · Admin UI translated to **English** for global users (especially Persian speakers).

**Demo UI:** [Login](https://shahzad55.github.io/EDT-Pages.github.io/login/) · [Admin](https://shahzad55.github.io/EDT-Pages.github.io/admin/)

---

## 🇬🇧 English

### Features

- **Protocols:** VLESS, Trojan, Shadowsocks
- **Admin panel:** visual dashboard (English UI) — config, logs, traffic, preferred IPs
- **Deploy:** Cloudflare Workers or Pages
- **Subscriptions:** auto-generated links for Clash, Sing-box, Surge, v2ray clients
- **Extras:** ProxyIP, SOCKS5/HTTP chain, preferred IP API, fragmentation

### Quick deploy (Workers)

1. Create a **Worker** in Cloudflare Dashboard.
2. Paste the content of [`_worker.js`](./_worker.js).
3. **Settings → Variables** → add:
   - `ADMIN` = your panel password
4. **Settings → Bindings** → add **KV Namespace**:
   - Variable name: `KV`
5. Optional: **Triggers → Custom Domain** (e.g. `vless.yourdomain.com`).
6. Open `https://your-domain/admin` and log in with the `ADMIN` password.

### Quick deploy (Pages — recommended)

1. Download [main.zip](https://github.com/Shahzad55/edgetunnel/archive/refs/heads/main.zip).
2. Cloudflare Pages → **Upload assets** → create project → upload zip → deploy.
3. **Settings → Environment variables** (Production):
   - `ADMIN` = your password → Save.
4. **Create new deployment** and upload the zip again.
5. **Settings → Bindings** → KV Namespace, name: `KV` → Save → redeploy.
6. Open `https://your-project.pages.dev/admin`.

### Environment variables

| Name | Required | Description |
|------|----------|-------------|
| `ADMIN` | Yes | Admin panel password |
| `UUID` | No | Fixed UUID (v4) |
| `KEY` | No | Quick subscription path key |
| `HOST` | No | Custom node domain(s) |
| `PATH` | No | Custom node path |
| `PROXYIP` | No | Custom ProxyIP |
| `GO2SOCKS5` | No | SOCKS5 whitelist domains |
| `DEBUG` | No | `1` / `true` for debug logs |

### UI repositories

| Repo | Role |
|------|------|
| [Shahzad55/edgetunnel](https://github.com/Shahzad55/edgetunnel) | Worker backend |
| [Shahzad55/EDT-Pages.github.io](https://github.com/Shahzad55/EDT-Pages.github.io) | English static admin UI |

The worker uses:

```js
const Pages静态页面 = 'https://shahzad55.github.io/EDT-Pages.github.io';
```

### Clients

Works with v2rayN, v2rayNG, Clash Meta / Mihomo, Sing-box, Surge, Shadowrocket, and most VLESS/Trojan clients.

### Disclaimer

For learning and research only. You are responsible for lawful use and compliance with Cloudflare ToS and local laws.

### Credits

- Upstream: [cmliu/edgetunnel](https://github.com/cmliu/edgetunnel)
- Original edge idea: [zizifn/edgetunnel](https://github.com/zizifn/edgetunnel)
- This fork: English admin UI + docs for non-Chinese users

---

## 🇮🇷 فارسی

### معرفی

**EdgePanel** نسخهٔ انگلیسی‌شدهٔ پنل **edgetunnel** است که روی **Cloudflare Workers / Pages** اجرا می‌شود و از پروتکل‌های **VLESS، Trojan و Shadowsocks** پشتیبانی می‌کند.

مناسب کاربرانی که رابط چینی برایشان سخت است — مخصوصاً فارسی‌زبان‌ها.

**دمو:** [ورود](https://shahzad55.github.io/EDT-Pages.github.io/login/) · [پنل ادمین](https://shahzad55.github.io/EDT-Pages.github.io/admin/)

### امکانات

- پشتیبانی از VLESS / Trojan / Shadowsocks
- پنل مدیریت با **رابط انگلیسی**
- استقرار روی Workers یا Pages
- ساخت خودکار لینک اشتراک (Clash، Sing-box و …)
- ProxyIP، پروکسی زنجیره‌ای، آی‌پی ترجیحی

### استقرار سریع (Workers)

1. در Cloudflare یک **Worker** بساز.
2. محتوای فایل [`_worker.js`](./_worker.js) را داخل ادیتور پیست کن.
3. از **Settings → Variables** متغیر زیر را اضافه کن:
   - `ADMIN` = رمز ورود پنل
4. از **Bindings** یک **KV Namespace** با نام متغیر `KV` وصل کن.
5. (اختیاری) دامنهٔ اختصاصی تنظیم کن.
6. برو به `https://دامنه‌ات/admin` و با رمز `ADMIN` وارد شو.

### استقرار سریع (Pages — پیشنهادی)

1. فایل [main.zip](https://github.com/Shahzad55/edgetunnel/archive/refs/heads/main.zip) را دانلود کن.
2. در Cloudflare Pages گزینه **Upload assets** را بزن و zip را آپلود و Deploy کن.
3. در **Environment variables** برای Production:
   - `ADMIN` = رمز عبور
4. یک Deploy جدید با همان zip بساز.
5. **Bindings** → KV با نام `KV` → ذخیره و Redeploy.
6. آدرس: `https://نام-پروژه.pages.dev/admin`

### متغیرهای محیطی

| نام | اجباری | توضیح |
|-----|--------|--------|
| `ADMIN` | بله | رمز ورود پنل |
| `UUID` | خیر | UUID ثابت |
| `KEY` | خیر | کلید اشتراک سریع |
| `HOST` | خیر | دامنهٔ نود |
| `PATH` | خیر | مسیر نود |
| `PROXYIP` | خیر | ProxyIP سفارشی |
| `GO2SOCKS5` | خیر | لیست سفید SOCKS5 |
| `DEBUG` | خیر | لاگ دیباگ |

### کلاینت‌ها

v2rayN، v2rayNG، Clash Meta، Sing-box، Surge، Shadowrocket و اکثر کلاینت‌های VLESS/Trojan.

### سلب مسئولیت

فقط برای یادگیری و تحقیق. مسئولیت استفادهٔ قانونی با خود کاربر است.

### اعتبار

- پروژه اصلی: [cmliu/edgetunnel](https://github.com/cmliu/edgetunnel)
- این فورک: رابط انگلیسی + مستندات برای کاربران غیربومی چینی

---

## License

See [LICENSE](./LICENSE). No warranty.

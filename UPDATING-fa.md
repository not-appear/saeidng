# چطور SaeidNG را آپدیت کنیم

این ریپو کپی خصوصی PattNG است با یک لایه نازک از تغییرات (شاخه `saeidng`):

- نام نمایشی SaeidNG و آیکون شاهین
- شناسه نصب جدا: `com.saeid.saeidng`
- کلید امضای ثابت در `keystore/saeidng.jks` (رمزهایش سکرت‌های گیت‌هاب‌اند)

## روند آپدیت (هر وقت PattNG نسخه تازه داد)

```bash
git fetch upstream            # upstream = github.com/patterniha/PattNG
git checkout saeidng
git merge upstream/master     # لایه تغییرات روی نسخه تازه می‌نشیند
git push origin saeidng
gh workflow run build.yml --ref saeidng -R not-appear/saeidng
```

بعد از سبز شدن بیلد، آرتیفکت arm64 را بگیرید و APK تازه را روی قبلی نصب کنید؛
چون امضا و شناسه ثابت‌اند، تنظیمات و کانفیگ‌ها سر جایشان می‌مانند.

اگر موقع merge تداخلی پیش آمد، معمولاً فقط در همین چند فایل است:
`V2rayNG/app/build.gradle.kts`، `res/values/strings.xml`، `res/xml/shortcuts.xml`،
`Utils.kt`، آیکن‌ها و `.github/workflows/build.yml` (پله Provide Keystore).

# 🚀 GDrive to YouTube Multi-Channel Uploader (Google Colab)

یک اسکریپت پایتون تعاملی و پرسرعت برای انتقال و آپلود مستقیم ویدیوها از **Google Drive** به **YouTube** از طریق محیط ابری **Google Colab** بدون مصرف حجم اینترنت یا افت سرعت.

---

## ✨ ویژگی‌ها

- ⚡ **سرعت فوق‌العاده بالا:** انتقال ابری فایل‌ها درون شبکه داخلی دیتاسنترهای گوگل (+100 MB/s).
- 📺 **پشتیبانی از چند کانال (Multi-Channel):** امکان اتصال و مدیریت آسان چندین کانال یوتیوب و Brand Account به صورت تفکیک‌شده.
- 📁 **منوی تعاملی و ایمن:** اسکن خودکار پوشه درایو، نمایش حجم فایل‌ها و انتخاب شماره ویدیو برای جلوگیری از آپلود اشتباه.
- 📝 **سفارشی‌سازی کامل متادیتا:** تعیین عنوان، توضیحات، برچسب‌ها (Tags) و وضعیت انتشار (`Private`، `Unlisted` یا `Public`).
- 🔄 **نشست‌های ماندگار (Persistent Tokens):** ذخیره خودکار توکن‌های احراز هویت در گوگل درایو بدون نیاز به لاگین مجدد در هر بار اجرا.
- 📊 **نمایش زنده درصد پیشرفت:** آپلود تکه‌تکه (Chunked) به همراه نمایش وضعیت پیشرفت.

---

## 📋 پیش‌نیازها

1. یک حساب گوگل با کانال یوتیوب فعال.
2. پوشه‌ای در گوگل درایو برای قرار دادن ویدیوها (پیش‌فرض: `/MyDrive/YouTube_Upload`).
3. فایل دسترسی `client_secrets.json` از کنسول گوگل کلود.

---

## 🛠️ راه‌اندازی و تنظیمات اولیه (فقط یک‌بار)

### ۱. دریافت فایل `client_secrets.json`
1. وارد [Google Cloud Console](https://console.cloud.google.com/) شوید و یک پروژه جدید بسازید.
2. از منوی **APIs & Services > Library** عبارت **YouTube Data API v3** را سرچ کرده و **Enable** کنید.
3. در تب **OAuth consent screen**:
   - نوع را **External** انتخاب کرده و فرم را ذخیره کنید.
   - وضعیت پروژه را با زدن دکمه **PUBLISH APP** به حالت **In Production** درآورید.
4. در تب **Credentials**:
   - روی **+ CREATE CREDENTIALS** زده و گزینه **OAuth client ID** را انتخاب کنید.
   - فیلد **Application type** را روی **Web application** بگذارید.
   - در بخش **Authorized redirect URIs** این دو آدرس را وارد کنید:
     - `http://localhost:8080/`
     - `http://localhost:8080`
   - روی **Create** کلیک کرده و فایل JSON ایجاد شده را دانلود کنید.
5. نام فایل را به `client_secrets.json` تغییر دهید و آن را در **صفحه اصلی (Root) گوگل درایو** خود آپلود کنید.

---

## 🚀 نحوه استفاده در Google Colab

### گام اول: اجرای نوت‌بوک و اتصال درایو
نوت‌بوک را در Google Colab باز کرده و سلول اتصال درایو را اجرا کنید:

```python
!pip install --upgrade google-api-python-client google-auth-oauthlib google-auth-httplib2
from google.colab import drive
drive.mount('/content/drive')

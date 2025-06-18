# دليل إعداد مفاتيح API

## 1. إعداد TMDB API (مطلوب)

### الخطوة 1: إنشاء حساب TMDB
1. اذهب إلى https://www.themoviedb.org/
2. انقر على "Join TMDB" لإنشاء حساب جديد
3. أكمل عملية التسجيل وتأكيد البريد الإلكتروني

### الخطوة 2: الحصول على API Key
1. بعد تسجيل الدخول، اذهب إلى Settings (الإعدادات)
2. انقر على "API" في القائمة الجانبية
3. انقر على "Create" لإنشاء API key جديد
4. اختر "Developer" كنوع الاستخدام
5. املأ المعلومات المطلوبة:
   - Application Name: Semo VOD App
   - Application URL: يمكنك ترك هذا فارغاً
   - Application Summary: Flutter VOD streaming application

### الخطوة 3: الحصول على Access Token
1. بعد إنشاء API key، ستجد "API Read Access Token"
2. انسخ هذا Token (يبدأ بـ eyJ...)
3. هذا هو ما تحتاجه لـ `tmdbAccessTokenAuth`

### الخطوة 4: تحديث الكود
```dart
// في ملف lib/utils/api_keys.dart
class APIKeys {
  static const String tmdbAccessTokenAuth = 'eyJhbGciOiJIUzI1NiJ9...'; // ضع token هنا
  static const String subdl = 'YOUR_SUBDL_API_KEY_HERE';
}
```

## 2. إعداد Subdl API (اختياري)

### الخطوة 1: إنشاء حساب Subdl
1. اذهب إلى https://subdl.com/
2. انقر على "Sign Up" لإنشاء حساب
3. أكمل عملية التسجيل

### الخطوة 2: الحصول على API Key
1. اذهب إلى https://subdl.com/api
2. ستجد API key الخاص بك في لوحة التحكم
3. انسخ API key

### الخطوة 3: تحديث الكود
```dart
// في ملف lib/utils/api_keys.dart
class APIKeys {
  static const String tmdbAccessTokenAuth = 'YOUR_TMDB_TOKEN_HERE';
  static const String subdl = 'your-subdl-api-key-here'; // ضع key هنا
}
```

## 3. إعداد Firebase (اختياري)

### الخطوة 1: إنشاء مشروع Firebase
1. اذهب إلى https://console.firebase.google.com/
2. انقر على "Create a project"
3. اتبع الخطوات لإنشاء المشروع

### الخطوة 2: إضافة تطبيق Android
1. في لوحة تحكم Firebase، انقر على أيقونة Android
2. أدخل package name: `net.examnet.semo`
3. أدخل App nickname: `Semo VOD App`
4. اترك SHA-1 فارغاً للآن

### الخطوة 3: تحميل google-services.json
1. حمل ملف `google-services.json`
2. ضعه في مجلد `android/app/`
3. تأكد من أن package name في الملف يطابق `net.examnet.semo`

### الخطوة 4: تفعيل الخدمات (اختياري)
- **Authentication**: لتسجيل الدخول
- **Firestore**: لحفظ البيانات
- **Analytics**: لتتبع الاستخدام
- **Crashlytics**: لتتبع الأخطاء

## 4. إعادة بناء التطبيق

بعد تحديث مفاتيح API:

```bash
# تنظيف البناء السابق
flutter clean

# الحصول على التبعيات
flutter pub get

# بناء APK جديد
flutter build apk --release
```

## 5. اختبار التطبيق

### اختبار TMDB API:
- افتح التطبيق
- جرب البحث عن فيلم
- تأكد من ظهور النتائج والصور

### اختبار Subdl API:
- افتح فيلم أو مسلسل
- ابحث عن خيار الترجمات
- تأكد من توفر ترجمات

### اختبار Firebase:
- جرب تسجيل الدخول (إذا كان متاحاً)
- تأكد من حفظ المفضلة

## 6. استكشاف الأخطاء

### مشكلة: لا تظهر الأفلام
**الحل**: تأكد من صحة TMDB Access Token

### مشكلة: لا تعمل الترجمات
**الحل**: تأكد من صحة Subdl API key

### مشكلة: خطأ في Firebase
**الحل**: تأكد من وضع google-services.json في المكان الصحيح

## 7. حدود الاستخدام

### TMDB API:
- 1000 طلب كل 24 ساعة (مجاني)
- 50 طلب كل 10 ثوانٍ

### Subdl API:
- حسب خطة الاشتراك

## 8. الأمان

⚠️ **تحذير أمني**:
- لا تشارك مفاتيح API مع أحد
- لا ترفع مفاتيح API إلى GitHub
- استخدم متغيرات البيئة في الإنتاج

---

**ملاحظة**: هذا الدليل للاستخدام التعليمي والتطويري فقط. تأكد من اتباع شروط استخدام كل API.
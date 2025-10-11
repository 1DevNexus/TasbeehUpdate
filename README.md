# نظام فحص التحديثات عبر GitHub

## 📋 الوصف
نظام بسيط وفعال لفحص تحديثات التطبيق عبر ملف JSON مستضاف على GitHub.

---

## 📁 هيكل المجلد

```
inventory/
├── versions/
│   └── app_updates.json    ← ملف التحديثات
└── README.md               ← هذا الملف
```

---

## 📝 ملف app_updates.json

### البنية:
```json
[
  {
    "version": 21,
    "updatePriority": 0
  }
]
```

### الحقول:
- **version**: رقم الإصدار (versionCode من build.gradle)
- **updatePriority**: أولوية التحديث

### أولويات التحديث:
| القيمة | النوع | الوصف |
|-------|-------|-------|
| `5` | CRITICAL | حرج - يجب التحديث فوراً |
| `4` | MAJOR | مهم - تحديث موصى به |
| `3` | MODERATE | متوسط - تحديث عادي |
| `2` | MINOR | بسيط - تحسينات صغيرة |
| `1` | COSMETIC | تجميلي - تغييرات بصرية |
| `0` | NONE | لا يوجد تحديث |

---

## 🚀 كيفية الاستخدام

### 1. رفع المجلد على GitHub:
```bash
# إنشاء مستودع جديد على GitHub
# ثم رفع مجلد inventory

git init
git add inventory/
git commit -m "Add app updates system"
git remote add origin https://github.com/YourUsername/YourRepo.git
git push -u origin main
```

### 2. تحديث رابط GitHub في الكود:
في ملف `UpdateManager.java`:
```java
private static final String UPDATES_URL = 
    "https://raw.githubusercontent.com/YourUsername/YourRepo/main/inventory/versions/app_updates.json";
```

### 3. إضافة تحديث جديد:
عدّل ملف `app_updates.json`:
```json
[
  {
    "version": 22,
    "updatePriority": 4
  },
  {
    "version": 21,
    "updatePriority": 0
  }
]
```

---

## 📊 مثال عملي

### السيناريو:
```
التطبيق الحالي: versionCode = 21
ملف JSON:
[
  {"version": 23, "updatePriority": 5},  ← تحديث حرج
  {"version": 22, "updatePriority": 4},  ← تحديث مهم
  {"version": 21, "updatePriority": 0}   ← الإصدار الحالي
]
```

### النتيجة:
1. ✅ يتم تحميل الملف من GitHub
2. ✅ يتم فلترة الإصدارات الأحدث من 21
3. ✅ يتم اختيار الإصدار 23 (أعلى أولوية = 5)
4. ✅ يظهر حوار "تحديث حرج"
5. ✅ عند الضغط على "تحديث الآن" → يفتح Google Play

---

## ⚙️ الملفات المطلوبة في المشروع

### 1. Models:
- `app/src/main/java/com/isysway/altasbih/models/AppUpdate.java`

### 2. Utils:
- `app/src/main/java/com/isysway/altasbih/utils/AppUpdateInfo.java`
- `app/src/main/java/com/isysway/altasbih/utils/UpdateManager.java`

### 3. Strings:
- `app/src/main/res/values/strings.xml`
- `app/src/main/res/values-ar/strings.xml`

### 4. MainActivity:
- تم إضافة دالة `checkForAppUpdates()` في `MainActivity.java`

---

## 🔧 Dependencies المطلوبة

في `build.gradle`:
```gradle
dependencies {
    // Volley for network requests (already included)
    implementation 'com.android.volley:volley:1.2.1'
    
    // Gson for JSON parsing (add if not exists)
    implementation 'com.google.code.gson:gson:2.10.1'
}
```

---

## ✅ المميزات

1. ✅ **لا يحتاج سيرفر** - فقط GitHub
2. ✅ **سهل التحديث** - فقط عدل ملف JSON
3. ✅ **مرن** - 6 مستويات أولوية
4. ✅ **آمن** - يمكن إغلاق الحوار
5. ✅ **سريع** - يستخدم GitHub Raw
6. ✅ **مجاني** - بدون تكاليف

---

## 📱 الاختبار

### 1. اختبار محلي:
- غيّر `versionCode` في `build.gradle` إلى 20
- شغّل التطبيق
- يجب أن يظهر حوار التحديث

### 2. اختبار على GitHub:
- ارفع الملف على GitHub
- غيّر الرابط في `UpdateManager.java`
- شغّل التطبيق
- يجب أن يتم تحميل التحديثات من GitHub

---

## 🎯 ملاحظات مهمة

1. ⚠️ **لا تنسى تحديث الرابط** في `UpdateManager.java`
2. ⚠️ **استخدم Raw URL** من GitHub (ليس الرابط العادي)
3. ⚠️ **رتب التحديثات** من الأحدث للأقدم
4. ⚠️ **اختبر قبل النشر** على Google Play

---

## 📞 الدعم

إذا واجهت أي مشاكل:
1. تحقق من الرابط في `UpdateManager.java`
2. تحقق من صحة ملف JSON
3. تحقق من الـ Logs في Android Studio

---

**تم إنشاء النظام بنجاح! 🎉**

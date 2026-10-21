# مشغل محمد عيشان — Android APK دون إنترنت

هذا المستودع جاهز للرفع إلى GitHub. التطبيق يعمل دون إنترنت بعد تثبيته، وملفات الفيديو والصوت والصور تبقى على الهاتف.

## البناء من الهاتف عبر GitHub Actions

1. أنشئ مستودعًا جديدًا على GitHub.
2. ارفع **محتويات** هذا المجلد إلى المستودع، بحيث يكون الملف `package.json` في الجذر، وبداخله:
   - `android/`
   - `www/`
   - `.github/workflows/build-apk.yml`
3. افتح تبويب **Actions** في GitHub.
4. اختر **Build محمد عيشان APK**.
5. اضغط **Run workflow**، أو ادفع أي تعديل إلى فرع `main` أو `master`.
6. بعد انتهاء البناء افتح نتيجة التشغيل، ثم قسم **Artifacts**.
7. حمّل `mohamed-aishan-debug-apk`، فك الضغط، ثم ثبّت `app-debug.apk` على هاتف Android.

ملف الـ Workflow يستخدم Node.js 22 وJava 21، يثبت اعتماديات المشروع، يزامن ملفات الواجهة، ثم ينفذ `assembleDebug` ويرفع APK كـ Artifact.

## البناء محليًا عبر Android Studio

```bash
npm ci
npx cap sync android
npx cap open android
```

بعد فتح مجلد `android/` في Android Studio يمكنك اختيار **Build > Build APK(s)**.

## إصدار Release موقّع

نسخة `debug` مناسبة للاختبار والتثبيت اليدوي. للنشر العام استخدم Android Studio أو Workflow منفصلًا مع Keystore محفوظ في GitHub Secrets. لا ترفع ملف `.jks` أو كلمات المرور إلى المستودع.

## تحديث التطبيق

بعد تعديل `www/index.html` نفّذ:

```bash
npx cap sync android
```

ثم ارفع التغييرات إلى GitHub ليُبنى APK جديد تلقائيًا.

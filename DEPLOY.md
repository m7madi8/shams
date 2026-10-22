# نشر الموقع (Vercel)

## المشكلة الشائعة

الكود على GitHub محدّث لكن **shams-three.vercel.app** يعرض نسخة قديمة ولا يظهر **Deployment** جديد.

السبب المعتاد: مشروع Vercel **غير مربوط** بمستودع `m7madi8/shams` (أو انقطع الربط). مستودع GitHub بدون webhooks لـ Vercel = لا نشر تلقائي.

## الحل ١ — إعادة ربط المشروع (مُفضّل)

1. ادخل [vercel.com](https://vercel.com) بنفس الحساب الذي أنشأ `shams-three`.
2. **Add New… → Project**.
3. اختر **Import** لمستودع **m7madi8/shams**.
4. الإعدادات:
   - **Framework Preset:** Other
   - **Root Directory:** `./`
   - **Build Command:** اتركه فارغًا
   - **Output Directory:** اتركه فارغًا (موقع ثابت)
5. **Deploy**.

إذا ظهر مشروع مكرر: احذف القديم أو اربط النطاق `shams-three.vercel.app` بالمشروع الجديد من **Settings → Domains**.

بعد الربط، كل `git push` على `main` يجب أن يظهر Deployment جديد خلال دقيقة.

## الحل ٢ — GitHub Actions

إذا لم يعمل الربط من لوحة Vercel، استخدم الـ workflow في `.github/workflows/vercel-deploy.yml`:

1. أنشئ **Vercel Token** (Account Settings → Tokens).
2. من مشروع shams في Vercel: **Project ID** و **Team ID**.
3. في GitHub: **Settings → Secrets and variables → Actions** وأضف:
   - `VERCEL_TOKEN`
   - `VERCEL_ORG_ID`
   - `VERCEL_PROJECT_ID`
4. ادفع أي تغيير على `main` أو شغّل الـ workflow يدويًا من **Actions**.

## التحقق بعد النشر

- https://shams-three.vercel.app/heba.jpg → يجب أن يعيد **200**
- صفحة المؤسِّسة تعرض صورة **heba.jpg** (وليس `nawal.png`)

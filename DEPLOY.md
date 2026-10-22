# لماذا لا يظهر Deployment جديد على Vercel؟

الكود على GitHub **محدّث** (مثلاً `3533e55` وما بعده). إذا Vercel لا ينشر:

1. **لا يوجد ربط Git** — مستودع `m7madi8/shams` بدون webhooks لـ Vercel (شائع بعد حذف المشروع أو تغيير الحساب).
2. **Outage GitHub** — رسالة Vercel «Automatic deployments from GitHub may be delayed» تعني انتظر أو انشر يدويًا.
3. **مشروع Vercel على حساب/فريق آخر** — تحقق أنك في نفس Team الذي يملك `shams-three.vercel.app`.

---

## الحل الأسرع: Deploy Hook (دقيقتان)

لا يحتاج إعادة ربط Git كاملًا.

1. **Vercel** → مشروع الموقع → **Settings** → **Git** → **Deploy Hooks**.
2. **Create Hook** — الاسم: `github-main` — الفرع: `main` — انسخ الرابط.
3. **GitHub** → `m7madi8/shams` → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:
   - الاسم: `VERCEL_DEPLOY_HOOK`
   - القيمة: الرابط الذي نسخته.
4. **GitHub** → **Actions** → **Trigger Vercel deploy** → **Run workflow**.

بعدها كل `push` على `main` يشغّل الـ workflow ويستدعي Vercel.

تأكد أن **Actions** مفعّلة: **Settings** → **Actions** → **General** → Allow all actions.

---

## الحل الكامل: إعادة ربط Git في Vercel

1. **Add New** → **Project** → Import **`m7madi8/shams`**.
2. Framework: **Other** — بدون Build — بدون Output Directory.
3. **Deploy**.
4. اربط النطاق **shams-three.vercel.app** من **Settings** → **Domains** إن لزم.

---

## بديل: GitHub Pages (إذا Vercel تعطل)

1. **GitHub** → **Settings** → **Pages** → **Build and deployment** → Source: **GitHub Actions**.
2. ادفع على `main` أو شغّل workflow **Deploy to GitHub Pages**.
3. الرابط: `https://m7madi8.github.io/shams/` (الصور النسبية `heba.jpg` تعمل).

---

## بعد أي نشر ناجح

- `…/heba.jpg` → HTTP 200
- قسم المؤسِّسة يعرض الصورة (بدون `hidden` + `lazy` القديم)

# توجيه إصدار 9.00 إلى المستودع المستقل (خطوة منفصلة)

**لا تطبّق هذا التغيير قبل نشر ملفات المضيف أعلاه والتأكد من ظهور رابط GitHub Pages.**

الملف المطلوب تعديله هو `gamerhack-launch.html` في المستودع `alryes96.github.io` فقط؛ لا تعدل الصفحة الرئيسية `index.html` ولا تحذف `g2all`.

1. في آخر سكربت صفحة `gamerhack-launch.html` ابحث عن: `var BASE='https://alryes96.github.io/ALRYES96-PS4-Host/g2all/';`
2. أضف تحته: `var BASE_900='https://alryes96.github.io/ALRYES96-PS4-Host-900/';`
3. بعد دالة `firmwareCode(version)` أضف: `function hostFor(version){ return firmwareCode(version)===900 ? BASE_900 : BASE; }`
4. غيّر التحويل التلقائي ليصبح: `setTimeout(function(){ window.location.replace(hostFor(detected)+'index.html'); }, 900);`
5. غيّر تحويل زر البدء ليصبح: `window.location.href=hostFor(firmware)+'index.html';`

هذه القاعدة تجعل 9.00 فقط يذهب إلى المستودع الجديد. الإصدار 9.03 وما بعده يبقى على المسار القديم لأن `hostFor` يطابق `900` بدقة. بعد الحفظ افحص أن بقية الإصدارات لم تتغير.

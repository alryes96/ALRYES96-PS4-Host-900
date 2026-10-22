# تعديل توجيه Firmware 9.00 من بوابة ALRYES96 الرئيسية

**لا تطبّق هذا التغيير قبل نشر صفحة المستودع الجديد عبر GitHub Pages والتأكد من فتحها بنجاح.** هذا تعديل توجيه فقط؛ لا يضيف ملفات الجلبريك إلى المستودع الجديد.

الملف الذي سيتعدل في المستودع `alryes96/alryes96.github.io` هو `gamerhack-launch.html` فقط. لا تعدّل `index.html` الرئيسي ولا تصميم الخلفية.

## 1) أضف عنوان المستودع الجديد
ابحث في سكربت آخر الصفحة عن:

```js
var BASE='https://alryes96.github.io/ALRYES96-PS4-Host/g2all/';
```

وخليه هكذا:

```js
var BASE='https://alryes96.github.io/ALRYES96-PS4-Host/g2all/';
var BASE_900='https://alryes96.github.io/ALRYES96-PS4-Host-900/';
```

## 2) أضف دالة تحديد المضيف
بعد نهاية الدالة `firmwareCode(version)` مباشرة، وقبل `function routeFor(version)`، أضف:

```js
function hostFor(version){
  return firmwareCode(version)===900 ? BASE_900 : BASE;
}
```

هذا يوجّه **9.00 فقط** إلى المستودع الجديد؛ 9.03 و9.50 و9.60 تبقى على المسار الحالي.

## 3) غيّر موضعي التحويل فقط
ابحث عن التحويل التلقائي:

```js
setTimeout(function(){ window.location.replace(BASE+'index.html'); }, 900);
```

واستبدله بـ:

```js
setTimeout(function(){ window.location.replace(hostFor(detected)+'index.html'); }, 900);
```

ثم ابحث عن تحويل زر البدء:

```js
window.location.href=BASE+'index.html';
```

واستبدله بـ:

```js
window.location.href=hostFor(firmware)+'index.html';
```

## 4) اختبارات ما بعد الحفظ
- افتح الرابط الرئيسي من الحاسبة وتأكد أن التصميم ما تغيّر.
- افحص أن اختيار 9.00 يتجه إلى `https://alryes96.github.io/ALRYES96-PS4-Host-900/`.
- افحص أن 9.03 و9.50 و9.60 والإصدارات الأخرى المدعومة تبقى على `https://alryes96.github.io/ALRYES96-PS4-Host/g2all/`.
- بما أن صفحة المستودع الجديد حالياً تأسيسية فقط، لا تتوقع أن تشغّل الجلبريك من هذا المسار بعد.

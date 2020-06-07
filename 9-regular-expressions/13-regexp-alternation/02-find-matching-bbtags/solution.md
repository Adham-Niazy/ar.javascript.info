
علامة الفتح هي `النمط: \ [(b | url | الاقتباس) \]`.

ثم للعثور على كل شيء حتى علامة الإغلاق - دعنا نستخدم النمط `pattern:. *؟` مع العلامة `pattern: s` لمطابقة أي حرف بما في ذلك السطر الجديد ثم إضافة مرجع خلفي إلى علامة الإغلاق.

النمط الكامل: `pattern: \ [(b | url | الاقتباس) \]. *؟ \ [/ \ 1 \]`.

بشكل عملي:

```js run
let regexp = /\[(b|url|quote)\].*?\[\/\1\]/gs;

let str = `
  [b]hello![/b]
  [quote]
    [url]http://google.com[/url]
  [/quote]
`;

alert( str.match(regexp) ); // [b]hello![/b],[quote][url]http://google.com[/url][/quote]
```

يرجى ملاحظة أنه بالإضافة إلى الهروب من `نمط: [` و `نقش:]` ، كان علينا أن نهرب من شرطة مائلة لنموذج علامة الإغلاق: [\ / \ 1] `، لأن الخط المائل يغلق النمط عادةً.
---
title: "انتخاب تعداد اجزای اصلی"
date: 2020-11-13T11:56:23+03:30
draft: false
weight: 100
---

چگونه k را انتخاب کنیم، که به آن تعداد اجزای اصلی نیز گفته می‌شود؟

<!-- به یاد بیاورید که k ابعادی است که ما به آن کاهش می‌دهیم. -->

یکی از راه های انتخاب k استفاده از فرمول زیر است:

- با توجه به خطای average squared projection: $\frac{1}{m} \sum _{i = 1} ^ m || x ^{(i)} - x ^{(i)} _ {approx} || ^ 2 $ 

- همچنین با توجه به تنوع کل داده ها: $\frac{1}{m} \sum _{i = 1} ^ m || x ^{(i)} || $ 

- k راه طوری انتخاب کنید که کوچکترین مقدار باشد:
$$
\frac{\frac{1}{m} \sum _{i = 1} ^ m || x ^{(i)} - x ^{(i)} _ {approx} || ^ 2 }
{\frac{1}{m} \sum _{i = 1} ^ m || x ^{(i)} ||} \leq 0.01
$$

به عبارت دیگر، خطای squared projection تقسیم بر کل تغییر باید کمتر از یک درصد باشد،
به طوری که 99٪ از واریانس حفظ شود.

### الگوریتم انتخاب k

1. PCA را با $k=1,2,...$ امتحان کنید
2. محاسبه $U _ {reduce}, z , x$
3. فرمول بالا را بررسی کنید تا 99٪ واریانس حفظ شود. در غیر این صورت، به مرحله یک بروید و k را افزایش دهید.

این روش در واقع به طرز وحشتناکی ناکارآمد خواهد بود.
در اوکتاو ما از svd استفاده خواهیم کرد:


<div align="left">

```
[U,S,V] = svd(Sigma)
```

</div>

که به ما یک ماتریس S می‌دهد،
در واقع می‌توانیم 99٪ از واریانس حفظ شده را با استفاده از ماتریس S به شرح زیر بررسی کنیم:

$$
\frac{ \sum _ {i = 1} ^ k S_{ii} }{\sum _ {i = 1} ^ n  S_{ii}} \geq 0.99
$$

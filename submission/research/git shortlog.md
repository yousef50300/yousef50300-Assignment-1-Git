# Git Shortlog

## إيه هو `git shortlog`؟

أمر `git shortlog` بيديني ملخص للـ `Commits` الموجودة في المشروع، وبيجمعها حسب اسم كل شخص شارك فيه.

بدل ما أشوف كل الـ Commits بترتيبها زي `git log`، الأمر بيعرض اسم كل مطور وتحته الـ Commits اللي عملها.

## إزاي بستخدمه؟

```bash
git shortlog
```

النتيجة اللي بشوفها بتكون بالشكل ده:

```text
Ahmed:
    Add login page
    Fix validation error

Yousef:
    Add payment service
    Update order status
```

## عرض عدد الـ Commits لكل شخص

```bash
git shortlog -s
```

النتيجة:

```text
2  Ahmed
2  Yousef
```

`-s` بتعرضلي عدد الـ Commits بس، من غير رسائلها.

## الترتيب حسب عدد الـ Commits

```bash
git shortlog -sn
```

- `-s` لعرض العدد.
- `-n` للترتيب من أكبر عدد لأقل عدد.

النتيجة:

```text
25  Yousef Ahmed
18  Ahmed Ali
7   Mohamed Hassan
```

## عرض البريد الإلكتروني

```bash
git shortlog -sne
```

لو استخدمت `-e`، بيظهرلي البريد الإلكتروني جنب اسم الشخص:

```text
25  Yousef Ahmed <yousef@example.com>
18  Ahmed Ali <ahmed@example.com>
```

وده مفيد لو نفس الشخص كان بيعمل Commits بأكتر من بريد إلكتروني.

## عرض البيانات من كل الفروع

```bash
git shortlog -sne --all
```

`--all` بتخليني أحسب الـ Commits الموجودة في كل الفروع.

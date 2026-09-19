# Git Squash

## إيه هو `Git Squash`؟

الـ `Squash` معناه دمج كذا `Commit` في `Commit` واحدة.

مثلاً لو عملت الـ Commits دي أثناء شغلي:

```text
Add payment service
Fix validation
Fix error message
```

ممكن أدمجهم في Commit واحدة مرتبة:

```text
Add payment service
```

الكود نفسه مش بيضيع، لكن تاريخ الـ Commits بيتغير.

## إزاي بعمل Squash؟

لو عاوز أدمج آخر 3 Commits، أستخدم:

```bash
git rebase -i HEAD~3
```

هيظهرلي:

```text
pick a1b2c3d Add payment service
pick b2c3d4e Fix validation
pick c3d4e5f Fix error message
```

بسيب أول واحدة `pick`، وبغيّر الباقي إلى `squash` أو `s`:

```text
pick a1b2c3d Add payment service
squash b2c3d4e Fix validation
squash c3d4e5f Fix error message
```

بعد الحفظ، Git هيطلب مني أكتب رسالة الـ Commit النهائية.

## هل الـ Squash فيه خطورة؟

الـ Squash بيعيد كتابة تاريخ المشروع، وبيعمل `Commit Hash` جديد. علشان كده هو شبه `git commit --amend`.

لو الـ Commits لسه عندي محليًا ومترفعتش، أقدر أعمل Squash بشكل طبيعي.

لكن لو اترفعت على الـ Remote، وفي حد من الفريق بنى شغله عليها، تغييرها ممكن يعمل تعارض واختلاف في التاريخ عند باقي الفريق.

لو الـ Branch خاص بيا ومحدش شغال عليه، ممكن أرفع التعديل باستخدام:

```bash
git push --force-with-lease
```

الأفضل استخدام `--force-with-lease` بدل `--force`؛ لأنه أكثر أمانًا، وبيوقف العملية لو فيه تغييرات جديدة على الـ Remote مش موجودة عندي.

## الخلاصة

`Git Squash` بستخدمه علشان أدمج كذا Commit صغيرة في Commit واحدة مرتبة.

هو مفيد لتنظيم تاريخ المشروع، لكن لازم أستخدمه بحذر بعد رفع الـ Commits، خصوصًا لو فيه حد تاني من الفريق بنى شغله عليها.

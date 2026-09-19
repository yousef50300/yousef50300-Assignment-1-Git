# Git Cherry-pick

## إيه هو `git cherry-pick`؟

أمر `git cherry-pick` بستخدمه لما أكون عاوز آخد `Commit` معينة من Branch وأضيفها عندي، من غير ما أعمل `Merge` للـ Branch كله.

يعني باختصار:

> بدل ما أخد كل تعديلات الـ Branch، باختار Commit واحدة بس.

## مثال بسيط

عندي Branch اسمه:

```text
feature/payment
```

وعليه 3 Commits:

```text
A — B — C
```

أنا محتاج التعديل الموجود في `Commit B` بس، ومش عاوز باقي التعديلات.

أول حاجة بجيب رقم الـ Commit:

```bash
git log --oneline
```

ممكن النتيجة تكون:

```text
a1b2c3d Add payment service
b2c3d4e Fix payment error
c3d4e5f Update payment page
```

لو الـ Commit اللي محتاجها رقمها:

```text
b2c3d4e
```

بروح للـ Branch اللي عاوز أضيف التعديل عليه:

```bash
git switch main
```

وبعدها أكتب:

```bash
git cherry-pick b2c3d4e
```

كده Git هياخد تغييرات الـ Commit دي ويحطها على الـ Branch الحالي.

## إيه اللي بيحصل بعد الأمر؟

Git بيعمل Commit جديدة عندي فيها نفس التغييرات، لكن بيكون ليها `Hash` جديد؛ لأنها اتضافت في مكان مختلف في تاريخ المشروع.

مثلاً:

قبل `cherry-pick`:

```text
main: A — D
feature: A — B — C
```

بعد ما أخدت `B`:

```text
main: A — D — B'
feature: A — B — C
```

`B'` فيها نفس تغييرات `B`، لكن الـ Hash مختلف.

## لو حصل Conflict

لو حصل تعارض، بحل المشكلة في الملفات وبعدها أكتب:

```bash
git add .
git cherry-pick --continue
```

ولو عاوز ألغي العملية وأرجع زي ما كنت:

```bash
git cherry-pick --abort
```

## إمتى أستخدمه؟

ممكن أستخدم `cherry-pick` في حالات زي:

* نقل إصلاح Bug من Branch لفرع تاني.
* أخذ تعديل معين من غير دمج باقي الـ Branch.
* نقل Commit اتعملت على الـ Branch الغلط.

## الخلاصة

`git cherry-pick` بياخد تغييرات Commit معينة ويضيفها على الـ Branch الحالي في Commit جديدة.

```bash
git cherry-pick commit-hash
```

الأمر مفيد لما أكون محتاج تعديل محدد، لكن مش محتاج أعمل `Merge` لكل شغل الـ Branch.

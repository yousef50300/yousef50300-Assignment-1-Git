# شرح Git Worktree

أمر `git worktree` بيسمحلي أفتح أكتر من فرع من نفس الـRepository في فولدرات مختلفة، وأشتغل عليهم في نفس الوقت.

## المشكلة العادية

لو أنا شغال على فرع:

```text
feature/payment
```

وفجأة محتاج أصلح مشكلة سريعة على:

```text
main
```

غالبًا هضطر أحفظ شغلي باستخدام `commit` أو `stash`، وبعدها أغيّر الفرع.

## الحل باستخدام Worktree

أقدر أفتح فرع `main` في فولدر منفصل:

```bash
git worktree add ../project-main main
```

هيبقى عندي:

```text
project/       → feature/payment
project-main/  → main
```

الفولدران تابعان لنفس الـRepository، لكن كل فولدر مفتوح على فرع مختلف.

## إنشاء Worktree مع فرع جديد

```bash
git worktree add -b hotfix/login ../project-hotfix main
```

الأمر ده:

1. ينشئ فرعًا جديدًا اسمه `hotfix/login`.
2. يبدأه من `main`.
3. يفتحه داخل فولدر `project-hotfix`.

## عرض الـWorktrees

```bash
git worktree list
```

## إزالة Worktree

بعد ما أخلص:

```bash
git worktree remove ../project-main
```

ده بيحذف فولدر الـWorktree، لكنه لا يحذف الفرع نفسه.


## تنظيف Worktrees المحذوفة يدويًا

لو حذفت فولدر الـWorktree من خارج Git:

```bash
git worktree prune
```

الأمر ده بينظف بيانات الـWorktrees القديمة، ومختلف عن:

```bash
git prune
```

## ملاحظات مهمة

- مينفعش أفتح نفس الفرع في Worktree تانية في نفس الوقت.
- كل Worktree لها ملفاتها و`Working Directory` الخاص بها.
- الـWorktrees تشترك في تاريخ الـRepository والـObjects.
- بستفيد منه في الـHotfixes أو تشغيل أكثر من نسخة من المشروع.

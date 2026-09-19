# شرح Git Prune

أمر `git prune` بيحذف الـGit Objects اللي مبقاش فيه أي مرجع بيوصل ليها.

الـObjects دي ممكن تكون:

- Commits
- ملفات `Blobs`
- مجلدات `Trees`

## مثال بسيط

لو عملت Commit وبعدها استخدمت:

```bash
git reset --hard HEAD~1
```

الـCommit اختفت من تاريخ الفرع، لكنها ممكن تفضل موجودة مؤقتًا داخل مجلد:

```text
.git/objects
```

طالما مفيش Branch أو Tag أو Reference بيشاور عليها، بسميها:

```text
Unreachable Object
```

## عرض الـObjects غير المستخدمة

قبل الحذف، أقدر أفحصها:

```bash
git fsck --unreachable
```

## حذفها

```bash
git prune
```

لكن غالبًا مش بستخدم الأمر ده مباشرة؛ لأن الحذف ممكن يمنعني من استرجاع Commit ضاعت مني.

الطريقة اللي بفضلها عادة:

```bash
git gc
```

الأمر ده بينظف ويحسن تخزين المستودع، وبيشغّل `prune` بطريقة أكثر أمانًا وفقًا لمدة الاحتفاظ المحددة.

## مهم

`git prune`:

- مش بيحذف Branches.
- مش بيحذف الملفات الحالية.
- مش بيحذف Commits لسه فيه Reference بيوصل ليها.
- بيحذف Objects غير قابلة للوصول فقط.

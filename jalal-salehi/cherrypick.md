
# توضیح cherry-pick در گیت

دستور `git cherry-pick` برای گرفتن یک یا چند کامیت از یک شاخه دیگر و اعمال آن‌ها روی شاخه فعلی استفاده می‌شود.

---

## 🎯 هدف

فرض کنیم در شاخه `feature-1` یک یا چند کامیت مهم داریم و می‌خواهیم فقط آن‌ها را روی شاخه `master` اعمال کنیم، بدون اینکه کل شاخه را ادغام کنیم.

---

## 🧪 مثال عملی: مرحله به مرحله

### ✅ مرحله 1: ساخت یک ریپوی ساده

```bash
git init cherrypick-repo
cd cherrypick-repo
echo "line 1" > file.txt
git add .
git commit -m "add file.txt"
```

---

### ✅ مرحله 2: ساخت شاخه جدید و اعمال تغییر

```bash
git checkout -b feature-1
echo "line 2 from feature-1" >> file.txt
git commit -am "Add line 2 in feature-1"

echo "line 3 from feature-1" >> file.txt
git commit -am "Add line 3 in feature-1"
```

اکنون در شاخه `feature-1` دو کامیت جدید داریم.

---

### ✅ مرحله 3: بازگشت به main

```bash
git checkout master
```

---

### ✅ مرحله 4: استفاده از git cherry-pick

فرض کنیم فقط می‌خواهیم **کامیت دوم** (خط ۳) را وارد `master` کنیم.

ابتدا `log` را بررسی می‌کنیم:

```bash
git log feature-1 --oneline
```

مثلاً خروجی:
```
f3c3d17 Add line 3 in feature-1
b4e2a98 Add line 2 in feature-1
```

اکنون فقط کامیت `f3c3d17` را چری‌پیک می‌کنیم:

```bash
git cherry-pick f3c3d17
```

> ✅ این دستور تغییر مربوط به آن کامیت را در شاخه فعلی (master) اعمال می‌کند و یک کامیت جدید با همان تغییر ایجاد می‌شود.

---

### ✅ مرحله 5: بررسی نتیجه

```bash
cat file.txt
```

خروجی:
```
line 1
line 3 from feature-1
```
Твоё первое задание ученика 🥋

Сделай эти шаги и напиши мне:

1 Что показал git status до git add?
Ответ: On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        journal.md
        lesson.txt

nothing added to commit but untracked files present (use "git add" to track)
2 Что показал git status после git commit?
Ответ: On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        day1.md
        journal.md

nothing added to commit but untracked files present (use "git add" to track)
3 Возникли ли ошибки?
Ответ: нет

Маленькая проверка знаний 🧠

Ответь своими словами:

1 Почему Git показывает Untracked files?
Ответ: Чтобы выделить файлы которые не добавлены в коммит.
2 Что делает команда:
git add .
Ответ: Добавляет все новые файлы в коммит.
3. В чём разница между:
git add

и

git commit

Ответ: add добавляет файлы, а commit добавляет описание

Теперь следующий мини-урок: история Git ⏳

Представь, что у тебя есть:

commit 1
↓
commit 2
↓
commit 3
↓
commit 4

Git позволяет посмотреть эту историю.

Команда:

git log

Она покажет:

кто сделал commit
когда
сообщение
уникальный номер commit (hash)

Например:

commit a84f92d3
Author: Alex


Добавил страницу профиля




commit 91bd72aa
Author: Alex


Создал проект

А теперь задание №2:

В своём репозитории выполни:

git log

И пришли мне:

1 Сколько commit'ов ты увидел?
Ответ: Один
2 Как выглядит строка commit?
Ответ: commit 242af50eaadb59521427d412a945faea84579177 (HEAD -> main)
Author: ShawnRainson <ifetchenko2017@gmail.com>
Date:   Fri Aug 14 05:58:45 2026 +0300
3 Какое сообщение у твоего последнего commit?
Ответ: Add lesson.txt

🥋 Задание №3 — эксперимент

Теперь хочу, чтобы ты сам увидел, как Git запоминает изменения.

Открой lesson.txt и добавь в конец:

Сегодня я впервые изучил историю Git.

После этого не делай git add и git commit.

Сразу выполни:

git status

и затем:

git diff

Пришли мне вывод обеих команд.
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   lesson.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        day1.md
        journal.md

no changes added to commit (use "git add" and/or "git commit -a")

diff --git a/lesson.txt b/lesson.txt
index 580a130..4b7f27c 100644
--- a/lesson.txt
+++ b/lesson.txt
@@ -1,2 +1,3 @@
:

🥋 Следующий эксперимент

Теперь выполни:

git add lesson.txt

Но commit пока НЕ делай.

После этого:

git status

и:

git diff

А затем:

git diff --staged

И пришли мне вывод трёх команд.

Вот тут ты увидишь очень интересную вещь:

после git add обычный git diff и git diff --staged покажут разные результаты.

Это будет наш следующий важный урок. 😎

PS D:\git-studying> git add lesson.txt
PS D:\git-studying> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   lesson.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        day1.md
        journal.md

PS D:\git-studying> git diff
PS D:\git-studying> git diff --staged
diff --git a/lesson.txt b/lesson.txt
index 580a130..4b7f27c 100644
--- a/lesson.txt
+++ b/lesson.txt
@@ -1,2 +1,3 @@
 I'm studying Git!
:

🧠 Проверка понимания

Представь ситуацию:

Ты изменил:

A.txt
B.txt
C.txt

Потом сделал:

git add A.txt

И после этого:

git diff

показывает изменения B.txt и C.txt.

А:

git diff --staged

показывает изменения A.txt.

Вопрос:

Почему A.txt находится в git diff --staged, а B.txt и C.txt — в обычном git diff?

Ответь своими словами. Не нужно идеально — мне важно понять, действительно ли ты понял принцип staging area. 🥋
Ответ: Потому что для A.txt был выполнен git add, а для других нет.

🧠 А теперь закрепим на практике

Сделай:

git commit -m "Updated lesson.txt"

Затем:

git status

И пришли мне результат.

PS D:\git-studying> git commit -m "Updated lesson.txt"
[main dfe79b9] Updated lesson.txt
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\git-studying> git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        day1.md
        journal.md

nothing added to commit but untracked files present (use "git add" to track)
PS D:\git-studying> 

🥋 Последнее упражнение на сегодня

Выполни:

git log --oneline

Ты должен увидеть примерно:

dfe79b9 Updated lesson.txt
242af50 Add lesson.txt

Затем выполни:

git show dfe79b9

И пришли мне результат.

Вот после git show мы подведём итог Дня 1, а я дам тебе небольшой финальный экзамен без подсказок. 😈

Сегодня ты уже освоил:

repository → working directory → staging → commit → history → HEAD → origin/main

Для первого дня это очень достойный прогресс. 🥋

PS D:\git-studying> git log --oneline
dfe79b9 (HEAD -> main) Updated lesson.txt
242af50 Add lesson.txt
a915b5b (origin/main, origin/HEAD) Initial commit
PS D:\git-studying> git show dfe79b9
commit dfe79b9b8d95e05183a98c13837649dfbdf8a260 (HEAD -> main)
Author: ShawnRainson <ifetchenko2017@gmail.com>
Date:   Fri Aug 14 06:30:29 2026 +0300

:
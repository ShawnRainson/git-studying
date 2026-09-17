Задание 1

У тебя есть:

hello.py

Ты изменил его.

Что произойдёт после:

git status

Ответ: Untracked file hello.py, так как ещё не был выполнен git add

Задание 2

Ты выполнил:

git add hello.py

Что изменилось?

И главное:

создался ли commit?

Ответ: Файл добавлен в Staging, commit ещё не созданю

Задание 3

В чём разница:

git add hello.py - Добавление в Staging

и:

git commit -m "Update hello" - Отметка в истории

Задание 4

Что показывает:

git diff

?

Ответ: Показывает изменения в файлах

Задание 5

Что показывает:

git diff --staged

?
Ответ: Изменения при git add

Задание 6

Что такое commit?

Не просто:

«сохранение».

Попробуй объяснить чуть подробнее.

Ответ: Отметка в истории

Задание 7

Что означает:

HEAD -> main

?
Ответ: Показывает в какой ветке находимся

Задание 8

У тебя:

main
    ↓
A
    ↓
B
    ↓
C

А origin/main находится на:

A
 ↓
B

Что означает:

Your branch is ahead of 'origin/main' by 1 commit.

?
Ответ: В ветке находится один коммит

⌨️ Практика — создаём репозиторий

Теперь руки к клавиатуре. 😎

Создай отдельную папку для обучения:

mkdir git-day1
cd git-day1

Инициализируй Git:

git init

Проверь:

git status

Ответ:
PS D:\git-studying> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md
        deleted:    lesson.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md

no changes added to commit (use "git add" and/or "git commit -a")

Практика 1 — первый файл

Создай:

lesson.txt

Напиши:

Я изучаю Git.
Сегодня мой первый день.

Теперь:

git status

Посмотри, что Git говорит про файл.

Ответ:
PS D:\git-studying> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md
        modified:   lesson.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md

no changes added to commit (use "git add" and/or "git commit -a")

Практика 2 — первый staging

Выполни:

git add lesson.txt

Теперь:

git status

Обрати внимание, как изменился статус файла.

После этого:

git diff

Что получилось?

Ответ:
PS D:\git-studying> git add lesson.txt
PS D:\git-studying> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   lesson.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md

PS D:\git-studying> git diff
diff --git a/day1.md b/day1.md
index 59b897b..632d208 100644

Практика 3 — посмотрим staging

Выполни:

git diff --staged

Ты должен увидеть содержимое изменения, которое сейчас подготовлено к commit.

Ответ:
PS D:\git-studying> git diff --staged
diff --git a/lesson.txt b/lesson.txt
index 4b7f27c..c55cc60 100644

Практика 4 — первый commit

Теперь:

git commit -m "Add lesson.txt"

И:

git status

Репозиторий должен сообщить, что рабочее дерево чистое, если других изменений нет.

Ответ:
PS D:\git-studying> git commit -m "Add lesson.txt"
[main a6127e2] Add lesson.txt
 1 file changed, 2 insertions(+), 3 deletions(-)
PS D:\git-studying> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md

no changes added to commit (use "git add" and/or "git commit -a")

Практика 5 — изменяем файл

Теперь добавь в lesson.txt:

Я уже понимаю основы staging area.

Не делай git add.

Сначала:

git status

Потом:

git diff

Посмотри, что Git обнаружил.

Ответ:
PS D:\git-studying> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md
        modified:   lesson.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying> git diff
diff --git a/day1.md b/day1.md
index 59b897b..5ce3a04 100644

Практика 6 — staging

Теперь:

git add lesson.txt

И:

git diff

После этого:

git diff --staged

Сравни результаты.

Ты должен своими глазами увидеть:

До git add:

git diff
    ↓
показывает изменение


После git add:

git diff
    ↓
ничего

git diff --staged
    ↓
показывает изменение

Ответ:
PS D:\git-studying> git add lesson.txt
PS D:\git-studying> git diff
diff --git a/day1.md b/day1.md
index 59b897b..323a914 100644
PS D:\git-studying> git diff --staged
diff --git a/lesson.txt b/lesson.txt
index c55cc60..b31ea54 100644

Практика 7 — второй commit

Теперь:

git commit -m "Update lesson.txt"

После этого:

git log --oneline

Ты должен увидеть примерно:

XXXXXXXX Update lesson.txt
XXXXXXXX Add lesson.txt

Ответ:
PS D:\git-studying> git commit -m "Update lesson.txt"
[main 0732801] Update lesson.txt
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\git-studying> git log --oneline
0732801 (HEAD -> main) Update lesson.txt
a6127e2 Add lesson.txt
4827d7b (origin/main, origin/HEAD) Day 1: Completed
dfe79b9 Updated lesson.txt

Практика 8 — изучаем commit

Возьми hash второго commit и выполни:

git show <hash>

Например:

git show dfe79b9

Посмотри:

hash;
автора;
дату;
сообщение;
изменения.

Ответ:
PS D:\git-studying> git show dfe79b9
commit dfe79b9b8d95e05183a98c13837649dfbdf8a260
Author: ShawnRainson <ifetchenko2017@gmail.com>

⭐ Дополнительное задание

Теперь создай два файла:

notes.txt
test.txt

Но добавь в staging только:

git add notes.txt

Потом:

git status

Ты должен увидеть примерно:

Changes to be committed:
    new file: notes.txt

Untracked files:
    test.txt

Теперь сделай:

git commit -m "Add notes"

После этого test.txt не должен находиться в commit.

Проверь через:

git status

Ответ:
PS D:\git-studying> git add notes.txt
PS D:\git-studying> git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   notes.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md
        test.txt

PS D:\git-studying> git commit -m "Add notes"
[main f37a65b] Add notes
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 notes.txt
PS D:\git-studying> git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   day1.md
        deleted:    journal.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        plan.md
        progress.md
        test.txt

no changes added to commit (use "git add" and/or "git commit -a")

🥷 Задание на понимание

Представь:

A.txt
B.txt
C.txt

Все три файла были изменены.

Ты выполнил:

git add A.txt
git add B.txt
git commit -m "Update A and B"

Что произойдёт с:

A.txt
B.txt
C.txt

?
Ответ: Ну по сути в Staging будут добавлены только A и B и отмечены в истории тоже, а C останется Untracked

🔥 Задание повышенной сложности

Представь такую ситуацию:

Последний commit:
    A.txt = "Hello"

Ты изменил A.txt:
    A.txt = "Hello World"

git add A.txt

После этого снова изменил A.txt:
    A.txt = "Hello World!!!"

Теперь ответь:

Что будет содержать:

git diff - Тут будут показаны изменения файла

и что будет содержать:

git diff --staged - А здесь изменения в Staging

?

Это очень важный вопрос. Если ты его поймёшь, staging area перестанет быть для тебя абстрактным понятием.
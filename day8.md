Практика в отдельном репозитории
PS D:\git-studying> cd git-day8
PS D:\git-studying\git-day8> git init
Initialized empty Git repository in D:/git-studying/git-day8/.git/
PS D:\git-studying\git-day8> git branch --show-current
master
PS D:\git-studying\git-day8> 


                             git add app.txt
PS D:\git-studying\git-day8> git commit -m "Commit A"
[master (root-commit) eeeb828] Commit A
 1 file changed, 1 insertion(+)
 create mode 100644 app.txt
PS D:\git-studying\git-day8> git add app.txt
PS D:\git-studying\git-day8> git commit -m "Commit B"
[master 2a6d423] Commit B
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day8> git add app.txt
PS D:\git-studying\git-day8> git commit -m "Commit C"
[master 952837a] Commit C
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day8> git log --oneline --decorate
952837a (HEAD -> master) Commit C
2a6d423 Commit B
eeeb828 Commit A

Практическое задание №1 — --soft
PS D:\git-studying\git-day8> git reset --soft HEAD~1
PS D:\git-studying\git-day8> git log --oneline
>> 
2a6d423 (HEAD -> master) Commit B
eeeb828 Commit A
PS D:\git-studying\git-day8> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   app.txt

PS D:\git-studying\git-day8> git diff
PS D:\git-studying\git-day8> git diff --staged
diff --git a/app.txt b/app.txt
index d10d260..a35c795 100644
--- a/app.txt
+++ b/app.txt
@@ -1 +1 @@
-Version B
PS D:\git-studying\git-day8> Get-Content app.txt
Version C

Проверка понимания
Ответь своими словами:
1 Что делает git reset в первую очередь? - переносит указатель на предыдущий коммит
2 Чем --soft отличается от --mixed? - первый меняет указатель, второй указатель и staging area
3 Что происходит с Working Directory при --mixed? - ничего
4 Почему --hard считается опасным? - он откатывает всё, изменения могут быть потеряны
5 Что произойдёт, если выполнить git reset HEAD~1 без указания режима? - выполнится mixed
6 Чем git reset отличается от git restore? - первый перемещает указатель по истории, второй откатывает изменения

Задание 2. Изучаем --mixed
PS D:\git-studying\git-day8> git reset --mixed HEAD
Unstaged changes after reset:
M       app.txt
PS D:\git-studying\git-day8> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day8> git diff
diff --git a/app.txt b/app.txt
index d10d260..a35c795 100644
--- a/app.txt
+++ b/app.txt
PS D:\git-studying\git-day8> git diff --staged
PS D:\git-studying\git-day8> Get-Content app.txt
Version C

Задание 3. Сравниваем --soft и --mixed
PS D:\git-studying\git-day8> git add app.txt
PS D:\git-studying\git-day8> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   app.txt

PS D:\git-studying\git-day8> git reset --soft HEAD
PS D:\git-studying\git-day8> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   app.txt

PS D:\git-studying\git-day8> git diff
PS D:\git-studying\git-day8> git diff --staged
diff --git a/app.txt b/app.txt
index d10d260..a35c795 100644
--- a/app.txt
+++ b/app.txt
@@ -1 +1 @@
PS D:\git-studying\git-day8> git reset --mixed HEAD
Unstaged changes after reset:
M       app.txt
PS D:\git-studying\git-day8> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day8> git diff
diff --git a/app.txt b/app.txt
index d10d260..a35c795 100644
--- a/app.txt
+++ b/app.txt
@@ -1 +1 @@
PS D:\git-studying\git-day8> git diff --staged

Задание 4. Изучаем --hard
PS D:\git-studying\git-day8> git reset --hard HEAD
HEAD is now at 2a6d423 Commit B
PS D:\git-studying\git-day8> git status
On branch master
nothing to commit, working tree clean
PS D:\git-studying\git-day8> git diff
PS D:\git-studying\git-day8> git diff --staged

Задание 5. Практика с перемещением на два коммита назад
PS D:\git-studying\git-day8> git add app.txt
PS D:\git-studying\git-day8> git commit -m "Commit D"
[master ab0c1c9] Commit D
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day8> git add app.txt
PS D:\git-studying\git-day8> git commit -m "Commit E"
[master a24e629] Commit E
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day8> git log --oneline --decorate
a24e629 (HEAD -> master) Commit E
ab0c1c9 Commit D
2a6d423 Commit B
eeeb828 Commit A
PS D:\git-studying\git-day8> git reset --mixed HEAD~2
Unstaged changes after reset:
M       app.txt
PS D:\git-studying\git-day8> git log --oneline --decorate
2a6d423 (HEAD -> master) Commit B
eeeb828 Commit A
PS D:\git-studying\git-day8> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day8> git diff
diff --git a/app.txt b/app.txt
index d10d260..0c5fe6c 100644
--- a/app.txt
+++ b/app.txt
@@ -1 +1 @@
-Version B
PS D:\git-studying\git-day8> git diff --staged
PS D:\git-studying\git-day8> Get-Content app.txt
Version E

Задание 6. Восстанавливаем «потерянный» коммит через reflog
PS D:\git-studying\git-day8> git reflog
2a6d423 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~2
a24e629 HEAD@{1}: commit: Commit E
ab0c1c9 HEAD@{2}: commit: Commit D
2a6d423 (HEAD -> master) HEAD@{3}: reset: moving to HEAD
2a6d423 (HEAD -> master) HEAD@{4}: reset: moving to HEAD
PS D:\git-studying\git-day8> git reset --hard a24e629
HEAD is now at a24e629 Commit E
PS D:\git-studying\git-day8> git log --oneline --decorate
a24e629 (HEAD -> master) Commit E
ab0c1c9 Commit D
2a6d423 Commit B
eeeb828 Commit A
PS D:\git-studying\git-day8> Get-Content app.txt
Version E
PS D:\git-studying\git-day8> git status
On branch master
nothing to commit, working tree clean

Задание 7. Финальный экзамен 🥋
Часть А. Теория
1 Что делает git reset? - перемещает указатель
2 Чем отличаются --soft, --mixed и --hard? - первый перемещает только указатель, второй указатель и staging area, а последний откатывает всё
3 Какой режим используется по умолчанию? - mixed
4 Что произойдёт с Working Directory при --soft? - ничего
5 Что произойдёт со Staging Area при --mixed? - откатиться
6 Почему --hard опасен? - можно потерять изменения
7 Что такое HEAD~1? - откат на 1 шаг
8 Что такое reflog? - более продвинутые логи
9 Можно ли восстановить коммит, который больше не виден в обычном git log? - да, через hash
10 Чем git reset отличается от git restore? - первый перемещает HEAD, воторой откатывает изменения

Часть Б. Практические сценарии

Представь, что:
- HEAD содержит Version A;
- ты создал Version B;
- выполнил git add;
- затем создал Version C.
Заполни таблицу:
Команда	HEAD	Staging Area	Working Directory
git reset --soft HEAD~1	A	B	C
git reset --mixed HEAD~1	A	A	C
git reset --hard HEAD~1	A	A	A


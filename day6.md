Практика в PowerShell
PS D:\git-studying\git-day5> git log
commit 48057b3673e676affc1e98adfea86bf7115d4637 (HEAD -> master, origin/master, origin/HEAD)
Author: ShawnRainson <ifetchenko2017@gmail.com>
Date:   Tue Oct 20 02:55:19 2026 +0300
PS D:\git-studying\git-day5> git log --oneline    
48057b3 (HEAD -> master, origin/master, origin/HEAD) Add change from peer
e960ada Initial remote training commit
PS D:\git-studying\git-day5> git log --oneline --decorate --graph --all

* 48057b3 (HEAD -> master, origin/master, origin/HEAD) Add change from peer
* e960ada Initial remote training commit
PS D:\git-studying\git-day5> git show HEAD
commit 48057b3673e676affc1e98adfea86bf7115d4637 (HEAD -> master, origin/master, origin/HEAD)
Author: ShawnRainson <ifetchenko2017@gmail.com>
Date:   Tue Oct 20 02:55:19 2026 +0300
PS D:\git-studying\git-day5> git show --no-patch --pretty=fuller HEAD
commit 48057b3673e676affc1e98adfea86bf7115d4637 (HEAD -> master, origin/master, origin/HEAD)
Author:     ShawnRainson <ifetchenko2017@gmail.com>
AuthorDate: Tue Oct 20 02:55:19 2026 +0300
PS D:\git-studying\git-day5> git diff e960ada 48057b3
diff --git a/app.txt b/app.txt
index b7901e9..f373135 100644
--- a/app.txt
+++ b/app.txt
PS D:\git-studying\git-day5> git diff 48057b3 e960ada
>> 
diff --git a/app.txt b/app.txt
index f373135..b7901e9 100644
--- a/app.txt
+++ b/app.txt
PS D:\git-studying\git-day5> git diff e960ada 48057b3 -- app.txt
diff --git a/app.txt b/app.txt
index b7901e9..f373135 100644
--- a/app.txt
+++ b/app.txt
PS D:\git-studying\git-day5> git show e960ada:app.txt
>> 
Remote training v1
PS D:\git-studying\git-day5> git show 48057b3:app.txt
Remote training v1
Change from peer
PS D:\git-studying\git-day5> Add-Content app.txt "Day 6 practice"
PS D:\git-studying\git-day5> git diff
diff --git a/app.txt b/app.txt
index f373135..ebce445 100644
--- a/app.txt
+++ b/app.txt
PS D:\git-studying\git-day5> git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day5> git add app.txt
PS D:\git-studying\git-day5> git diff
PS D:\git-studying\git-day5> git diff --staged
diff --git a/app.txt b/app.txt
index f373135..ebce445 100644
--- a/app.txt
+++ b/app.txt

Контрольные вопросы
Ответь своими словами.

1 Чем git log отличается от git show? - git log - подробная история, git show - коммиты и внесённые изменения

2 Что показывает команда git diff A B? - разницу между коммитами

3 Почему при выполнении git diff B A знаки + и - могут поменяться местами? - потому-что меняется порядок, сначала показывают новый коммит, а потом предудущий

4 Что показывает git show HEAD? - текущий коммит

5 Чем отличаются git diff и git diff --staged? - первый разница между коммитами, а второй разница между staging area

6 Что означает HEAD~1? - первый родитель текущего коммита

7 Зачем нужен параметр --all в команде git log --oneline --graph --all? - показывает историю достижимую от ссылок, которые учитываются при обходе

8 Если ты выполнил git add app.txt, почему git diff может перестать показывать изменения в этом файле? - Не уверен, но возможно потому-что после этого были внесены ещё изменения

9 Какая команда покажет содержимое app.txt в коммите e960ada, не изменяя текущий файл на диске? - git show

10 Что показывает команда git log --oneline --decorate --graph --all такого, чего не видно в обычном git log? - покажет краткую историю в виде графов
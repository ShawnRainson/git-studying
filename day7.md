Задание 1. Подготовка
PS D:\git-studying> cd git-day7
PS D:\git-studying\git-day7> git init
Initialized empty Git repository in D:/git-studying/git-day7/.git/
PS D:\git-studying\git-day7> git branch --show-current
master
PS D:\git-studying\git-day7> git add app.txt
PS D:\git-studying\git-day7> git commit -m "Initial commit"
[master (root-commit) a532e1d] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 app.txt

Задание 2. Отменяем изменения в Working Directory
PS D:\git-studying\git-day7> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day7> git diff
diff --git a/app.txt b/app.txt
index 271a0eb..bb363bc 100644
--- a/app.txt
PS D:\git-studying\git-day7> Get-Content app.txt
Changed version
PS D:\git-studying\git-day7> git restore app.txt
PS D:\git-studying\git-day7> Get-Content app.txt
Original version
PS D:\git-studying\git-day7> git status
On branch master
nothing to commit, working tree clean

Задание 3. Убираем файл из Staging Area
PS D:\git-studying\git-day7> git add app.txt
PS D:\git-studying\git-day7> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   app.txt

PS D:\git-studying\git-day7> git diff --staged
diff --git a/app.txt b/app.txt
index 271a0eb..119ec1c 100644
--- a/app.txt
PS D:\git-studying\git-day7> git restore --staged app.txt
PS D:\git-studying\git-day7> git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day7> git diff
diff --git a/app.txt b/app.txt
index 271a0eb..119ec1c 100644
--- a/app.txt
PS D:\git-studying\git-day7> git diff --staged
PS D:\git-studying\git-day7> git diff --staged
PS D:\git-studying\git-day7> Get-Content app.txt
Staged version

Задание 4. Комбинированная ситуация
PS D:\git-studying\git-day7> git add app.txt
PS D:\git-studying\git-day7> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   app.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.txt

PS D:\git-studying\git-day7> git diff
diff --git a/app.txt b/app.txt
index bb52493..e7612d1 100644
--- a/app.txt
PS D:\git-studying\git-day7> git diff --staged
diff --git a/app.txt b/app.txt
index 271a0eb..bb52493 100644
--- a/app.txt

Проверка понимания
Ответь без запуска команд.

1 Ты изменил app.txt, но ещё не выполнил git add. Как отменить изменение? - git restore app.txt

2 Ты выполнил git add app.txt, но передумал включать файл в коммит. Как убрать его из Staging Area, сохранив изменения? - git restore --staged app.txt

3 Удаляет ли git restore --staged app.txt изменения из рабочего файла? - нет

4 Отменяет ли git restore app.txt уже созданный коммит? - нет

5 Из какого состояния Git восстанавливает файл при обычном git restore app.txt? - немного не понял вопрос, если речь о том к чему он возвращается, то к прошлому записаному в истории изменения, а если речь о том в каком состоянии файл сейчас, то пока он не находится в staging area, значит из working directory

6 Из какого состояния восстанавливается Staging Area при git restore --staged app.txt? - просто убирается из staging area

7 Чем git restore отличается от git reset? Пока достаточно объяснить на уровне назначения. - первый отменяет изменения, а второй их удаляет полностью

Финальный экзамен 🥋
Представь ситуацию:

В последнем коммите файл содержал:
A


Ты выполнил следующие действия:
Add-Content app.txt "B"
git add app.txt
Add-Content app.txt "C"


Теперь ответь:
1 Что содержит HEAD? - C
2 Что содержит Staging Area? - B
3 Что содержит Working Directory? - C
4 Что покажет git diff? - A, B, C
5 Что покажет git diff --staged? - A, B 
6 Как убрать B из Staging Area, но оставить файл с A, B и C в рабочей директории? - git restore --staged app.txt
7 Как после этого полностью вернуть файл к содержимому последнего коммита? - git restore app.txt
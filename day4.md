🧪 Практика №1 — разрешаем твой настоящий конфликт
PS D:\git-studying\git-day3> git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\git-studying\git-day3> git diff
diff --cc app.txt

app.txt:
Version 1
<<<<<<< HEAD
Master version
=======
Feature version 2
>>>>>>> feature

app.txt(fix):
Version 1
Master version
Feature version 2

PS D:\git-studying\git-day3> git diff
diff --cc app.txt
PS D:\git-studying\git-day3> git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")

 D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   app.txt


PS D:\git-studying\git-day3> git commit -m "App version fix"
[master 36ba378] App version fix

PS D:\git-studying\git-day3> git status
On branch master
nothing to commit, working tree clean
PS D:\git-studying\git-day3> git log --oneline --decorate --graph --all

*   36ba378 (HEAD -> master) App version fix

🧪 Практика №2 — самостоятельное закрепление
PS D:\git-studying\git-day3> git switch -c feature-conflict
Switched to a new branch 'feature-conflict'
PS D:\git-studying\git-day3> git branch
  feature
* feature-conflict
PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Change app"
[feature-conflict 767dc31] Change app
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day3> git switch master
Switched to branch 'master'
PS D:\git-studying\git-day3> git branch
  feature
  feature-conflict
:
  feature
  feature-conflict
* master
:
  feature
  feature-conflict
* master
~
(END)
  feature
  feature-conflict
* master
~
~
(END)
  feature
  feature-conflict
* master
~
~
~
(END)
  feature
  feature-conflict
* master
~
~
~
~
~
~
~
PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Change master app"
[master 3ca315b] Change master app
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day3> git merge feature-cnflict
merge: feature-cnflict - not something we can merge
PS D:\git-studying\git-day3> git merge feature-conflict
Auto-merging app.txt
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed; fix conflicts and then commit the result.

app.txt: 
Version 1
<<<<<<< HEAD
Master conflict version
=======
Feature-conflict version
>>>>>>> feature-conflict
Feature version 2

app.txt(fix):
Version 1
Master conflict version
Feature-conflict version
Feature version 2

PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Fix"
[master 94c2d36] Fix

PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Fix"
[master 94c2d36] Fix
PS D:\git-studying\git-day3> git status
On branch master
nothing to commit, working tree clean
PS D:\git-studying\git-day3> git log --oneline --decorate --graph --all

*   94c2d36 (HEAD -> master) Fix
|\  

Вопрос 1. Почему Git не всегда может разрешить конфликт автоматически? - Потому-что при изменении обеих веток, Git не знает какая правильнее и просит изменить вручную
Вопрос 2. Что означает <<<<<<< HEAD? - указывает на ветку в которой находимся и в которую делаем слияние
Вопрос 3. Что означает =======? - разделяет конфликтные места
Вопрос 4. Что означает >>>>>>> feature? - конец вливаемой ветки
Вопрос 5. После ручного исправления файла почему нужно выполнить git add? - потому-что были произведены изменения
Вопрос 6. Какая команда завершает незавершённый merge после разрешения всех конфликтов? - git commit
Вопрос 7. Чем отличается git merge --abort от git commit во время слияния? - первый отменяет merge, второй завершает при исправлении
Вопрос 8. Может ли Git принять файл с оставшимися конфликтными маркерами в индекс? Почему всё равно важно проверять файл? - нет не может, если маркеры остались то он считается конфликтным
Вопрос 9. Если ты находишься на master и выполняешь git merge feature, какая сторона обозначается HEAD в обычном конфликтном блоке? - master - HEAD, feature - конфликтный блок
Вопрос 10. Объясни своими словами весь процесс от появления CONFLICT до успешного merge commit. - 1 Изменения в обеих ветках 2 git merge 3 CONFLICT 4 fix конфликтного файла 5 git add 6 git commit

🏆 Финальный экзамен Day 4
Теперь более практические ситуации.
Задача A
Git сообщает:
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed


Какие три основных действия ты предпримешь, чтобы завершить merge?
1 Исправить конфликтный файл (убрать маркеры)
2 git add
3 git commit

Задача B
В файле осталось:
<<<<<<< HEAD
Hello from master
=======
Hello from feature
>>>>>>> feature


Ты хочешь сохранить только Hello from feature. Как должен выглядеть итоговый файл?
Hello from feature

Задача C
Ты выполнил:
git add app.txt
git status


Файл больше не отображается как конфликтующий, но merge ещё не завершён. Что нужно сделать дальше?
git commit

Задача D
Ты начал merge, возник конфликт, и решил полностью отменить операцию. Какую команду использовать, если merge ещё не завершён?
git merge --abort

Задача E
Почему команда git add app.txt сама по себе не гарантирует, что конфликт разрешён правильно?
Потому-что она добавляет файл для коммита
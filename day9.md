Практика — создаём репозиторий git-day9
PS D:\git-studying> cd git-day9
PS D:\git-studying\git-day9> git init
Initialized empty Git repository in D:/git-studying/git-day9/.git/
PS D:\git-studying\git-day9> git branch --show-current
master
PS D:\git-studying\git-day9> git add app.txt
PS D:\git-studying\git-day9> git commit -m "Initial commit"
[master (root-commit) e20f345] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 app.txt
PS D:\git-studying\git-day9> Get-Content app.txt
Hello!
PS D:\git-studying\git-day9> git log --oneline
e20f345 (HEAD -> master) Initial commit
PS D:\git-studying\git-day9> git add app.txt
PS D:\git-studying\git-day9> git commit -m "Add Git is awesome"
[master 0d3fcfa] Add Git is awesome
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\git-studying\git-day9> Get-Content app.txt
Hello!
Git is awesome!
PS D:\git-studying\git-day9> git log --oneline
0d3fcfa (HEAD -> master) Add Git is awesome
e20f345 Initial commit
PS D:\git-studying\git-day9> git rever --no-edit HEAD
git: 'rever' is not a git command. See 'git --help'.

The most similar command is
        revert
PS D:\git-studying\git-day9> git log --oneline --decorate
0d3fcfa (HEAD -> master) Add Git is awesome
e20f345 Initial commit
PS D:\git-studying\git-day9> Get-Content app.txt
Hello!
Git is awesome!
PS D:\git-studying\git-day9> git status
On branch master
nothing to commit, working tree clean
PS D:\git-studying\git-day9> git revert --no-edit HEAD
[master 8b05b54] Revert "Add Git is awesome"
 Date: Fri Nov 27 04:10:15 2026 +0300
 1 file changed, 1 insertion(+), 2 deletions(-)
PS D:\git-studying\git-day9> git log --oneline --decorate
8b05b54 (HEAD -> master) Revert "Add Git is awesome"
0d3fcfa Add Git is awesome
e20f345 Initial commit
PS D:\git-studying\git-day9> Get-Content app.txt
Hello!
PS D:\git-studying\git-day9> git status
On branch master
nothing to commit, working tree clean

Практика №2 — отменяем не последний коммит
PS D:\git-studying\git-day9> git add app.txt
PS D:\git-studying\git-day9> git commit -m "Add Another feature"
[master e55a51a] Add Another feature
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\git-studying\git-day9> git log --oneline
e55a51a (HEAD -> master) Add Another feature
8b05b54 Revert "Add Git is awesome"
0d3fcfa Add Git is awesome
e20f345 Initial commit
PS D:\git-studying\git-day9> git revert 0d3fcfa
Auto-merging app.txt
CONFLICT (content): Merge conflict in app.txt
error: could not revert 0d3fcfa... Add Git is awesome
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git revert --continue".
hint: You can instead skip this commit with "git revert --skip".
hint: To abort and get back to the state before "git revert",
hint: run "git revert --abort".
hint: Disable this message with "git config set advice.mergeConflict false"
PS D:\git-studying\git-day9> git log --oneline --decorate
e55a51a (HEAD -> master) Add Another feature
8b05b54 Revert "Add Git is awesome"
0d3fcfa Add Git is awesome
e20f345 Initial commit
PS D:\git-studying\git-day9> Get-Content app.txt
<<<<<<< HEAD
Hello!
Another feature!
=======
Hello!
>>>>>>> parent of 0d3fcfa (Add Git is awesome)
PS D:\git-studying\git-day9> git status
On branch master
You are currently reverting commit 0d3fcfa.
  (fix conflicts and run "git revert --continue")
  (use "git revert --skip" to skip this patch)
  (use "git revert --abort" to cancel the revert operation)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both modified:   app.txt

no changes added to commit (use "git add" and/or "git commit -a")

Проверка понимания
Ответь без запуска команд:
1 Что делает git revert? - отменяет изменения предыдущего коммита, создавая новый коммит, не удаляя старый
2 Удаляет ли он отменяемый коммит из истории? - нет
3 Создаёт ли revert новый коммит? - да
4 Почему revert безопаснее для общей истории? - не удаляет коммиты, а создаёт новые с отменёнными изменениями
5 В чём главное отличие reset от revert? - первый переносит HEAD на предыдущий коммит, второй создаёт новый, отменяя изменения, но не трогая предыдущий
6 Что произойдёт, если отменяемый коммит изменил файл, который после него тоже меняли? - предупреждение
7 Как отменить последний коммит с помощью revert? - git revert --no-edit HEAD
8 Можно ли отменить конкретный старый коммит, не отменяя последний? - через хэш, но будет предупреждение в файле

Завершаем конфликт
Забыл скопировать и вставить, но всё сработало.

Финальное закрепление
Ответь на три вопроса после разрешения конфликта:
1 Почему Git не удалил Another feature!, когда ты отменял Add Git is awesome? - потому-что оно отновится к коммиту D
2 Для чего мы выполнили git add app.txt после разрешения конфликта? - чтобы по новой добавить в staging area окончательные изменения
3 Что делает git revert --continue? - продолжает незавершённый revert
Практика 1 — первый commit

Создай файл:

app.txt

Напиши:

Version 1

Затем:

git add app.txt
git commit -m "Initial version"

Проверь:

git log --oneline --decorate

Должно быть примерно:

abc1234 (HEAD -> main) Initial version

Ответ:
PS D:\git-studying\git-day2> git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
PS D:\git-studying\git-day2> git add app.txt
PS D:\git-studying\git-day2> git commit -m "Initial version"
[master (root-commit) d09b428] Initial version
 1 file changed, 1 insertion(+)
 create mode 100644 app.txt
PS D:\git-studying\git-day2> git log --oneline --decorate
d09b428 (HEAD -> master) Initial version

Практика 2 — создаём feature

Выполни:

git branch feature

Теперь:

git branch

Должно быть:

  feature
* main

Ответь себе:

Создался ли новый commit?

Нет.

Изменилась только структура указателей.

Было:

main → A

Стало:

main    → A
feature → A

Ответ:
PS D:\git-studying\git-day2> git branch feature
PS D:\git-studying\git-day2> git branch
  feature
* master

Практика 3 — переключаемся

Выполни:

git switch feature

Проверь:

git branch

Теперь:

* feature
  main

А затем:

git log --oneline --decorate

Получишь примерно:

abc1234 (HEAD -> feature, main) Initial version

Вот это очень важная строка.

И feature, и main пока указывают на один и тот же commit.

Ответ:
PS D:\git-studying\git-day2> git switch feature
Switched to branch 'feature'
PS D:\git-studying\git-day2> git branch
* feature
  master
PS D:\git-studying\git-day2> git log --oneline --decorate
d09b428 (HEAD -> feature, master) Initial version

Практика 4 — создаём новый commit в feature

Измени app.txt:

Version 1
Feature version

Затем:

git add app.txt
git commit -m "Add feature"

Посмотри:

git log --oneline --decorate

Получишь примерно:

def5678 (HEAD -> feature) Add feature
abc1234 (main) Initial version

Вот теперь произошло интересное.

abc1234 ← main

    ↓

def5678 ← feature
             ↑
            HEAD

feature ушла вперёд.

main осталась на старом commit.

Ответ:
PS D:\git-studying\git-day2> git add app.txt
PS D:\git-studying\git-day2> git commit -m "Add feature"
[feature c0ca038] Add feature
 1 file changed, 2 insertions(+), 1 deletion(-)
PS D:\git-studying\git-day2> git log --oneline --decorate
c0ca038 (HEAD -> feature) Add feature
d09b428 (master) Initial version

Практика 5 — переключаемся обратно

Выполни:

git switch main

Теперь:

git log --oneline --decorate

Ты должен увидеть:

abc1234 (HEAD -> main) Initial version

А commit def5678 не исчез.

Он всё ещё существует:

abc1234 ← main
    ↓
def5678 ← feature

Просто текущая ветка main на него не указывает.

Ответ:
PS D:\git-studying\git-day2> git switch master
Switched to branch 'master'
PS D:\git-studying\git-day2> git log --oneline --decorate
d09b428 (HEAD -> master) Initial version

🔥 Практика 6 — самое важное

Находясь в main, выполни:

git log --oneline --decorate --all

--all показывает историю всех refs, включая другие ветки.

Ты должен увидеть что-то вроде:

def5678 (feature) Add feature
abc1234 (HEAD -> main) Initial version

Это очень полезная команда для изучения истории.

Ответ:
PS D:\git-studying\git-day2> git log --oneline --decorate --all
c0ca038 (feature) Add feature
d09b428 (HEAD -> master) Initial version

Практика 7 — эксперимент

На main сейчас:

Version 1

На feature:

Version 1
Feature version

Переключись:

git switch feature

Посмотри содержимое app.txt.

Потом:

git switch main

Снова посмотри app.txt.

Ты должен увидеть разные версии файла.

Это и есть одно из практических преимуществ веток.

🧠 Контрольные вопросы

Не подглядывай в предыдущий текст. Ответь своими словами.

Вопрос 1

Что такое branch?

Не «место для кода».

Попробуй дать техническое определение.
Ответ:
Указатель на commit

Вопрос 2

Есть:

A → B → C
         ↑
        main

Выполнили:

git branch feature

Сколько новых commit появилось?
Ответ:
0, мы создали ветку, но не переключалиьс и не делали на ней commit

Вопрос 3

После:

git branch feature

где находятся main и feature?
Ответ:
Обе на C

Вопрос 4

Что делает:

git switch feature
Ответ:
Переключает ветку

Вопрос 5

Что означает:

HEAD -> feature
Ответ:
HEAD указывает что мы находимся в ветке feature

Вопрос 6

Есть:

A → B → C
         ↑
       main

Мы сделали:

git switch -c feature

А затем commit D.

Как будет выглядеть история?
Ответ:
A->B->C->D
      |   |
    MAIN feature

Вопрос 7

Почему после создания feature команда:

git branch feature

не создаёт commit?
Ответ:
Потому-что данная  команда создаёт только ветку

🔥 Задание повышенной сложности

Представь:

A → B → C
         ↑
       main

Создаём:

git switch -c feature

Получаем:

A → B → C
         ↑
   main  feature
           ↑
          HEAD

Делаем два commit:

D
E

Теперь история:

A → B → C → D → E
                  ↑
               feature

main всё ещё находится на C.

Теперь выполняем:

git switch main

Вопрос:

Где сейчас находятся:
HEAD? - указывает на main
main? - указывает на C
feature? - указывает на E
E? - в ветке feature

И самое главное:

Исчезли ли commits D и E после переключения на main? - нет, они просто остались в ветке feature

🥋 Финальный экзамен Дня 2

Ответь без командной подсказки:

1 Что такое branch в Git? - ветка, указатель на commit

2 Чем git branch feature отличается от git switch feature? - первая создаёт ветку, вторая переключает

3 Что делает git switch -c feature? - создаёт и сразу переключвет на созданную ветку

4 Что означает HEAD -> main? - указывает на какой ветке мы находимся

5 Почему после создания нового commit ветка перемещается вперёд? - потому-что ветка всегда двигается с коммитом

6 Если main находится на C, а feature на E, исчезнут ли D и E после git switch main? - ну по идее они останутся в feature

7 Объясни схему:

HEAD
 ↓
feature
 ↓
E

своими словами. - HEAD указывает на ветку feature, а feature указывает на commit E
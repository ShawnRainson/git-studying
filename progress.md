🥋 День 1 — Фундамент Git

Сегодня мы заложим основу, на которой будет строиться весь остальной курс.

К концу занятия ты должен не просто знать git add и git commit, а понимать:

что такое Git;
что такое репозиторий;
где Git хранит историю;
чем отличаются Working Directory, Staging Area и Repository;
что такое commit;
что такое HEAD;
что такое branch;
как читать историю;
как смотреть изменения;
как Git понимает, что именно изменилось.
1. Что вообще такое Git?

Представь, что ты пишешь программу.

Сегодня:

app.py

Завтра ты что-то изменил.

Послезавтра ещё что-то.

Через неделю программа сломалась.

И возникает вопрос:

«А что я изменил три дня назад?»

Без системы контроля версий можно получить:

app.py
app_old.py
app_final.py
app_final2.py
app_final_really.py
app_final_really_fixed.py

😄

Git решает эту проблему иначе.

Он позволяет создавать историю изменений:

Версия 1
   ↓
Версия 2
   ↓
Версия 3
   ↓
Версия 4

Каждая такая сохранённая точка называется commit.

2. Git — это не GitHub

Очень важно не путать:

Git — система контроля версий.

GitHub — сервис, который позволяет хранить Git-репозитории на сервере и работать с ними совместно.

Условно:

Git
│
├── commits
├── branches
├── history
├── merge
└── rebase

GitHub
│
├── хранение репозитория
├── Pull Requests
├── Code Review
└── совместная работа

Git прекрасно работает без GitHub.

Можно создать Git-репозиторий на компьютере и вообще не подключать его к интернету.

3. Репозиторий

Репозиторий — это проект, история которого отслеживается Git.

Допустим:

my-project/

    main.py
    config.py
    README.md

Выполняем:

git init

Git создаёт:

my-project/

    .git/
    main.py
    config.py
    README.md

.git — это специальная директория, в которой Git хранит информацию о репозитории.

Не удаляй .git, если хочешь сохранить историю. 😄

4. Три главных состояния Git

Это, пожалуй, самая важная концепция сегодняшнего дня.

У нас есть:

Working Directory
       ↓
Staging Area
       ↓
Repository

Разберём каждое.

5. Working Directory

Это твоя обычная рабочая папка.

Например:

project/

    main.py
    user.py
    README.md

Ты открываешь main.py и меняешь:

print("Hello")

на:

print("Hello, world!")

Изменение пока существует только в рабочей директории.

Git его видит, но commit ещё не создан.

6. Staging Area

Теперь выполняем:

git add main.py

Мы говорим Git:

«Вот это изменение я хочу включить в следующий commit».

Изменение перемещается в Staging Area.

Схема:

Working Directory
      │
      │ git add
      ↓
Staging Area

Важно:

git add не создаёт commit.

Он только подготавливает изменения.

7. Repository

Теперь:

git commit -m "Update main"

Git создаёт новый commit.

Получается:

Working Directory
      │
      │ git add
      ↓
Staging Area
      │
      │ git commit
      ↓
Repository

Вот эту схему нужно знать практически наизусть:

Изменил → add → commit

8. Что такое commit?

Commit — это сохранённая точка истории проекта.

Например:

commit A
↓
Добавил README

commit B
↓
Добавил авторизацию

commit C
↓
Исправил ошибку

commit D
↓
Добавил регистрацию

Каждый commit имеет уникальный идентификатор — hash.

Например:

dfe79b9b8d95e05183a98c13837649dfbdf8a260

Обычно в командах достаточно короткой версии:

dfe79b9
9. Commit — это не просто сообщение

Когда ты пишешь:

git commit -m "Добавил авторизацию"

строка:

Добавил авторизацию

— это commit message.

Но сам commit содержит гораздо больше информации:

изменения;
автора;
дату;
родительский commit;
hash;
метаданные.

Условно:

Commit
│
├── Hash
├── Author
├── Date
├── Message
├── Parent
└── Changes
10. git status

Одна из самых полезных команд Git:

git status

Она отвечает:

«Что сейчас происходит с моим репозиторием?»

Например:

On branch main

Changes not staged for commit:
    modified: main.py

Это значит:

main.py изменён, но ещё не добавлен в staging.

Другой вариант:

Changes to be committed:
    modified: main.py

Это значит:

изменение уже находится в staging и попадёт в следующий commit.

А:

Untracked files:
    test.py

означает:

Git видит новый файл, но пока его не отслеживает.

11. Untracked

Допустим, ты создал:

test.py

Git показывает:

Untracked files:
    test.py

Чтобы начать отслеживание:

git add test.py

После этого файл попадёт в staging.

12. git add .

Можно добавить все изменения:

git add .

Точка означает:

текущая директория и её содержимое.

Например:

main.py
user.py
README.md

После:

git add .

все подходящие изменения будут подготовлены к commit.

⚠️ Но помни:

git add .

не означает:

«создай commit».

Это означает:

«подготовь изменения».

13. git commit

Теперь:

git commit -m "Add user authentication"

Создаёт commit из того, что находится в staging.

Очень важно:

Если у тебя есть:

A.py
B.py
C.py

и ты сделал:

git add A.py

а потом:

git commit -m "Update A"

в commit попадёт только A.py.

B.py и C.py не попадут.

14. git diff

Теперь представим:

Последний commit содержит:

print("Hello")

Ты изменил файл:

print("Hello, world!")

Команда:

git diff

покажет разницу.

Например:

- print("Hello")
+ print("Hello, world!")

- означает удалённую строку.

+ означает добавленную строку.

15. git diff --staged

А теперь:

git add main.py

Изменение уже в staging.

Если выполнить:

git diff

может ничего не показаться.

Почему?

Потому что между:

Working Directory

и:

Staging Area

разницы уже нет.

Но:

git diff --staged

покажет:

Какие изменения сейчас находятся в staging и попадут в следующий commit?

16. Очень важная схема

Запомни:

                  git add
                     ↓
Working Directory → Staging Area
                         ↓
                      git commit
                         ↓
                     Repository

А теперь:

git diff
   ↓
Working Directory
       ↕
Staging Area

и:

git diff --staged
        ↓
Staging Area
       ↕
последний commit
17. git log

Теперь мы хотим посмотреть историю.

git log

Например:

commit dfe79b9...
Author: Alex
Date: ...

    Updated lesson.txt

commit 242af50...
Author: Alex
Date: ...

    Add lesson.txt

Ты видишь историю commit'ов.

18. git log --oneline

Полный git log иногда слишком подробный.

Поэтому:

git log --oneline

Например:

dfe79b9 Updated lesson.txt
242af50 Add lesson.txt
a915b5b Initial commit

Это один из самых удобных вариантов просмотра истории.

19. HEAD

Теперь появляется важное понятие.

HEAD — это указатель на текущую позицию в истории.

Например:

a915b5b
    ↓
242af50
    ↓
dfe79b9
    ↑
   HEAD

Ты сейчас находишься на dfe79b9.

Если выполнить:

git log --oneline

можно увидеть:

dfe79b9 (HEAD -> main) Updated lesson.txt

Это означает:

HEAD
 ↓
main
 ↓
dfe79b9
20. Что такое main?

main — это ветка.

Пока достаточно понимать её как имя одной линии истории.

Например:

main
 ↓
A
 ↓
B
 ↓
C

Позже мы посвятим веткам целый день и разберём их очень подробно.

21. git show

Если мы хотим посмотреть конкретный commit:

git show dfe79b9

Git покажет информацию о нём и изменения, которые этот commit внёс.

То есть:

git log
   ↓
Какие commits существуют?

git show dfe79b9
   ↓
Что было внутри этого commit?
22. Remote и origin

Если репозиторий связан с GitHub, появляется понятие remote.

Например:

origin

Обычно origin — имя удалённого репозитория.

Можно посмотреть:

git remote -v

Например:

origin  https://github.com/user/project.git
origin  https://github.com/user/project.git
23. origin/main

Это уже интереснее.

У тебя есть:

main

локально.

И:

origin/main

который представляет состояние ветки main на удалённом репозитории с точки зрения последнего полученного Git состояния.

Например:

origin/main
     ↓
     A
     ↓
     B

main
     ↓
     A
     ↓
     B
     ↓
     C

Git может сказать:

Your branch is ahead of 'origin/main' by 1 commit.

То есть:

У тебя локально есть один commit, которого пока нет на remote.

24. git push

Чтобы отправить локальные commits на удалённый репозиторий:

git push

Схема:

Твой компьютер
      │
      │ git push
      ↓
    GitHub
25. git clone

Если репозиторий уже существует на GitHub:

git clone <repository>

Git скачает его на компьютер.

Схема:

GitHub
   │
   │ git clone
   ↓
Компьютер
26. Что происходит при обычной работе?

Типичный цикл:

1. Изменил файл
        ↓
2. git status
        ↓
3. git diff
        ↓
4. git add
        ↓
5. git diff --staged
        ↓
6. git commit
        ↓
7. git log
        ↓
8. git push

Не обязательно каждый раз выполнять абсолютно все команды, но логика именно такая.

🧠 Теперь проверяем понимание

Не запускай терминал. Ответь своими словами.

Задание 1

У тебя есть:

hello.py

Ты изменил его.

Что произойдёт после:

git status
Задание 2

Ты выполнил:

git add hello.py

Что изменилось?

И главное:

создался ли commit?

Задание 3

В чём разница:

git add hello.py

и:

git commit -m "Update hello"
Задание 4

Что показывает:

git diff

?

Задание 5

Что показывает:

git diff --staged

?

Задание 6

Что такое commit?

Не просто:

«сохранение».

Попробуй объяснить чуть подробнее.

Задание 7

Что означает:

HEAD -> main

?

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

⌨️ Практика — создаём репозиторий

Теперь руки к клавиатуре. 😎

Создай отдельную папку для обучения:

mkdir git-day1
cd git-day1

Инициализируй Git:

git init

Проверь:

git status
Практика 1 — первый файл

Создай:

lesson.txt

Напиши:

Я изучаю Git.
Сегодня мой первый день.

Теперь:

git status

Посмотри, что Git говорит про файл.

Практика 2 — первый staging

Выполни:

git add lesson.txt

Теперь:

git status

Обрати внимание, как изменился статус файла.

После этого:

git diff

Что получилось?

Практика 3 — посмотрим staging

Выполни:

git diff --staged

Ты должен увидеть содержимое изменения, которое сейчас подготовлено к commit.

Практика 4 — первый commit

Теперь:

git commit -m "Add lesson.txt"

И:

git status

Репозиторий должен сообщить, что рабочее дерево чистое, если других изменений нет.

Практика 5 — изменяем файл

Теперь добавь в lesson.txt:

Я уже понимаю основы staging area.

Не делай git add.

Сначала:

git status

Потом:

git diff

Посмотри, что Git обнаружил.

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
Практика 7 — второй commit

Теперь:

git commit -m "Update lesson.txt"

После этого:

git log --oneline

Ты должен увидеть примерно:

XXXXXXXX Update lesson.txt
XXXXXXXX Add lesson.txt
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

git diff

и что будет содержать:

git diff --staged

?

Это очень важный вопрос. Если ты его поймёшь, staging area перестанет быть для тебя абстрактным понятием.

📝 Что нужно прислать мне

Чтобы не растягивать День 1 на несколько сообщений, можешь выполнить всю практику сразу, а затем отправить мне:

Теория

Ответы на:

Что делает git add?
Что делает git commit?
Что показывает git diff?
Что показывает git diff --staged?
Что такое commit?
Что такое HEAD?
Что означает HEAD -> main?
Что означает ahead of origin/main by 1 commit?
Практика

И результаты:

git status
git log --oneline

А также ответ на задание повышенной сложности с A.txt.

Я разберу твои ответы, исправлю неточности и, если всё усвоено, закроем День 1 и перейдём к Дню 2 — Branches. 🌳🥋
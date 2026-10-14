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

🥋 День 2 — Branches: ветки, HEAD и git switch

Сегодня наша цель — перестать воспринимать ветку как «копию проекта» и начать видеть её так, как Git видит её на самом деле:

Ветка — это указатель на commit.

После сегодняшнего дня ты должен понимать, что происходит с HEAD, когда мы создаём ветку, переключаемся между ветками и делаем новые commit.

1. 🎯 Цели дня

Сегодня изучим:

что такое branch;
зачем вообще нужны ветки;
почему ветка — это не отдельная копия проекта;
git branch;
git switch;
старый git checkout;
HEAD;
как branch указывает на commit;
почему ветки двигаются;
почему HEAD перемещается;
создание ветки;
переключение между ветками;
удаление ветки;
как читать вывод git log;
detached HEAD — пока только познакомимся с понятием.

В конце будет практическое задание и экзамен по Дню 2.

2. 🧠 Главная идея дня

Представим историю:

A → B → C

У нас есть ветка main.

Она указывает на C:

A → B → C
         ↑
       main

Теперь мы создаём новую ветку:

git branch feature

Получается:

A → B → C
         ↑
       main
         ↑
      feature

Обрати внимание:

нового commit не появилось.

Мы просто создали ещё один указатель на существующий commit.

3. 🔥 Что такое branch на самом деле?

Очень распространённая ошибка новичка:

«Ветка — это копия проекта».

Нет.

В Git ветка — это указатель на определённый commit.

Например:

A → B → C
         ↑
       main

main можно мысленно представить как бумажную стрелку:

main ───────→ C

Создаём:

git branch feature

Теперь:

main ───────→ C
feature ────→ C

Обе ветки указывают на один commit.

4. 🤔 Тогда зачем нужны ветки?

Представь, что у тебя есть рабочий проект:

main
  ↓
A → B → C

Ты хочешь добавить новую функцию.

Можно делать изменения прямо в main.

Но это неудобно.

Лучше создать:

feature

И работать там:

main
  ↓
A → B → C
         ↑
      feature

Теперь делаешь commit:

A → B → C → D
         ↑   ↑
       main feature

Важный момент:

main остался на C.

А feature переместился на D.

5. 🧩 Ветка движется вместе с commit

Это фундаментальный принцип.

До commit:

A → B → C
         ↑
       feature

Делаем:

git commit -m "Add feature"

Получаем:

A → B → C → D
             ↑
          feature

Ветка feature автоматически переместилась на новый commit.

Почему?

Потому что commit был создан, пока мы находились на ветке feature.

6. 👑 А где здесь HEAD?

Вот здесь начинается самое интересное.

HEAD — это специальный указатель Git, который говорит:

Где я сейчас нахожусь?

Например:

A → B → C
         ↑
       main
         ↑
        HEAD

Мы находимся в main.

Git показывает:

HEAD -> main
7. Переключаемся на feature

Предположим:

A → B → C
         ↑
       main
         ↑
      feature

Выполняем:

git switch feature

Теперь:

A → B → C
         ↑
       main
         ↑
      feature
         ↑
        HEAD

То есть:

HEAD → feature → C

Теперь текущая ветка — feature.

8. 🧠 Очень важная схема

Запомни:

HEAD
 ↓
branch
 ↓
commit

Например:

HEAD
 ↓
feature
 ↓
C

Или:

HEAD
 ↓
main
 ↓
C

HEAD обычно указывает на текущую ветку, а ветка указывает на commit.

9. git branch

Теперь переходим к командам.

Выполни:

git branch

Например, Git может показать:

* main

Звёздочка:

*

означает:

Это текущая ветка.

Если есть две ветки:

  feature
* main

мы сейчас в main.

Если:

* feature
  main

мы сейчас в feature.

10. Создание ветки

Команда:

git branch feature

создаёт ветку feature.

Но есть важный нюанс:

она не переключает тебя на неё.

Например:

git branch feature
git branch

Получим:

  feature
* main

Ветка создана.

Но мы всё ещё в main.

11. Переключение

Для переключения:

git switch feature

Теперь:

  main
* feature
12. Создать и сразу переключиться

Очень удобная команда:

git switch -c feature

Она делает сразу две вещи:

1. создаёт feature
2. переключается на feature

То есть вместо:

git branch feature
git switch feature

можно:

git switch -c feature
13. Почему существует git checkout?

Исторически Git использовал:

git checkout

для нескольких разных операций.

Например:

git checkout feature

переключает ветку.

А:

git checkout -b feature

создаёт и переключает на новую ветку.

Современный Git рекомендует разделять эти операции:

git switch feature

и:

git switch -c feature

Почему это удобно?

Потому что назначение команды становится очевиднее:

switch → переключиться
restore → восстановить файл

А старый checkout был своего рода «многофункциональной командой».

Мы ещё встретим checkout, но в новых командах будем преимущественно использовать switch.

14. 🥋 Практическая модель

Создадим историю:

A → B → C
         ↑
        main

Создадим feature:

A → B → C
         ↑
     main
     feature

Переключимся:

A → B → C
         ↑
     main
     feature
         ↑
        HEAD

Создадим новый commit:

A → B → C → D
         ↑   ↑
       main feature
             ↑
            HEAD

Переключимся обратно:

git switch main

Получим:

A → B → C → D
         ↑   ↑
       main feature
       ↑
      HEAD

Обрати внимание:

D никуда не исчез.

Он просто находится в истории feature, а main пока указывает на C.

15. 😈 А что произойдёт, если сделать commit в main?

Продолжим:

A → B → C → D
         ↑   ↑
       main feature

Мы в main.

Делаем новый commit:

A → B → C → E
         ↑   ↑
       feature main
               ↑
              HEAD

Теперь история выглядит так:

        D ← feature
       /
A → B → C
       \
        E ← main

Это называется расхождением веток.

И именно здесь ветки начинают становиться по-настоящему полезными.

16. 🌳 Почему Git называют распределённой системой контроля версий?

Потому что история проекта может выглядеть как дерево:

             D ← feature
            /
A → B → C
            \
             E ← main

Позже эти линии можно объединить через merge.

Но merge мы подробно изучим завтра, в День 3.

Сегодня наша задача — научиться уверенно создавать и переключать ветки.

17. 🔍 git log --oneline --decorate

Сегодня добавим полезный вариант log:

git log --oneline --decorate

Например:

8f32abc (HEAD -> feature) Add login
91ab234 (main) Initial project

Это очень информативно.

Можно увидеть:

8f32abc
   ↑
commit

HEAD -> feature
   ↑
мы сейчас на feature

91ab234
   ↑
commit

main
   ↑
main сейчас указывает сюда
18. --decorate — что это?

--decorate позволяет показывать указатели около commit:

(HEAD -> feature)
(main)
(origin/main)

Например:

abc1234 (HEAD -> feature) Add login
def5678 (main) Initial commit

Можно буквально читать:

HEAD находится на feature, а feature находится на abc1234.

19. 🧠 Важное различие: branch ≠ commit

Это очень важно.

Если ты говоришь:

«Я нахожусь в commit abc1234»

это не обязательно означает, что ты находишься на ветке.

В обычной ситуации:

HEAD
 ↓
main
 ↓
abc1234

Но существует особый режим:

HEAD
 ↓
abc1234

без ветки.

Это называется:

Detached HEAD

Сегодня мы только познакомимся с ним.

Подробно разберём позже, когда будем изучать историю Git.

20. ⚠️ Detached HEAD

Представим:

A → B → C
         ↑
       main

Ты выполняешь:

git switch --detach B

Теперь:

A → B → C
    ↑   ↑
   HEAD main

HEAD больше не указывает на ветку.

Он непосредственно указывает на commit.

Поэтому:

HEAD → B

а не:

HEAD → main → B

Это называется detached HEAD.

Пока просто запомни:

Обычный режим: HEAD → branch → commit
Detached HEAD: HEAD → commit

Подробно разберём позже.

21. 🗑️ Удаление ветки

Когда ветка больше не нужна:

git branch -d feature

Git удалит локальную ветку feature, если считает, что её изменения уже не потеряются.

Есть и принудительное удаление:

git branch -D feature

Но с -D надо быть осторожным.

Почему?

Потому что ты можешь удалить указатель на commit, который больше не доступен через другую ветку.

Мы пока будем использовать:

git branch -d
22. ⚠️ Ветка не содержит отдельную копию файлов

Это очень важно.

Когда ты делаешь:

git branch feature

Git не создаёт:

project/
├── main-copy/
└── feature-copy/

Нет.

Есть одна история commit и дополнительные указатели:

          main
            ↓
A → B → C
            ↑
         feature

Это намного эффективнее.

23. 🧪 Практика — создаём лабораторию

Теперь руки к клавиатуре. 😎

Для этой практики рекомендую использовать отдельный чистый репозиторий, чтобы старые изменения из D:\git-studying не мешали.

В PowerShell:

cd D:\git-studying
mkdir git-day2
cd git-day2
git init

Проверь:

git status

Должно быть примерно:

On branch main

No commits yet

nothing to commit
24. Практика 1 — первый commit

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
25. Практика 2 — создаём feature

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
26. Практика 3 — переключаемся

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

27. Практика 4 — создаём новый commit в feature

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

28. Практика 5 — переключаемся обратно

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

29. 🔥 Практика 6 — самое важное

Находясь в main, выполни:

git log --oneline --decorate --all

--all показывает историю всех refs, включая другие ветки.

Ты должен увидеть что-то вроде:

def5678 (feature) Add feature
abc1234 (HEAD -> main) Initial version

Это очень полезная команда для изучения истории.

30. Практика 7 — эксперимент

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

31. 🧠 Контрольные вопросы

Не подглядывай в предыдущий текст. Ответь своими словами.

Вопрос 1

Что такое branch?

Не «место для кода».

Попробуй дать техническое определение.

Вопрос 2

Есть:

A → B → C
         ↑
        main

Выполнили:

git branch feature

Сколько новых commit появилось?

Вопрос 3

После:

git branch feature

где находятся main и feature?

Вопрос 4

Что делает:

git switch feature
Вопрос 5

Что означает:

HEAD -> feature
Вопрос 6

Есть:

A → B → C
         ↑
       main

Мы сделали:

git switch -c feature

А затем commit D.

Как будет выглядеть история?

Вопрос 7

Почему после создания feature команда:

git branch feature

не создаёт commit?

32. 🔥 Задание повышенной сложности

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
HEAD?
main?
feature?
E?

И самое главное:

Исчезли ли commits D и E после переключения на main?

🥋 Финальный экзамен Дня 2

Ответь без командной подсказки:

1. Что такое branch в Git?

2. Чем git branch feature отличается от git switch feature?

3. Что делает git switch -c feature?

4. Что означает HEAD -> main?

5. Почему после создания нового commit ветка перемещается вперёд?

6. Если main находится на C, а feature на E, исчезнут ли D и E после git switch main?

7. Объясни схему:

HEAD
 ↓
feature
 ↓
E

своими словами.

🧘 Главная мантра Дня 2

Запомни её:

Branch — это указатель на commit.
HEAD — указатель на текущую ветку.
Commit двигает текущую ветку вперёд.

И ещё одна:

HEAD → branch → commit

Если эта модель станет для тебя естественной, merge, rebase, cherry-pick и даже сложные конфликты позже будут значительно понятнее.

Жду твои ответы на контрольные вопросы + выводы команд из практики, ученик. 🥋

🥋 DAY 3 — MERGE
🎯 Цель дня
К концу занятия ты должен понимать:
- что делает git merge;
- что такое Fast-Forward merge;
- что такое Three-Way Merge;
- когда появляется merge commit;
- почему при merge одна ветка «вливается» в другую;
- как читать историю после merge;
- почему git merge не переносит тебя автоматически на другую ветку;
- чем merge отличается от обычного git switch.
1. 🧠 Теория — зачем вообще нужен Merge?
Вчера мы научились создавать ветки.
У нас была примерно такая история:
A
│
B ← master

Создали feature:
A
│
B ← master
  ↑
feature

Затем сделали коммит в feature:
A
│
B ← master
 \
  C ← feature

Теперь представь, что работа над feature закончена.
Мы хотим получить её изменения в master.
Вот для этого существует:
git merge

То есть:
Merge объединяет историю текущей ветки с другой веткой.

Например:
git switch master
git merge feature

Здесь очень важно:
Мы находились на master.
Поэтому именно master является веткой, в которую мы вливаем feature.
2. 🔥 Самая важная мысль сегодняшнего дня
Запомни:
git merge feature

не означает:
«Переключись на feature».

И не означает:
«Сделай feature главной».

Это означает:
«Возьми изменения из feature и объедини их с той веткой, на которой я сейчас нахожусь».

Например:
A──B──C
    ↑  ↑
 master feature

Если выполнить:
git switch master
git merge feature

Git объединяет feature в master.
3. 🌿 Первый тип merge — Fast-Forward
Начнём с самого простого случая.
Представим:
A
│
B ← master
 \
  C ← feature

На самом деле здесь master просто находится позади feature.
История выглядит так:
A ── B ── C
     ↑    ↑
   master feature

Если feature содержит все коммиты master плюс несколько новых, Git может просто передвинуть указатель master.
До:
A ── B ── C
     ↑    ↑
   master feature

После:
A ── B ── C
          ↑
       master
       feature

Никакого нового коммита не создаётся.
Это называется:
Fast-Forward
То есть буквально:
«быстро перемотать указатель вперёд».

4. 🧠 Почему это возможно?
Потому что Git видит:
master
   ↓
   B
   │
   C
   ↑
feature

B является прямым предком C.
Поэтому Git говорит:
«Зачем мне создавать дополнительный commit? Просто передвину master на C.»

И всё.
5. 🧪 Практика №1 — Fast-Forward
Создай новый репозиторий:
D:\git-studying\git-day3

Перейди в него:
cd D:\git-studying\git-day3

Инициализируй:
git init

Проверь:
git status

У тебя, скорее всего, снова будет:
On branch master

Это нормально.
Создаём первый коммит
Создай файл:
app.txt

Содержимое:
Version 1

Затем:
git add app.txt
git commit -m "Initial version"

Проверь:
git log --oneline --decorate

Будет примерно:
A1B2C3D (HEAD -> master) Initial version

6. Создаём feature
Теперь:
git switch -c feature

Проверь:
git branch

Должно быть:
* feature
  master

Добавь в app.txt:
Version 1
Feature version

Сделай commit:
git add app.txt
git commit -m "Add feature"

Теперь:
git log --oneline --decorate --all

Примерно:
B2B2B2B (HEAD -> feature) Add feature
A1A1A1A (master) Initial version

И визуально:
A ── B
↑    ↑
master feature

7. 🔥 Теперь сам Merge
Переключаемся на master:
git switch master

Проверяем:
git log --oneline --decorate --all

Теперь:
B2B2B2B (feature) Add feature
A1A1A1A (HEAD -> master) Initial version

Теперь выполняем:
git merge feature

Git, скорее всего, напишет что-то вроде:
Fast-forward

После этого:
git log --oneline --decorate --all

Получим:
B2B2B2B (HEAD -> master, feature) Add feature
A1A1A1A Initial version

Обрати внимание! 👀
Раньше:
A ── B
↑    ↑
master feature

После merge:
A ── B
     ↑
     master
     feature

Новый commit не появился.
Git просто передвинул master.
8. ⚠️ Очень важный нюанс
Многие новички думают:
«Merge всегда создаёт новый commit».

❌ Нет.
Возможны разные варианты.
Первый:
Fast-Forward
A ── B
     ↑
master
feature

Нового commit нет.
Второй:
Three-Way Merge
Может появиться отдельный merge commit:
       C ── D
      /      \
A ── B        M
      \      /
       E ── F

Вот это уже гораздо интереснее.
9. 🧠 Three-Way Merge
Представим, что после создания feature мы продолжаем работать и в master, и в feature.
Получаем:
        C ← feature
       /
A ── B
       \
        D ← master

То есть ветки разошлись.
master получил свой commit:
D

feature получила свой:
C

Теперь Git не может просто передвинуть указатель.
Почему?
Потому что:
master → D
feature → C

Обе ветки содержат уникальные коммиты.
Git должен объединить две линии истории.
10. 🔀 Merge Commit
Когда Gitу нужно объединить такие истории, он может создать специальный commit:
        C
       / \
A ── B   M ← master
       \ /
        D

M — merge commit.
И вот здесь появляется очень важная особенность:
Обычный commit обычно имеет одного родителя:
B → A

А merge commit имеет двух родителей:
M
↙ ↘
C   D

То есть он говорит:
«Я объединяю две линии истории».

11. 🧠 Почему называется Three-Way Merge?
Git рассматривает три точки:
             feature
                ↓
                C
               /
              B  ← общий предок
               \
                D
                ↑
              master

Git сравнивает:
1. общий предок — B;
2. состояние feature — C;
3. состояние master — D.
Отсюда:
Three-Way Merge

Три состояния участвуют в объединении.
Это очень важно понять перед следующим днём, потому что Day 4 будет посвящён конфликтам.
12. 🥋 Практика №2 — настоящий Three-Way Merge
Теперь создадим ситуацию, где Git действительно должен будет объединить две ветки.
У нас уже есть:
A ── B

После предыдущего упражнения у тебя, скорее всего:
A ── B
     ↑
master
feature

Нам нужно сделать так, чтобы обе ветки получили свои собственные коммиты.
Шаг 1
На master измени app.txt:
Version 1
Master version

Сделай:
git add app.txt
git commit -m "Update master"

Теперь:
        feature
           ↓
A ── B ── C
     ↑
   master

Стоп — здесь направление не такое, потому что master получил новый commit.
Правильная схема:
A ── B ── C ← master
     \
      D ← feature

Но нам сначала нужно перейти в feature и сделать там отдельный commit.
Шаг 2
Переключись:
git switch feature

Измени app.txt, например:
Version 1
Feature version

И:
git add app.txt
git commit -m "Update feature"

Теперь история:
        C ← master
       /
A ── B
       \
        D ← feature

13. 🔥 Теперь самое главное
Переключись:
git switch master

И выполни:
git merge feature

Git должен создать merge commit или, если изменения затронули одни и те же строки, остановиться на конфликте.
Мы пока не будем глубоко разбирать конфликт — это тема Day 4.
Но если Git создаст merge commit, история будет примерно:
        C ──┐
       /    │
A ── B      M ← master
       \    │
        D ──┘

Проверь:
git log --oneline --decorate --graph --all

Вот эта команда сегодня особенно полезна:
git log --oneline --decorate --graph --all

Она позволит увидеть структуру ветвления прямо в терминале.
14. 🎨 Очень важная команда
Запомни:
git log --oneline --decorate --graph --all

Например:
*   7f123ab (HEAD -> master) Merge branch 'feature'
|\
| * 91abcde (feature) Update feature
* | 82def12 Update master
|/
* 1234567 Initial version

Теперь ты буквально видишь историю.
       Update master
      /
Initial
      \
       Update feature
             \
            Merge

15. 🧠 Ещё один важный нюанс
Когда ты выполняешь:
git merge feature

текущая ветка не меняется.
Например:
git switch master
git merge feature

После merge ты всё ещё находишься:
master

а не:
feature

Это принципиально важно.
Merge означает:
«Влить feature в текущую ветку»

а не:
«Перейти на feature».

16. 🥋 Ментальная модель
Хочу, чтобы у тебя в голове закрепилась такая картинка.
Branch
Это указатель:
master ──→ C

HEAD
Указывает на текущую ветку:
HEAD ──→ master ──→ C

Merge
Говорим:
git switch master
git merge feature

То есть:
             feature
                ↓
A ── B ──────── C
     ↑
   master

Git пытается сделать:
feature
   ↓
   C
  / \
 B   ...
 ↑
master

Если возможно просто передвинуть master → Fast-Forward.
Если ветки разошлись → Git объединяет две линии → Merge Commit.
17. ⚠️ Важные нюансы
Нюанс №1
git merge работает с текущей веткой.
git switch master
git merge feature

→ feature вливается в master.
Нюанс №2
Fast-Forward не создаёт новый commit.
A ── B
     ↑
 master
 feature

Нюанс №3
Если истории разошлись, может появиться merge commit.
      C
     / \
A ── B  M
     \ /
      D

Нюанс №4
Merge commit может иметь двух родителей.
Это одна из причин, почему Git способен хранить сложную структуру истории.
Нюанс №5
git merge не удаляет ветку.
После:
git merge feature

ветка feature всё ещё существует.
Удалять её можно отдельно:
git branch -d feature

Но сегодня этого делать не надо.
🧪 18. Проверка понимания
Не спеши смотреть ниже — сначала ответь сам. 🥋
Вопрос 1
Есть:
A ── B
     ↑
   master

Создали feature, сделали один commit:
A ── B ── C
     ↑    ↑
   master feature

Выполняем:
git switch master
git merge feature

Создастся ли новый merge commit? Почему?
Вопрос 2
Что делает:
git merge feature

если ты находишься на master?
Вопрос 3
После:
git switch master
git merge feature

на какой ветке ты останешься?
Вопрос 4
Чем отличается:
Fast-Forward
от
Three-Way Merge?
Вопрос 5
Почему в Three-Way Merge может появиться специальный merge commit?
🥋 19. Практическое задание дня
После теории выполни в git-day3:
Часть A
Создай:
A — Initial version

Часть B
Создай feature и сделай в ней commit.
Часть C
Сделай merge feature в master.
Часть D
Создай ситуацию, где master и feature разойдутся, то есть обе ветки получат свои коммиты.
Часть E
Сделай второй merge.
Часть F
Покажи:
git log --oneline --decorate --graph --all

И обязательно выполни:
git status

📝 20. Финальный экзамен Day 3
Ответь своими словами, без поиска:
1. Что такое git merge?
2. Что означает Fast-Forward?
3. Почему при Fast-Forward не создаётся новый commit?
4. Что такое merge commit?
5. Сколько родителей может иметь обычный commit? А merge commit?
6. Почему Three-Way Merge называется именно так?
7. Если я нахожусь на master и выполняю:
git merge feature

какая ветка является целевой?
8. После git merge feature я автоматически перейду на feature?
9. Удаляется ли feature после успешного merge?
10. Объясни своими словами разницу между:
A ── B ── C

и
      C ──┐
     /    │
A ── B    M
     \    │
      D ──┘

🥋 Главное правило сегодняшнего дня
Запомни одну фразу:
git merge X — это «влить X в текущую ветку».

И вторую:
Fast-Forward — просто передвинули указатель. Three-Way Merge — объединили две разошедшиеся линии истории.

Когда выполнишь практику, пришли мне вывод git log --oneline --decorate --graph --all и ответы на экзамен. Я разберу их как сэнсэй: где всё идеально, где есть неточность, и после этого засчитаем Day 3. 🥋

🥋 DAY 4 — MERGE CONFLICTS







opennana.com


Этап 1 · Основы Git · Урок 4 из 20
🎯 Цель дня
К концу занятия ты должен уметь:
- объяснить, почему возникают конфликты;
- читать конфликтные маркеры в файлах;
- понимать, что означают HEAD, ======= и >>>>>>>;
- самостоятельно разрешать конфликт;
- завершать merge после исправления файла;
- отменять незавершённое слияние через git merge --abort;
- проверять результат с помощью git status, git diff и git log.

1. 🧠 Теория: что такое Merge Conflict?
Вспомним прошлый урок. Мы научились объединять ветки:
git switch master
git merge feature


Иногда Git может объединить изменения автоматически. Но иногда он останавливается и сообщает:
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed; fix conflicts and then commit the result.


Что произошло?
Представь, что после общего коммита обе ветки изменили одну и ту же строку файла.
Общий предок
Version 1



Ветка master
Version 1
Master version




Ветка feature
Version 1
Feature version





Обе ветки изменили одну и ту же область файла по-разному.

Git может определить, какие изменения были внесены в каждой ветке, но не всегда способен понять, какой вариант ты считаешь правильным.
Он не знает, что важнее: Master version, Feature version или обе строки сразу.
Поэтому Git останавливается и просит тебя принять решение.
Merge conflict — это ситуация, когда Git не может автоматически согласовать изменения.
Важная тонкость: конфликт может возникнуть не только при изменении одной строки. Например, одна ветка может удалить файл, а другая изменить его. Но сегодня сосредоточимся на конфликтах содержимого файлов.

2. 🔍 Как выглядят конфликтные маркеры?
Когда Git обнаруживает конфликт, он может записать в файл примерно следующее:
Version 1
<<<<<<< HEAD
Master version
=======
Feature version
>>>>>>> feature


Это не обычный текст твоего приложения. Git временно вставил специальные маркеры, чтобы показать конфликтующие варианты.
Разберём каждую часть.
<<<<<<< HEAD
Начало конфликтующего блока со стороны текущей ветки.
В нашем примере мы выполняли:
git switch master
git merge feature


Поэтому HEAD относится к текущей ветке master.
=======
Разделяет два конфликтующих варианта.
Всё выше разделителя — одна сторона, всё ниже — другая.
>>>>>>> feature
Показывает конец блока со стороны вливаемой ветки feature.
Итого:
<<<<<<< HEAD
Master version
=======
Feature version
>>>>>>> feature


Читается так:
- текущая ветка предлагает Master version;
- вливаемая ветка предлагает Feature version;
- Git не знает, какой вариант оставить.
Запомни: HEAD здесь обозначает текущую сторону слияния, а не обязательно «самую новую» или «самую правильную» версию.

3. 🥋 Как правильно разрешать конфликт?
Есть три основных шага:
1. Изучить конфликт. Понять, что изменилось в обеих ветках и какой результат нужен.
2. Отредактировать файл. Оставить нужное содержимое и удалить все конфликтные маркеры.
3. Добавить исправленный файл в Staging Area и завершить merge. Для этого используются git add и git commit.
Допустим, мы решили сохранить обе строки:
Version 1
Master version
Feature version


Тогда нужно полностью удалить:
<<<<<<< HEAD
=======
>>>>>>> feature


А также оставить только тот текст, который должен попасть в итоговый файл.
Можно выбрать только одну сторону, объединить обе или написать совершенно новый вариант. Главное — результат должен отражать твоё решение.
После редактирования файл должен содержать обычный текст, без маркеров.

4. 🧪 Практика №1 — разрешаем твой настоящий конфликт
У тебя в D:\git-studying\git-day3 уже возник конфликт в app.txt.
Ранее ты получил:
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed


Это означает, что merge начался, но пока не завершился.
Шаг 1. Проверяем состояние
В PowerShell, находясь в D:\git-studying\git-day3, выполни:
git status


При незавершённом merge ты увидишь сообщение примерно такого вида:
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")


И файл app.txt будет указан как конфликтующий.
Теперь:
git diff


Эта команда поможет увидеть конфликтующие изменения. Открой также сам app.txt в редакторе.
Шаг 2. Изучаем содержимое
Судя по твоим предыдущим командам, в master ты записал:
Version 1
Master version


А в feature:
Version 1
Feature version


Если эти данные совпадают с тем, что ты видишь в файле, конфликтный блок будет похож на:
Version 1
<<<<<<< HEAD
Master version
=======
Feature version
>>>>>>> feature


Если содержимое отличается, ориентируйся на фактический текст в своём файле.
Шаг 3. Исправляем app.txt
Открой файл в редакторе и замени конфликтный блок на:
Version 1
Master version
Feature version


Сохрани файл.
Почему мы оставили обе строки? Для упражнения мы хотим сохранить изменения обеих веток. В реальном проекте решение зависит от смысла кода: иногда объединять обе версии нельзя, и нужно выбрать одну или написать корректный третий вариант.
Шаг 4. Проверяем исправление
Выполни:
git diff


Затем:
git status


Файл пока ещё может отображаться как неразрешённый конфликт. Это нормально: Git не считает, что конфликт разрешён, пока ты не добавишь исправленный файл в индекс.
Шаг 5. Отмечаем конфликт разрешённым
Выполни:
git add app.txt


И снова:
git status


Теперь app.txt должен исчезнуть из списка неразрешённых путей. Git обычно сообщает, что все конфликты исправлены и слияние можно завершить.
Важный нюанс: git add здесь не просто «добавляет файл». Команда помещает исправленную версию в Staging Area и тем самым сообщает Git, что конфликт в этом файле разрешён.
Шаг 6. Завершаем merge
Теперь:
git commit


Git может открыть редактор с подготовленным сообщением merge-коммита. Оставь сообщение по умолчанию и сохрани его, если редактор открылся.
Если редактор не открылся или Git сразу завершил коммит, проверь результат:
git status


И затем:
git log --oneline --decorate --graph --all


При успешном merge у тебя появится merge commit, у которого два родителя — коммиты двух объединившихся веток.
Упрощённо история будет выглядеть так:
*   M (HEAD -> master) Merge branch 'feature'
|\
| * F (feature) Feature app V2
* | D Master app
|/
* B Initial feature versuin
* A Initial version


Буквы M, F, D, B и A — условные обозначения коммитов, а не настоящие хеши.

5. 🔎 Что происходит внутри Git во время конфликта?
Во время merge Git использует общий предок и две вершины веток, чтобы вычислить итоговые изменения.
Если объединение не удаётся завершить автоматически, Git сохраняет состояние незавершённого слияния и позволяет тебе исправить конфликт.
До завершения merge ситуация выглядит примерно так:
             F ← feature
            /
A ── B ────
            \
             D ← master


Git пытается создать объединяющий коммит:
             F ──┐
            /    │
A ── B ─────     M ← master
            \    │
             D ──┘


Но пока конфликт не разрешён, M ещё не создан.
После исправления файла, git add app.txt и git commit merge завершается.
Почему нельзя сразу делать обычный commit?
Технически завершение merge как раз требует коммита, но сначала Git должен получить разрешённую версию каждого конфликтующего файла. Пока конфликт не разрешён, команда git commit обычно откажется завершать merge и попросит исправить конфликтующие пути.

6. 🧯 Как отменить незавершённый merge?
Представь, что ты начал merge, но передумал и хочешь вернуться к состоянию до его начала.
Если merge ещё не завершён, обычно можно выполнить:
git merge --abort


Эта команда пытается отменить текущую операцию слияния и восстановить состояние до её начала.
Проверь:
git status


Важно: git merge --abort не предназначен для отмены уже завершённого merge-коммита. Кроме того, если до начала merge были незакоммиченные изменения, восстановление может быть сложнее. Поэтому лучше начинать merge с чистого рабочего дерева.
В твоём текущем упражнении мы хотим научиться разрешать конфликт, поэтому не запускай git merge --abort — заверши практику через редактирование, git add и git commit.

7. ⚠️ Частые ошибки новичков
Ошибка №1. Оставить конфликтные маркеры в файле
Если в app.txt останутся:
<<<<<<< HEAD
=======
>>>>>>> feature


это не означает, что Git автоматически исправит файл при коммите.
Git может позволить добавить файл в индекс, даже если маркеры остались. Он не понимает смысл содержимого твоего приложения, поэтому проверяй файл вручную.
Ошибка №2. Сразу запускать git merge повторно
Если merge уже остановился на конфликте, второй запуск обычно не нужен. Сначала разреши или отмени текущий merge.
Ошибка №3. Думать, что git add создаёт коммит
Нет.
git add app.txt


помещает исправленную версию файла в Staging Area.
А:
git commit


завершает слияние, создавая merge commit.
Ошибка №4. Думать, что Git всегда выбирает текущую ветку
Нет. В конфликте Git не принимает за тебя смысловое решение. Текущая ветка обозначается HEAD, но ты можешь сохранить её версию, версию вливаемой ветки, обе версии или иной корректный вариант.
Ошибка №5. Путать merge conflict с неудачей Git
Конфликт — нормальная часть совместной разработки. Git не обязательно сломался: он остановился, потому что ему нужно твоё решение.

8. 🧠 Команды дня — краткая шпаргалка
Команда	Назначение
git status	Проверить состояние merge и список конфликтующих файлов
git diff	Посмотреть незастейдженные изменения, в том числе конфликтные
git diff --staged	Посмотреть изменения, уже добавленные в индекс
git add app.txt	Отметить исправленный файл как разрешённый
git commit	Завершить merge, создав коммит
git merge --abort	Отменить незавершённое слияние
git log --oneline --decorate --graph --all	Посмотреть историю и структуру веток

9. 🧪 Практика №2 — самостоятельное закрепление
После успешного завершения первого конфликта сделаем второй эксперимент. Чтобы не усложнять задачу, используй тот же репозиторий, но сначала убедись, что первый merge завершён и рабочее дерево чистое:
git status


Ожидаемый результат:
nothing to commit, working tree clean


Теперь создадим новую ветку:
git switch -c feature-conflict


Измени app.txt, заменив строку Master version на:
Feature conflict version


Сохрани файл и выполни:
git add app.txt
git commit -m "Change master line in feature"


Вернись в master:
git switch master


Измени ту же строку Master version на:
Master conflict version


Сохрани и выполни:
git add app.txt
git commit -m "Change master line"


Теперь выполни:
git merge feature-conflict


Если обе ветки изменили одну и ту же строку несовместимым образом, Git должен остановиться на конфликте.
Посмотри файл и самостоятельно разреши его, например, выбрав такой итог:
Version 1
Master conflict version
Feature conflict version
Feature version


Это лишь учебный пример: убедись, что итог соответствует фактическому содержимому твоего файла и что ты намеренно оставляешь нужные строки.
Затем:
git add app.txt
git commit


В конце проверь:
git status
git log --oneline --decorate --graph --all


Если у тебя получилась другая структура файла или Git объединил изменения автоматически, не пытайся искусственно создавать конфликт любой ценой — это тоже полезный результат, который можно разобрать.

10. 🥋 Проверка понимания
Сначала ответь на вопросы своими словами.
Вопрос 1. Почему Git не всегда может разрешить конфликт автоматически?
Вопрос 2. Что означает <<<<<<< HEAD?
Вопрос 3. Что означает =======?
Вопрос 4. Что означает >>>>>>> feature?
Вопрос 5. После ручного исправления файла почему нужно выполнить git add?
Вопрос 6. Какая команда завершает незавершённый merge после разрешения всех конфликтов?
Вопрос 7. Чем отличается git merge --abort от git commit во время слияния?
Вопрос 8. Может ли Git принять файл с оставшимися конфликтными маркерами в индекс? Почему всё равно важно проверять файл?
Вопрос 9. Если ты находишься на master и выполняешь git merge feature, какая сторона обозначается HEAD в обычном конфликтном блоке?
Вопрос 10. Объясни своими словами весь процесс от появления CONFLICT до успешного merge commit.

11. 🏆 Финальный экзамен Day 4
Теперь более практические ситуации.
Задача A
Git сообщает:
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed


Какие три основных действия ты предпримешь, чтобы завершить merge?
Задача B
В файле осталось:
<<<<<<< HEAD
Hello from master
=======
Hello from feature
>>>>>>> feature


Ты хочешь сохранить только Hello from feature. Как должен выглядеть итоговый файл?
Задача C
Ты выполнил:
git add app.txt
git status


Файл больше не отображается как конфликтующий, но merge ещё не завершён. Что нужно сделать дальше?
Задача D
Ты начал merge, возник конфликт, и решил полностью отменить операцию. Какую команду использовать, если merge ещё не завершён?
Задача E
Почему команда git add app.txt сама по себе не гарантирует, что конфликт разрешён правильно?

🥋 Правило дня
Git объединяет изменения, но решение о смысле конфликтующего кода остаётся за разработчиком.

Сегодня твоя задача — завершить практику №1 в git-day3, выполнить практику №2, а затем прислать мне вывод:
git status
git log --oneline --decorate --graph --all


И ответы на экзамен. Я проверю их, укажу на неточности и после этого засчитаем Day 4. Осу, ученик! 🥋
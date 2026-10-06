🧪 Практика №1 — Fast-Forward
PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Initial version"
[master (root-commit) 199a7b8] Initial version
 1 file changed, 1 insertion(+)
 create mode 100644 app.txt
PS D:\git-studying\git-day3> git log --oneline --decorate
199a7b8 (HEAD -> master) Initial version

Создаём feature
PS D:\git-studying\git-day3> git branch feature
PS D:\git-studying\git-day3> git switch feature
Switched to branch 'feature'
PS D:\git-studying\git-day3> git branch
* feature
  master
PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Initial feature versuin"
[feature 0f3c54a] Initial feature versuin
 1 file changed, 1 insertion(+)
PS D:\git-studying\git-day3> git log --oneline --decorate --all
0f3c54a (HEAD -> feature) Initial feature versuin
199a7b8 (master) Initial version

🔥 Теперь сам Merge
PS D:\git-studying\git-day3> git switch master
Switched to branch 'master'
PS D:\git-studying\git-day3> git log --oneline --decorate --all
0f3c54a (feature) Initial feature versuin
199a7b8 (HEAD -> master) Initial version
PS D:\git-studying\git-day3> git merge feature
Updating 199a7b8..0f3c54a
Fast-forward
 app.txt | 1 +
 1 file changed, 1 insertion(+)
PS D:\git-studying\git-day3> git log --oneline --decorate --all
0f3c54a (HEAD -> master, feature) Initial feature versuin
199a7b8 Initial version

🥋 Практика №2 — настоящий Three-Way Merge
PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Master app"
[master bf3571d] Master app
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day3> git switch feature
Switched to branch 'feature'
PS D:\git-studying\git-day3> git add app.txt
PS D:\git-studying\git-day3> git commit -m "Feature app V2"
[feature b16309c] Feature app V2
 1 file changed, 1 insertion(+), 1 deletion(-)
PS D:\git-studying\git-day3> git switch master
Switched to branch 'master'
PS D:\git-studying\git-day3> git branch
  feature
* master
PS D:\git-studying\git-day3> git merge feature
Auto-merging app.txt
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed; fix conflicts and then commit the result.
PS D:\git-studying\git-day3> git log --oneline --decorate --all
b16309c (feature) Feature app V2
bf3571d (HEAD -> master) Master app
PS D:\git-studying\git-day3> git log --oneline --decorate --graph --all

* b16309c (feature) Feature app V2
| * bf3571d (HEAD -> master) Master app

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

Создастся ли новый merge commit? Почему? - нет, просто master сдвигается туда где сейчас feature

Вопрос 2
Что делает:
git merge feature

если ты находишься на master? - переводит master на ту же позицию где и feature, добавляя изменения из feature

Вопрос 3
После:
git switch master
git merge feature

на какой ветке ты останешься? - master

Вопрос 4
Чем отличается:
Fast-Forward - слияние веток, не изменённая ветка получает изменения из изменённой
от
Three-Way Merge? - слияние двух параллельно изменённых веток

Вопрос 5
Почему в Three-Way Merge может появиться специальный merge commit? - потому-что ветки разошлись и просто переместить одну на тот же коммит где и другая уже нельзя.

Финальный экзамен Day 3
Ответь своими словами, без поиска:
1 Что такое git merge? - команда для слияния двух веток
2 Что означает Fast-Forward? - сдвиг неизменённой ветки вперёд на коммит изменённой
3 Почему при Fast-Forward не создаётся новый commit? - в этом нет смысла, так как изменения были лишь в одной ветке и грубо говоря Git просто добавляет те же зимения в неизменённую ветку и переводит её на коммит вперёд
4 Что такое merge commit? - коммит при слиянии двух параллельно изменённых веток
5 Сколько родителей может иметь обычный commit? А merge commit? - обычный в зависимости от кол-ва веток, а merge двоих
6 Почему Three-Way Merge называется именно так? - потому-что затрагивает три точки
7 Если я нахожусь на master и выполняю:
git merge feature
какая ветка является целевой? - master
8 После git merge feature я автоматически перейду на feature? - нет
9 Удаляется ли feature после успешного merge? - нет
10 Объясни своими словами разницу между:
A ── B ── C

и
      C ──┐
     /    │
A ── B    M
     \    │
      D ──┘

В первом это последовательная история, а во втором разветвлённая.
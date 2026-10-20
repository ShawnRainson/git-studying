Практика на твоём компьютере
PS D:\git-studying> mkdir git-day5
>> 


    Каталог: D:\git-studying


Mode                 LastWriteTime         Length Name                
----                 -------------         ------ ----                
d-----        20.10.2026      2:43                git-day5            


PS D:\git-studying> git clone D:\git-studying\remote-day5.git D:\git-studying\git-day5ty Git repository in D:/git-studying/remote-day5.git/
>> D:\git-studying> 
Cloning into 'D:\git-studying\git-day5'...
warning: You appear to have cloned an empty repository.
done.
PS D:\git-studying> cd D:\git-studying\git-day5
PS D:\git-studying\git-day5> git remote -v
origin  D:\git-studying\remote-day5.git (fetch)
origin  D:\git-studying\remote-day5.git (push)
PS D:\git-studying\git-day5> git branch -a
PS D:\git-studying\git-day5> "Remote training v1" | Out-File -Encoding utf8 app.txt
>> 
PS D:\git-studying\git-day5> git add app.txt
PS D:\git-studying\git-day5> git commit -m "Initial remote training commit"
[master (root-commit) e960ada] Initial remote training commit
 1 file changed, 1 insertion(+)
 create mode 100644 app.txt
PS D:\git-studying\git-day5> git status
On branch master
Your branch is based on 'origin/master', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

nothing to commit, working tree clean
PS D:\git-studying\git-day5> git log --oneline --decorate
e960ada (HEAD -> master) Initial remote training commit
PS D:\git-studying\git-day5> git branch --show-current
master
PS D:\git-studying\git-day5> git push -u origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 250 bytes | 250.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To D:\git-studying\remote-day5.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.
PS D:\git-studying\git-day5> git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
PS D:\git-studying\git-day5> git branch -vv
* master e960ada [origin/master] Initial remote training commit
PS D:\git-studying\git-day5> git clone D:\git-studying\remote-day5.git D:\git-studying\git-day5-peer
>> 
Cloning into 'D:\git-studying\git-day5-peer'...
done.
PS D:\git-studying\git-day5> cd D:\git-studying\git-day5-peer
PS D:\git-studying\git-day5-peer> Add-Content app.txt "Change from peer"
>> 
PS D:\git-studying\git-day5-peer> git add app.txt
PS D:\git-studying\git-day5-peer> git commit -m "Add change from peer"
[master 48057b3] Add change from peer
 1 file changed, 1 insertion(+)
PS D:\git-studying\git-day5-peer> git branch --show-current
master
PS D:\git-studying\git-day5-peer> git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 293 bytes | 293.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To D:\git-studying\remote-day5.git
   e960ada..48057b3  master -> master
PS D:\git-studying\git-day5-peer> cd D:\git-studying\git-day5
>> 
PS D:\git-studying\git-day5> git fetch origin
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 273 bytes | 27.00 KiB/s, done.
From D:\git-studying\remote-day5
   e960ada..48057b3  master     -> origin/master
PS D:\git-studying\git-day5> git status
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
PS D:\git-studying\git-day5> git log --oneline --decorate --all --graph

* 48057b3 (origin/master, origin/HEAD) Add change from peer
* e960ada (HEAD -> master) Initial remote training commit
PS D:\git-studying\git-day5> git pull
Updating e960ada..48057b3
Fast-forward
 app.txt | 1 +
 1 file changed, 1 insertion(+)
PS D:\git-studying\git-day5> Get-Content app.txt
Remote training v1
Change from peer
PS D:\git-studying\git-day5> git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
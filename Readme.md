# Report

Going to create the git repo on my local machine:
```console
me@laptop ~ $ mkdir GitPractice
me@laptop ~ $ cd GitPractice
me@laptop ~/GitPractice $ git init
Initialized empty Git repository in C:/Users/kbenton/projects/GitPractice/.git/
```

I've copied this file into the folder, and am going to commit it.
```console
me@laptop ~/GitPractice (master) $ git add .
me@laptop ~/GitPractice (master) $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Readme.md

me@laptop ~/GitPractice (master) $ git commit -m "First Commit!"
[master (root-commit) 71a5393] First Commit!
 1 file changed, 24 insertions(+)
 create mode 100644 Readme.md

me@laptop ~/GitPractice (master) $ git log
commit 71a539391974dea90093e7061342439deb837639 (HEAD -> master)
Author: knbedgm <knbedgm@users.noreply.github.com>
Date:   Wed Jan 15 14:44:27 2025 -0500

    First Commit!
 
```

I've created the first commit and now I want to push it to GitHub. I'll start by creating a repository there.
https://github.com/knbedgm/GitPractice

Now to add the remote to my local repo, commit these instructions, and push to GitHub:
```console
me@laptop ~/GitPractice (master) $ git remote add origin git@github.com:knbedgm/GitPractice.git
me@laptop ~/GitPractice (master) $ git add .
me@laptop ~/GitPractice (master) $ git commit -m "Adding a remote"
```
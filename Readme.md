# Report
## Git Basics

Going to create the git repo on my local machine:
```console
me@laptop ~ $ mkdir GitPractice
me@laptop ~ $ cd GitPractice
me@laptop ~/GitPractice $ git init
Initialized empty Git repository in C:/Users/kbenton/projects/GitPractice/.git/
```

I've copied this file into the folder, and am going to commit it.
```console
me@laptop ~/GitPractice master $ git add .
me@laptop ~/GitPractice master $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Readme.md

me@laptop ~/GitPractice master $ git commit -m "First Commit!"
[master (root-commit) 71a5393] First Commit!
 1 file changed, 24 insertions(+)
 create mode 100644 Readme.md

me@laptop ~/GitPractice master $ git log
commit 71a539391974dea90093e7061342439deb837639 (HEAD -> master)
Author: knbedgm <knbedgm@users.noreply.github.com>
Date:   Wed Jan 15 14:44:27 2025 -0500

    First Commit!
 
```

## Working with GitHub

I've created the first commit and now I want to push it to GitHub. I'll start by creating a repository there.
https://github.com/knbedgm/GitPractice

Now to add the remote to my local repo, commit these instructions, and push to GitHub:
```console
me@laptop ~/GitPractice master $ git remote add origin git@github.com:knbedgm/GitPractice.git
me@laptop ~/GitPractice master $ git add .
me@laptop ~/GitPractice master $ git commit -m "Adding a remote"
[master 9e54639] Adding a remote
 1 file changed, 22 insertions(+), 1 deletion(-)

me@laptop ~/GitPractice master $ git push -u origin master
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

me@laptop ~/GitPractice master $ git push -u origin master
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 16 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 1.35 KiB | 1.35 MiB/s, done.
Total 6 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), done.
To github.com:knbedgm/GitPractice.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.

```

Turns out my ssh key was only set up for signing on GitHub, not authentication, so I had to try again after fixing that.

# Branching and Merging

We start by making a new git branch to hold our changes:
```console
me@laptop ~/GitPractice master $ git checkout -b feature
Switched to a new branch 'feature'
```

I noticed that some highlighting was broken when viewing on GitHub, so I'll make changes to fix that on this branch, then push.
```console
me@laptop ~/GitPractice feature $ git add .
me@laptop ~/GitPractice feature $ git commit -m "Fix formatting"
[feature 744027b] Fix formatting
 1 file changed, 49 insertions(+), 8 deletions(-)
me@laptop ~/GitPractice feature $ git push -u origin feature
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.64 KiB | 842.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote:
remote: Create a pull request for 'feature' on GitHub by visiting:
remote:      https://github.com/knbedgm/GitPractice/pull/new/feature
remote:
To github.com:knbedgm/GitPractice.git
 * [new branch]      feature -> feature
branch 'feature' set up to track 'origin/feature'.
```

Now to switch back to `master` and merge in the changes.
```console
me@laptop ~/GitPractice feature $ git checkout master
error: Your local changes to the following files would be overwritten by checkout:
        Readme.md
Please commit your changes or stash them before you switch branches.
Aborting
```

Hmm, I'll have to copy the document somewhere else while I do the merge, otherwise I'm going to break things.

Now to revert the changes and actually merge:
```console
me@laptop ~/GitPractice feature $ git reset --hard
HEAD is now at 744027b Fix formatting

me@laptop ~/GitPractice feature $ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

me@laptop ~/GitPractice master $ git merge feature
Updating 9e54639..744027b
Fast-forward
 Readme.md | 57 +++++++++++++++++++++++++++++++++++++++++++++++++--------
 1 file changed, 49 insertions(+), 8 deletions(-)

```

And now to copy this file back in and commit it so you can read it.
```console
me@laptop ~/GitPractice master $ git add .
me@laptop ~/GitPractice master $ git commit -m "Merge instructions"
[master 6f7a0f2] Merge instructions
 1 file changed, 55 insertions(+)

me@laptop ~/GitPractice master $ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.29 KiB | 659.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:knbedgm/GitPractice.git
   9e54639..6f7a0f2  master -> master
```

Looking at it on GitHub, removing the brackets around the branch name didn't fix the formatting... Oh well.


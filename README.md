# Semantic Git
## How to Git++

### Git command list

1. [git show](#git-show)
2. [git status](#git-status)
3. [git diff](#git-diff)
4. [git log](#git-log)
5. [git blame](#git-blame)
6. [git reset](#git-reset)
7. [git cherry-pick](#git-cherry-pick)
8. [git stash](#git-stash)
9. [git rebase](#git-rebase)
10. [git reflog](#git-reflog)
11. [git bisect](#git-bisect)
12. [git revert](#git-revert)

#### $ git show
Manual: https://git-scm.com/docs/git-show
Shows information about a certain object like tags, commits branches...

Examples:
```shell
╰─$ git show HEAD

commit 2b43fd8b95f3ad95057b0a6d6e0debb4417c4cfe
Author: Luiz Sotero <luizsotero@gmail.com>
Date:   Thu Oct 27 12:57:51 2016 -0300

    Add first branch 1 words

diff --git a/README.md b/README.md
index aaa2b6e..8f84011 100644
--- a/README.md
+++ b/README.md
@@ -1,2 +1,4 @@
 # Semantic Git
 ## How to Git++
+
+Create branch 1
\ No newline at end of file
```

#### $ git status
Manual: https://git-scm.com/docs/git-status
Show status about the current git situation, like revision differences, rebase, merge or cherry-pick states, branch names etc.

Examples:
```shell
╰─$ git status
On branch git_status
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

#### $ git diff
Manual: https://git-scm.com/docs/git-diff
Shows a comparison of two different revisions. Can be used on a file, branch or two different pointers, such as branches or commits.

Examples:
```shell
╰─$ git diff README.md

diff --git a/README.md b/README.md
index 8fbb413..d578080 100644
--- a/README.md
+++ b/README.md
@@ -59,7 +59,7 @@ Changes not staged for commit:
 no changes added to commit (use "git add" and/or "git commit -a")
 ```

-### $ git diff
+#### $ git diff

 Shows a comparison of two different revisions. Can be used on a file, branch or two different pointers, such as branches or commits.
```

```shell
╰─$ git diff HEAD..HEAD^

diff --git a/README.md b/README.md
index ca9cf6a..8fbb413 100644
--- a/README.md
+++ b/README.md
@@ -59,26 +59,46 @@ [..] DESCRIPTION REMOVED FOR READABILITY IMPROVEMENT
```

```shell
╰─$ git diff git_show..git_status

diff --git a/README.md b/README.md
index e58b934..a3ff1df 100644
--- a/README.md
+++ b/README.md
@@ -3,28 +3,19 @@ [..] DESCRIPTION REMOVED FOR READABILITY IMPROVEMENT
```

#### $ git log

Manual: https://git-scm.com/docs/git-log
Show a list of commits with their descriptions in ancestor order

Examples:
```shell
╰─$ git log

commit 97ebd4274b9f3aa44538a20f0e7e26b61e4bd6a9
Author: Luiz Sotero <luizsotero@gmail.com>
Date:   Thu Oct 27 14:20:34 2016 -0300

    Add git diff example with two branches

commit 9efed07fc9e9c188090c8b2563a5e138b0d7d701
Merge: a25f4d8 ef36afa
Author: Luiz Sotero <luizsotero@gmail.com>
Date:   Thu Oct 27 13:40:09 2016 -0300

    Merge branch 'git_diff'
[..]
```

```shell
╰─$ git log --graph --oneline --decorate --all

* 97ebd42 (HEAD -> git_diff_branches) Add git diff example with two branches
*   9efed07 (master) Merge branch 'git_diff'
|\
| * ef36afa (git_diff) Add pointer..pointer git diff example
|/
* a25f4d8 Fix title header level and make the git diff example smaller
* ddb452e Add command list and first specification for git diff with one big example
*   0941896 Merge branch 'git_status'
|\
| * c5e81d4 (git_status) Add git status command information and example
* |   6b2a5ec Merge branch 'git_show'
|\ \
| |/
|/|
| * 0cbc622 (git_show) Add git show command description
* | 56688bd Add Git commands title
|/
* 3397a27 First commit
```

#### $ git blame
Manual: https://git-scm.com/docs/git-blame
Shows who, when and where (in which commit) the current state of a file was modified.

When commiting is done right, this command, allied with `git show` is great to understand why certain changes were made or bugs introduced.

Examples:
```shell
╰─$ git blame README.md

[..]
f3d79c57 (Luiz Sotero 2016-10-27 14:45:35 -0300 149) ```
f3d79c57 (Luiz Sotero 2016-10-27 14:45:35 -0300 150)
cea8273f (Luiz Sotero 2016-10-27 15:11:11 -0300 151) #### git error
cea8273f (Luiz Sotero 2016-10-27 15:11:11 -0300 152) This is no command at all! ERROR! ERROR!
cea8273f (Luiz Sotero 2016-10-27 15:11:11 -0300 153)
cea8273f (Luiz Sotero 2016-10-27 15:11:11 -0300 154)
ddb452e2 (Luiz Sotero 2016-10-27 13:33:10 -0300 155) ### Guidelines and best practices
[..]
```

- Use `git show` to understand better why someone added the code lines contained in commit cea8273f

```shell
╰─$ git show cea8273f

commit cea8273fc9ad9a3eb43ab2fe4b3b3908f59c3f76
Author: Luiz Sotero <luizsotero@gmail.com>
Date:   Thu Oct 27 15:11:11 2016 -0300

    crappy commit with error

diff --git a/README.md b/README.md
index 39651ed..dfc0bd2 100644
--- a/README.md
+++ b/README.md
@@ -148,4 +148,8 @@ Date:   Thu Oct 27 13:40:09 2016 -0300
 * 3397a27 First commit
 ```

+#### git error
+This is no command at all! ERROR! ERROR!
+
+
 ### Guidelines and best practices
```

#### $ git reset
Manual: https://git-scm.com/docs/git-reset
Reset the current HEAD pointer to a specified state

Used with `--hard` can make the branch move the HEAD pointer to any step in the tree ignoring the changes between states.

Examples:

```shell
╰─$ git log --graph --oneline --decorate --all
*   6b9564d (HEAD -> git_reset, master) Merge branch 'git_cherry'
|\
| * cfd80fc (git_cherry) Add second cherry-pick example with commit range
| * 25ba63f Add better description to git cherry-pick command telling about the most common case
| * c03812f Add git cherry-pick command with incomplete example
|/
*   d1eac7d Merge branch 'git_blame'
[..]

╰─$ git reset 25ba63f --hard
HEAD is now at 25ba63f Add better description to git cherry-pick command telling about the most common case

╰─$ git log --graph --oneline --decorate --all
*   6b9564d (master) Merge branch 'git_cherry'
|\
| * cfd80fc (git_cherry) Add second cherry-pick example with commit range
| * 25ba63f (HEAD -> git_reset) Add better description to git cherry-pick command telling about the most common case
| * c03812f Add git cherry-pick command with incomplete example
|/
*   d1eac7d Merge branch 'git_blame'
[..]

╰─$ git reset 098ed98 --hard
HEAD is now at 098ed98 WIP on git_reset: 6b9564d Merge branch 'git_cherry'
```

#### $ git cherry-pick
Manual: https://git-scm.com/docs/git-cherry-pick
Create new commits for every commit cherry-picked with the same changes. ** Important: this will create new commit hashes **

Most common use: You have inadvertidely created commits in the wrong branch and want to move them to the correct branch.

Examples:

```shell
╰─$ git cherry-pick 700ce57bfe00196d910069c7e44cbeb59bc5524f
[git_cherry c19ea20] Add git cherry-pick command with incomplete example
 Date: Thu Oct 27 20:49:08 2016 -0300
 1 file changed, 9 insertions(+)
```

```shell
╰─$ git cherry-pick master .. master^
[git_cherry c03812f] Add git cherry-pick command with incomplete example
 Date: Thu Oct 27 20:49:08 2016 -0300
 1 file changed, 9 insertions(+)
[git_cherry 25ba63f] Add better description to git cherry-pick command telling about the most common case
 Date: Thu Oct 27 20:58:58 2016 -0300
 1 file changed, 10 insertions(+), 4 deletions(-)
```

#### $ git stash
Manual: https://git-scm.com/docs/git-stash
Saves the current uncommited state with both staged and unstaged changes.

Very useful for doing rebases and changing briefly to another branch without having your changes applied avoiding conflict.

Examples:

```shell
╰─$ git stash
Saved working directory and index state WIP on master: 55af855 Merge branch 'git_reset'
HEAD is now at 55af855 Merge branch 'git_reset'
```

```shell
╰─$ git stash pop
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (e94d87f4822879c00969b5bee468ea0ab23e9e0c)
```

```shell
╰─$ git stash apply
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

### Guidelines and best practices

- Make commits semantic, by squashing changes that make sense together
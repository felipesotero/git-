# Semantic Git
## How to Git++

### Git command list

1. [git show](#-git-show)
2. [git status](#-git-status)
3. [git diff](#-git-diff)
4. [git log](#-git-log)
5. [git blame](#-git-blame)
6. [git reset](#-git-reset)
7. [git cherry-pick](#-git-cherry-pick)
8. [git stash](#-git-stash)
9. [git rebase](#-git-rebase)
10. [git reflog](#-git-reflog)
11. [git bisect](#-git-bisect)
12. [git revert](#-git-revert)

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

Create new commits for every commit cherry-picked with the same changes. **Important: this will create new commit hashes**

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

#### $ git rebase
Manual: https://git-scm.com/docs/git-rebase

Change the history by adding a branch on top of another branch, actually it can be any set of commits on top of another set.

This command is useful to remove unecessary commits after they were created, rename commits in batch, squashing and splitting commits and avoid diamond shapes in the history (merge-hell)

Three most common uses of rebase:
##### `$ git rebase -i`

Example:
```shell
╰─$ git rebase -i HEAD~4

pick 256e9db Add rebase title
s 9c72322 add manual reference
f cb8bc26 Add description and tips
f a4b6be8 Add new sub titles

# Rebase 41d2879..a4b6be8 onto 41d2879 (4 command(s))
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

Next step:
```shell
# This is a combination of 4 commits.
# The first commit's message is:
Add rebase title

# This is the 2nd commit message:

add manual reference

# The 3rd commit message will be skipped:
#   Add description and tips

# The 4th commit message will be skipped:
#   Add new sub titles

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sun Oct 30 09:55:15 2016 -0300
#
# rebase in progress; onto 41d2879
# You are currently editing a commit while rebasing branch 'git_rebase' on '41d2879'.
#
# Changes to be committed:
#   modified:   README.md
#
```

When finishing:
```shell
╰─$ git rebase -i HEAD~4
[detached HEAD fb7ecf0] Add rebase title
 Date: Sun Oct 30 09:55:15 2016 -0300
 1 file changed, 14 insertions(+)
Successfully rebased and updated refs/heads/git_rebase.
```

##### `$ git rebase --no-ff master`

Example:
Before `rebase --no-ff`:
```shell
* 35ad907 (master) Add first guideline and best practice
| * a977a9e (HEAD -> git_rebase) Add full example for git rebase -i
| * fb7ecf0 Add rebase title
|/
*   41d2879 Merge branch 'manual_refactor'
```
If merging without rebasing:
```shell
*   6752138 (HEAD -> master) Merge branch 'git_rebase'
|\
| * a977a9e (git_rebase) Add rebase commands with examples
* | 35ad907 Add first guideline and best practice
|/
*   41d2879 Merge branch 'manual_refactor'
```

After `rebase --no-ff` (before merging):
```shell
* aab0809 (HEAD -> git_rebase) Add full example for git rebase -i
* aaa9b2a Add rebase title
* 35ad907 (master) Add first guideline and best practice
*   41d2879 Merge branch 'manual_refactor'
```

After `merge --no-ff`:
```shell
*   46db0c2 (HEAD -> master) Merge branch 'git_rebase'
|\
| * f7d0aa4 (git_rebase) Add rebase commands with examples
|/
* 35ad907 Add first guideline and best practice
*   41d2879 Merge branch 'manual_refactor'
```

##### `$ git pull --rebase origin master`

This command avoids creating merge commits when pulling from the remote repository. If you are working in a shared branch and you and someone else makes a commit, both local branches will diverge requiring a merge commit. To avoid those, pull with `--rebase`.

#### $ git reflog
Manual: https://git-scm.com/docs/git-reflog

Reflog records all commands given and the commit state by each command. It is just like log, but with a commit for each command.

Reflog can save us when we think we lost a commit, deleted a wrong branch or did some confusing rebase or merge.

Example:
```shell
╰─$ git reflog
1ff5c49 HEAD@{0}: merge git_rebase: Merge made by the 'recursive' strategy.
35ad907 HEAD@{1}: checkout: moving from git_rebase to master
7f0b287 HEAD@{2}: rebase -i (finish): returning to refs/heads/git_rebase
7f0b287 HEAD@{3}: rebase -i (fixup): Add rebase commands with examples
f7d0aa4 HEAD@{4}: rebase -i (start): checkout HEAD~2
0902b4a HEAD@{5}: commit: asdasd
f7d0aa4 HEAD@{6}: checkout: moving from master to git_rebase
35ad907 HEAD@{7}: reset: moving to 35ad907
46db0c2 HEAD@{8}: merge git_rebase: Merge made by the 'recursive' strategy.
```

Used together with `git reset --hard` or `git checkout` we can move the HEAD pointer, restoring to a previous state or check the state on a given command.


#### $ git bisect
Manual: https://git-scm.com/docs/git-bisect

Uses a binary search algorithm to find which commit in the history introduced an undesired behaviour (commonly a bug).

Git bisect works as follows:
```shell
╰─$ git bisect start
╰─$ git bisect bad # if you ommit the ref, it will take the current version
╰─$ git bisect good v2.0.1-alpha2
```

Git will change its pointer and ask you to take action, which you will do one of:
```shell
╰─$ git bisect good
╰─$ git bisect bad
```

If you want to cancel:
```shell
╰─$ git bisect reset
```

You can pass a script for git to test:
```shell
╰─$ git bisect run script_name.sh args
```

Example:
```shell
╰─$ git bisect start
╭─ ~/dev/git++  ‹git_bisect*›
╰─$ git bisect bad
╭─ ~/dev/git++  ‹git_bisect*›
╰─$ git bisect good d1eac7dc5ef1e9642d4989b425aec6592fa31cde
Bisecting: 7 revisions left to test after this (roughly 3 steps)
[0b2d680df9c526cd3123f98ae34e0beb6bff11e2] Merge branch 'git_stash'
╭─ ~/dev/git++  ‹0b2d680›
╰─$ git bisect good
Bisecting: 3 revisions left to test after this (roughly 2 steps)
[7f0b287bfda3946c9d79213c05718af076a67cfb] Add rebase commands with examples
╭─ ~/dev/git++  ‹7f0b287›
╰─$ git bisect bad
Bisecting: 1 revision left to test after this (roughly 1 step)
[41d287968dccd9b1ba29e0c4b621d819cc92588c] Merge branch 'manual_refactor'
╭─ ~/dev/git++  ‹41d2879›
╰─$ git bisect good
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[35ad90764758bd603e58236da05ea60087df25cb] Add first guideline and best practice
╭─ ~/dev/git++  ‹35ad907›
# The hash above is the commit that introduced the problem.
╰─$ git revert 35ad907
[..]
```

Used together with `git revert` we can restore the introduced errors.

#### $ git revert
Manual: https://git-scm.com/docs/git-revert

Reverts one or more revisions, creating new commits for those.

Example:
```shell
# Before revert:
*   9e7fc7e (HEAD -> git_revert, master) Merge branch 'git_bisect'
|\
| * f7cc000 (git_bisect) Add git bisect command, usage and example
|/
*   0e86eb2 Merge branch 'git_reflog'
[..]

# Command:
╰─$ git revert f7cc000
[git_revert fb641c0] Revert "Add git bisect command, usage and example"
 1 file changed, 58 deletions(-)

# Create commit for the reversion.
--------------------------------------------------------------------
Revert "Add git bisect command, usage and example"

This reverts commit f7cc0005cbb3813b5bf274f1435cf780991a514e.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch git_revert
# Changes to be committed:
#   modified:   README.md
#
--------------------------------------------------------------------

# After revert:
* fb641c0 (HEAD -> git_revert) Revert "Add git bisect command, usage and example"
*   9e7fc7e (master) Merge branch 'git_bisect'
|\
| * f7cc000 (git_bisect) Add git bisect command, usage and example
|/
*   0e86eb2 Merge branch 'git_reflog'
[..]
```

### Guidelines and best practices

- Make commits semantic, by squashing changes that make sense together down to the minimum semantic amount.
- Always give some contextual information on your commit messages to avoid making the reader go through a long path of the history to understand what's going on on that particular commit.
- Don't `push --force` unless you know exactly what you are doing and try to be more explicitly as possible eg.: `git push origin my_nice_branch --force`
- Don't rewrite public history, only do it in extreme cases and be sure everyone in your team is on the same page.
- Linear histories are easier to be git-bisected and navigated, so keep that in mind.

### Flows

- Always merge with `--no-ff`. This will help keeping track of branches history.

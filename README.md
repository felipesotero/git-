# Semantic Git
## How to Git++

### Git command list

1. [git show](#git-show)
2. [git status](#git-status)
3. [git diff](#git-diff)
4. [git log](#git-log)
5. [git blame](#git-blame)
6. [git cherry-pick](#git-cherry-pick)
7. [git stash](#git-stash)
8. [git reset](#git-reset)
9. [git rebase](#git-rebase)
10. [git reflog](#git-reflog)
11. [git bisect](#git-bisect)
12. [git revert](#git-revert)

#### $ git show

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

### Guidelines and best practices

Git Cheat Sheet
===============

## Undoing/Changing

  * Undo last commit, move to staging area
    git reset --soft HEAD^

  * Undo last commit, remove from history (before push)
    git reset --hard HEAD^

  * Undo last commit, preserve history
    # -n means no auto-commit.
    git revert -n <commit>

  * Change last commit
    git commit --amend 

  * Untrack a previously tracked/checked-in file (but don't delete from filesystem)
    git rm --cached

  * Unstage a newly added file
    git rm --cached

  * Unstage staged changes (but leave changes in filesystem)
    # --mixed implied
    git reset HEAD 

  * Squash last 3 commits interactively.
    git rebase -i HEAD~3

## Git Configuration

  * Ignore file mode changes (for Windows!)
    git config --global core.filemode false

## Show Particular Version

  * Show last commit
    git show

  * Equivalent of 'svn cat'
    git show c3b3a:/[<file>]
    git show HEAD:/[<file>]

## Show Changes

  * Show short status
    git status -s
    git status --porcelain

  * Show log with changes made to files
    git log --stat
    git log --name-status
    git log --name-only

  * Show diff of last commit to file -- NICE!
    git log -p -1 <file>

  * Show changes (just files) of a commit
    git show --name-only c3b3a

  * Show changes (as diff) of a commit
    git show [<file>] # Last commit.
    git show c3b3a [<file>]
    git diff c3b3a^ c3b3a [<file>]

  * Show (cat) a specific version of a file
    git show c3b3a:<file>

  * Show changes between two commits
    git diff c3b3a e82c4

  * Detect file renames (super!)
    git diff -M

## Commit Ranges

    http://stackoverflow.com/questions/7251477/what-are-the-differences-between-double-dot-and-triple-dot-in-git-dif

### Git Log

  * Nice information on git commit range specifiers:
    # git log a..b vs git log a...b
    http://kwlug.org/pipermail/kwlug-disc_kwlug.org/2009-September/001907.html

  * Show all commits reachable from branch1 and branch2 (superset).
    git log branch1 branch2

  * Show all commits reachable from branch1 MINUS commits reachable from branch2.
    ie. all commits on branch1 that are NOT on branch2.
    git log branch1 ^branch2
    git log ^branch2 branch1 # same
    git log branch1..branch2 # same

### Git Diff

  * Show differences between two commits
    git diff foo bar
    git diff foo..bar  # same

  * Show differences between commit and merge base
    git diff foo...bar
    git diff $(git merge-base foo bar) bar

## Merging

  * Merge branch 'foo' into current branch
    git merge foo

  * Solving conflicts
    git checkout --ours filename.c
    git checkout --theirs filename.c

  * Interactive merging with beyond compare
    git mergetool -t bc3

  * Look at original files
    git show :1:<file> # common ancestor
    git show :2:<file> # HEAD
    git show :3:<file> # MERGE_HEAD

  * Undo last merge.
    git reset --hard ORIG_HEAD

## Reset vs. Checkout

  * checkout: changes HEAD

  * reset: changes tip of branch and makes HEAD point to it.

  * Initial state
    ... A - B - C (HEAD, master)

  * Let master point to B, not C, use 'git reset B'
    ... A - B (HEAD, master)      # - C is still here, but there's no branch pointing to it anymore

  * This is different from a checkout. If you'd run git checkout B, you'd get this:
    ... A - B (HEAD) - C (master)

## Various

  * Show file on a branch other than current branch:
    git show hsfz-experiments:Components/bsw/src/HSFZSystem.cpp

  * Show commits that are only on branch and not on master
    git cherry master hsfz-experiments

  * Find common ancestor for two branches
    git merge-base master hsfz-experiments

  * Stage deleted/modified files
    git add -u

  * Stage all files (new, deleted, modified)
    git add -A

  * Remember: HEAD is what you look at currently. HEAD is a reference to a reference
    and points at what is currently checked-out (eg. master).

  * [Nice tutorial on refs](https://people.gnome.org/~federico/news-2008-11.html#pushing-and-pulling-with-git-1)

  * Move last commit on branch of its own.
    git branch new_branch
    git reset --hard HEAD^  # Commit only lost on master, not new_branch.
    git checkout new_branch

  * Compress repo.
    git gc

  * Delete remote branch (need to delete local branch as well)
    git push origin --delete refactor/mc_4_refactor_foeslave

  * Delete local branch
    git branch -d refactor/mc_4_refactor_foeslave
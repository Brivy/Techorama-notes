# Git hidden gems

Maybe a Swiss army knife.

Pretty logs:

* `git log --pretty='%C(bold red)%hreset%C(bold yellow)%d%Creset %s %C(cyan)(%ar)%(Creset'"` A pretty git log string.
* Using git *alias*, we can reuse long commands.

Pretty diffs:

* All Git output is paased through an external program called *pager*. You can configure the *pager* with the `core.pager` option: `git config --global core.pager`. Better tool for git config is delta: `https://github.com/dandavison/delta`.

Pretty staging:

* You can stage individual changes within a file by using `git add --patch`. By using the `s` in the first command line, you get two hunks to stage. You can select one of them and not stage the other change.
* `git stash save --keep-index --include-untracked` will stash all your un-staged stuff, so you get a clean testable environment.
* Get the old changes back with `git stash pop`.

Searching:

* Git's most powerful search feature is *pickaxe*. It lets you find all commits that add or remove a line that contains a given string: `git log -S 'embarassing` (using -S).
* You can also search by function name: `git log -L:add:src/calculator.ts` (using -L and search on the `add` method in the `calculator` file (no *)).

Automation:

* By enabling `autosquash` you can more easily rewrite history: `git config --global rebase.autosquash true`. Place a commit after a specific commit: `git commit --fixup 398741`. Rebase without having to commit the changes in your working directory: `git config rebase.autoStash true` and then: `git rebase -i --root`.

Dot Nototion:

* Use the dot notation with `git log` to compare branches. For example: `git log main..topic`. You can also invert this to know which ones are not in topic but in main: `git log topic..main`.
* An alias is easy for this. For example, you can use `git config alias.new 'log --oneline main..HEAD`.
* Another one, but the other way around: `git config alias.missing 'log --oneline HEAD..main`.

Rebase onto:

* You can choose which commits to rebase in the current branch by using `rebase --onto`. For example: `git rebase --onto <new-base> <old-base>`.

ReFlog:

* The reflog keeps tracks of the changes in a branch: `git reflog branch-name`.
* *HEAD* also has it's own reflog: `git reflog`.
* `git switch -` will switch back to the branch you were coming from. It knows this because of the reflog.
* Get back to before a rebase. This is because the reflog remembers. Reset your branch: `git reset --hard feature/...@{1}`.
* Find some old code: `git lg -S --walk-reflogs`.

ReReRe:

* Reuse Recorded Resolution.
* Need to enable it `git config rerere.enabled true`.
* Once enabled, rerere will remember each side of a conflict and apply the recorded resolution next time the same conflict reappears.
* You can remove this recordings as wel.

*Difference between `checkout` and `switch`?*

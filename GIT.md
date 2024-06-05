### GIT
#### NEW REPO
```text
echo "# <reponame>" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M production
git remote add origin https://github.com/<orgname/<reponame>.git
git push -u origin production
```
#### EXIST REPO
```text
git remote add origin https://github.com/<orgname>/<reponame>.git
git branch -M production
git push -u origin production
```
#### ALIASES
```text
[user]
	name = denernun
	email = denernun@gmail.com
[color]
	ui = auto
	status = auto
	branch = auto
	interactive = auto
	diff = auto
[core]
	autocrlf = true
	editor = \"C:\\Users\\dener\\AppData\\Local\\Programs\\Microsoft VS Code Insiders\\bin\\code-insiders\" --wait
[alias]
	#
	# ----------------------------
	# status of branch
	# ----------------------------
	st = status
	#
	# ----------------------------
	# log branch
	# ----------------------------
	lo = log --no-merges --oneline --decorate --all --graph --pretty=format:'%C(yellow)[%h]%Cred%d%Creset %s %Cgreen [%cn] %ar'
	# ----------------------------
	# update branch
	# ----------------------------
	up = pull --rebase --verbose --progress
	#
	# ----------------------------
	# checkout to branch
	# ----------------------------
	co = checkout
	#
	# ----------------------------
	# add and commit changes
	# ----------------------------
	cm = !git add . && git commit -m
	#
	# ----------------------------
	# add, commit and push changes
	# ----------------------------
	cmm = !git add . && git commit --amend --no-edit && git push -f origin $(git bn)
	#
	# ----------------------------
	# verify merge conflicts
	# ----------------------------
	mt = "!f() { git merge --no-commit --no-ff \"$1\"; git merge --abort; echo \"Merge aborted\"; };f "
	#
	# ----------------------------
	# list branchs
	# ----------------------------
	br = branch -v -a
	#
	# ----------------------------
	# name of branch
	# ----------------------------
	bn = !git rev-parse --abbrev-ref HEAD
	#
	# ----------------------------
	# new branch
	# ----------------------------
	nb = !git checkout --track $(git config branch.$(git rev-parse --abbrev-ref HEAD).remote)/$(git rev-parse --abbrev-ref HEAD) -b
	#
	# ----------------------------
	# push branch to origin
	# ----------------------------
	pb = !git push -u origin $(git bn)
	#
	# ----------------------------
	# remove branch
	# ----------------------------
	rb = "!f() { git co production; git push origin --delete $1; git branch -D $1; };f "
	#
	# ----------------------------
	# prune remote
	# ----------------------------
	pr = !git remote prune origin
	#
[credential]
	helper = manager
[pull]
	rebase = true
[fetch]
	prune = true
[rebase]
	autoStash = false
[merge]
	tool = \"C:\\Users\\dener\\AppData\\Local\\Programs\\Microsoft VS Code Insiders\\Code - Insiders.exe\"
[mergetool "vscode"]
	cmd = code-insiders --wait $MERGED
[diff]
	tool = vscode
[difftool "vscode"]
	cmd = code-insiders --wait --diff $LOCAL $REMOTE
[winUpdater]
	recentlySeenVersion = 2.25.0.windows.1
[filter "lfs"]
	smudge = git-lfs smudge -- %f
	process = git-lfs filter-process
	required = true
	clean = git-lfs clean -- %f
[advice]
	detachedHead = false
[safe]
	directory = *
```




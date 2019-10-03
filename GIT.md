    git config --global credential.helper wincred
    git config --system http.sslcainfo "D:\GIT\mingw64\ssl\certs\ca-bundle.crt

    [user]
        name = Denernun
        email = denernun@gmail.com
    [color]
        ui = auto
    [core]
        autocrlf = false
    [alias]
	# update the branch
	up = pull --rebase --prune
	# checkout to branch
	co = checkout
	# List local/remote branchs
	br = branch -v -a
	# get the status of branch
	st = status
	# get the log of branch
	lo = log --oneline --decorate --all --graph --pretty=format:'%C(yellow)[%h]%Cred%d%Creset %s %Cgreen [%cn] %ar'
	# add and commit branch
	cm = !git add -A && git commit -m
	# get current branch name
	bn = !git rev-parse --abbrev-ref HEAD	
	# push the current branch to the remote "origin", and set it to track the upstream branch
	pb = !git co master && git push -u origin $(git bn)
	# delete the remote version of the current branch
	ub = "!git push origin :$(git bn)"
	# delete the local branch
	lb = !git co master && git branch -D $@
	# create a new branch
	nb = !git checkout --track $(git config branch.$(git rev-parse --abbrev-ref HEAD).remote)/$(git rev-parse --abbrev-ref HEAD) -b
	# run merge test to check for any conflicts beforehand.
	mt = "!f() { git merge --no-commit --no-ff \"$1\"; git merge --abort; echo \"Merge aborted\"; };f "
    [credential]
	helper = wincred

# Change the url projecvt

    git config --replace-all remote.origin.url https://user@bitbucket.org/UnicornsFactory/nome-do-projeto.git
    git remote set-url origin https://user@bitbucket.org/UnicornsFactory/nome-do-projeto.git

    git config --system http.sslcainfo "D:\GIT\mingw64\ssl\certs\ca-bundle.crt

    [user]
        name = Denernun
        email = denernun@gmail.com
    [color]
        ui = auto
    [core]
        autocrlf = false
    [alias]
        # Update the branch
        up = pull --rebase --prune
        # Checkout
        co = checkout
        # List local/remote branchs
        br = branch -v -a
        # Status
        st = status
        # Full log
        lo = log --oneline --decorate --all --graph --pretty=format:'%C(yellow)[%h]%Cred%d%Creset %s %Cgreen [%cn] %ar'
        # Add and Commit
        cm = !git add -A && git commit -m
        # Get the current branch name
        bn = "!git rev-parse --abbrev-ref HEAD"
        # Create a new branch
        nb = !git checkout --track $(git config branch.$(git rev-parse --abbrev-ref HEAD).remote)/$(git rev-parse --abbrev-ref HEAD) -b
        # Push the current branch to the remote "origin", and set it to track the upstream branch
        pb = "!git push -u origin $(git bn)"
        # Delete the remote version of the current branch
        ub = "!git push origin :$(git bn)"
        # Run merge test to check for any conflicts beforehand.
        mt = "!f() { git merge --no-commit --no-ff \"$1\"; git merge --abort; echo \"Merge aborted\"; };f "	

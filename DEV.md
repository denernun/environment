# Environment Install

**Java SDK**
---

    JavaSDK 64 http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
    JavaJRE 32 http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html

    Root
    
    C:\program Files\Java

    Environment

    JAVA_HOME=C:\Program Files\Java

----
**Android SDK**
---

    Android Studio https://developer.android.com/studio/preview/index.html

    Root
    
    D:\SDK

    Environment

    ANDROID_HOME=D:\SDK

    Path

    D:\SDK\tools\bin
    D:\SDK\platform-tools

----
**GIT**
---

    https://git-scm.com/download/win (portable)

    Root
    
    D:\GIT

    Path

    D:\GIT
    D:\GIT\cmd

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
	# Delete a branch and recreate it from master — useful if you have, say,
	# a development branch and a master branch and they could conceivably go
	# out of sync
	rb = "!f() { [[ -n $@ ]] && git checkout \"$@\" && git unpublish && git checkout master && git branch -D \"$@\" && git checkout -b \"$@\" && git publish; }; f"
	# Run merge test to check for any conflicts beforehand.
	mt = "!f() { git merge --no-commit --no-ff \"$1\"; git merge --abort; echo \"Merge aborted\"; };f "	

----
**Python**
---

    https://www.python.org/downloads/
	
    Root
    
    D:\PYTHON

    Environment

    PYTHON=D:\PYTHON\PYTHON.EXE

    Path

    D:\PYTHON
    D:\PYTHON\Scripts
	
----
**Ruby**
---

    https://rubyinstaller.org/downloads/
	
    Root
    
    D:\RUBY

    Path

    D:\RUBY\bin
	
----
**Redis**
---

    https://github.com/MicrosoftArchive/redis/releases
    
----
**NVM**
---

    https://github.com/coreybutler/nvm-windows

    Instructions
    
    Remove all versions of node in %appdata% and C:\Program Files\nodejs
    Install in D:\NVM
    Install SymLynk NodeJS in D:\NODE

    Root
    
    D:\NVM
    
    Path

    D:\NVM
        
    Comands
    
    nvm root <path> [D:\NVM]
    nvm install <version> arch [32|64]
    nvm list
    nvm use <version>
    nvm uninstall <version>

----
**Node**
---

    https://nodejs.org/en/

    Environment

    NODE_ENV=development

    Packages

    npm cache clean --force
    
    npm install -g node-gyp@latest
    npm install -g node-sass@latest
    npm install -g minifier
    npm install -g typescript
    
    npm install -g gulp
    npm install -g grunt
    
    npm install -g jslint
    npm install -g jshint
    npm install -g eslint
    npm install -g eslint-plugin-import
    npm install -g htmlhint
        
    npm install -g @angular/cli
    npm install -g loopback-cli
    npm install -g firebase-tools
        
    npm install -g npm-check-updates
    npm install -g source-map-explorer
    npm install -g cross-env
    
    npm install -g webpack-dev-server
    
    npm install -g --production windows-build-tools

----
**SSL**
---

    https://sourceforge.net/projects/openssl/

    Environment

    OPENSSL_HOME=D:\SSL
    OPENSSL_CONF=D:\SSL\BIN\OPENSSL.CNF

    Path

    D:\SSL\BIN

----
**SSH**
---

    https://mremoteng.org/download

    Path

    D:\SSH

----
**SVN**
---

    Path

    D:\SVN

----
**Others**
---

    Path

    D:\UTIL

----

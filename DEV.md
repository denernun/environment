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
**Gradle SDK**
---

    https://gradle.org/install/#manually

    Root
    
    D:\GRADLE
    
    Environment
    
    GRADLE_HOME=D:\GRADLE
    
    Path
    
    D:\GRADLE\bin

----
**GIT**
---

    https://git-scm.com/download/win (portable)

    Root
    
    D:\GIT

    Path

    D:\GIT
    D:\GIT\cmd

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
**RabbitMQ**
---

    Install Erlang
    http://www.erlang.org/downloads
    
    Install RabbitMQ
    https://www.rabbitmq.com/download.html

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

    # check updates
    npm i -g npm-check-updates

    # working with npm
    npm i -g yarn
    npm i -g npx
        
    # general utilities
    npm i -g node-gyp
    npm i -g node-sass
    npm i -g coffeescript
    npm i -g minifier
    npm i -g cross-env
    
    # debugging
    npm i -g ndb
    npm i -g nodemon

    # angular
    npm i -g typescript
    npm i -g @angular/cli

    # ionic
    npm i -g ionic
    npm i -g cordova

    # others
    npm i -g loopback-cli
    npm i -g firebase-tools
    npm i -g redis-commander

    # linting
    npm i -g jslint
    npm i -g jshint
    npm i -g eslint
    npm i -g eslint-config-standard
    npm i -g eslint-plugin-import
    npm i -g standard
    npm i -g htmlhint
    
    # utils
    npm i -g gulp
    npm i -g grunt
    npm i -g windows-build-tools --production
    npm i -g source-map-explorer
    
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

    # download portable edition
    https://winsshterm.blogspot.com/

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
    D:\DLL

----

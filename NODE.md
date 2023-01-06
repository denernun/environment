# Environment Install

## NODE
```text
Download
https://nodejs.org

Environment
NODE_ENV=development

Node-Gyp
https://github.com/nodejs/node-gyp#on-windows

node-gyp configure --msvs_version=2022
cd "C:\Program Files\nodejs"
cd node_modules\npm\node_modules\@npmcli\run-script
npm install node-gyp@latest

Node-SASS Build
npm config set msvs_version 2022
npm config set msvs_version 2022 --global
npm config set python "C:\Users\dener\AppData\Local\Programs\Python\Python311\python.exe"
npm config set msbuild_path "C:\Program Files\Microsoft Visual Studio\2022\Community\Msbuild\Current\Bin\MSBuild.exe"
npm config set node_gyp "C:\Users\dener\AppData\Roaming\npm\node_modules\node-gyp\bin\node-gyp.js"
```
## NPM
```text
Show
npm list -g --depth 0

Path
C:\Users\dener\AppData\Roaming\npm

Packages
+-- @angular/cli
+-- @loopback/cli
+-- @nestjs/cli
+-- cross-env
+-- dart-sass
+-- editorconfig
+-- eslint
+-- grunt
+-- gulp
+-- htmlhint
+-- http-server
+-- jest
+-- npm-check-updates
+-- nodemon
+-- node-gyp
+-- node-sass
+-- npm-check
+-- npm-run-all
+-- npm-windows-upgrade
+-- sass
+-- sass-migrator
+-- typescript
```
# Packages
```text
npm i -g @angular/cli @loopback/cli @nestjs/cli cross-env dart-sass editorconfig eslint grunt gulp htmlhint http-server jest node-gyp nodemon npm-check-updates node-sass npm-check npm-run-all npm-windows-upgrade sass sass-migrator typescript
```

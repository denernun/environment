# Environment Install

## NODE
```text
Download
https://nodejs.org

Environment
NODE_ENV=development
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
+-- node-sass
+-- npm-check
+-- npm-run-all
+-- sass
+-- typescript
```
# Packages
```text
npm i -g @angular/cli @loopback/cli @nestjs/cli cross-env dart-sass editorconfig eslint grunt gulp htmlhint http-server jest nodemon npm-check-updates node-sass npm-check npm-run-all sass typescript
```
# Windows Build Tools
```text
$ choco install visualstudio2019buildtools visualstudio2019-workload-vctools

$ npm config edit
  //registry.npmjs.org/:_authToken=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
  msbuild_path=C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\MSBuild.exe
  msvs_version=2019
  python=C:\Users\dener\AppData\Local\Programs\Python\Python312\python.exe
$ VCINSTALLDIR=C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\VC
$ GYP_MSVS_VERSION=2019
$ npm install --global node-gyp
$ npm i --force

$ cd "C:\Program Files\nodejs"
$ cd node_modules\npm\node_modules\@npmcli\run-script
$ npm install node-gyp@latest

$ project/binding.gyp
  {
    'targets': [
      {
        'target_name': 'bindings',
        'sources': [ 'bindings.node' ],
        'cflags!': [ '-fno-exceptions' ],
        'cflags_cc!': [ '-fno-exceptions' ],
        'conditions': [
          ['OS=="mac"', {
            'xcode_settings': {
              'GCC_ENABLE_CPP_EXCEPTIONS': 'YES'
            }
          }]
        ]
      }
    ]
  }
$ node-gyp rebuild


```

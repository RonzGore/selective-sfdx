SelectiveMDPlugin
=================

Selective push/pull of metadata from scratch orgs to source format

[![Version](https://img.shields.io/npm/v/SelectiveMDPlugin.svg)](https://npmjs.org/package/SelectiveMDPlugin)
[![CircleCI](https://circleci.com/gh/rohanatgwcs/SelectiveMDPlugin/tree/master.svg?style=shield)](https://circleci.com/gh/rohanatgwcs/SelectiveMDPlugin/tree/master)
[![Appveyor CI](https://ci.appveyor.com/api/projects/status/github/rohanatgwcs/SelectiveMDPlugin?branch=master&svg=true)](https://ci.appveyor.com/project/heroku/SelectiveMDPlugin/branch/master)
[![Codecov](https://codecov.io/gh/rohanatgwcs/SelectiveMDPlugin/branch/master/graph/badge.svg)](https://codecov.io/gh/rohanatgwcs/SelectiveMDPlugin)
[![Greenkeeper](https://badges.greenkeeper.io/rohanatgwcs/SelectiveMDPlugin.svg)](https://greenkeeper.io/)
[![Known Vulnerabilities](https://snyk.io/test/github/rohanatgwcs/SelectiveMDPlugin/badge.svg)](https://snyk.io/test/github/rohanatgwcs/SelectiveMDPlugin)
[![Downloads/week](https://img.shields.io/npm/dw/SelectiveMDPlugin.svg)](https://npmjs.org/package/SelectiveMDPlugin)
[![License](https://img.shields.io/npm/l/SelectiveMDPlugin.svg)](https://github.com/rohanatgwcs/SelectiveMDPlugin/blob/master/package.json)

<!-- toc -->
* [Debugging your plugin](#debugging-your-plugin)
<!-- tocstop -->
<!-- install -->
<!-- usage -->
```sh-session
$ npm install -g selective-sfdx
$ selective-sfdx COMMAND
running command...
$ selective-sfdx (-v|--version|version)
selective-sfdx/1.0.0 darwin-x64 node-v11.6.0
$ selective-sfdx --help [COMMAND]
USAGE
  $ selective-sfdx COMMAND
...
```
<!-- usagestop -->
<!-- commands -->
* [`selective-sfdx gs:source:pull`](#selective-sfdx-gssourcepull)
* [`selective-sfdx gs:source:push`](#selective-sfdx-gssourcepush)

## `selective-sfdx gs:source:pull`

Retrieves specific metadata/s to a sepcified location

```
USAGE
  $ selective-sfdx gs:source:pull

OPTIONS
  -d, --targetdir=targetdir                       (required) Path of target directory where the component needs to be
                                                  pulled

  -i, --includedir                                If you want to retrieve the directory as well along with the metadata
                                                  components

  -n, --names=names                               (required) Name of the component/s to retrieve

  -t, --type=type                                 (required) Type of the components to retrieve, only support one
                                                  component at a time

  -u, --targetusername=targetusername             username or alias for the target org; overrides default target org

  --apiversion=apiversion                         override the api version used for api requests made by this command

  --json                                          format output as json

  --loglevel=(trace|debug|info|warn|error|fatal)  logging level for this command invocation

EXAMPLES
  sfdx gs:source:pull --type ApexClass --names MyClass1,MyClass2 --targetdir app/main/default/classes
       // retrieves MyClass1 and MyClass2 from an org (sratch/non-scratch) to the provided directory location
    
  sfdx gs:source:pull --type Layout --names Layout1 --targetdir app/main/default --includedir
       // retrieves Layout1 along with the layouts folder from an org (sratch/non-scratch) to the provided directory 
  location
```

_See code: [src/commands/gs/source/pull.ts](https://github.com/rohanatgwcs/selective-sfdx/blob/v1.0.0/src/commands/gs/source/pull.ts)_

## `selective-sfdx gs:source:push`

Deploys a module in source-format from a sepcified location

```
USAGE
  $ selective-sfdx gs:source:push

OPTIONS
  -m, --modulepath=modulepath                     (required) Name of the component/s to retrieve
  -u, --targetusername=targetusername             username or alias for the target org; overrides default target org
  --apiversion=apiversion                         override the api version used for api requests made by this command
  --json                                          format output as json
  --loglevel=(trace|debug|info|warn|error|fatal)  logging level for this command invocation

EXAMPLE
  sfdx gs:source:push --modulePath app
       // deploys app module to the target org
```

_See code: [src/commands/gs/source/push.ts](https://github.com/rohanatgwcs/selective-sfdx/blob/v1.0.0/src/commands/gs/source/push.ts)_
<!-- commandsstop -->
<!-- debugging-your-plugin -->
# Debugging your plugin
We recommend using the Visual Studio Code (VS Code) IDE for your plugin development. Included in the `.vscode` directory of this plugin is a `launch.json` config file, which allows you to attach a debugger to the node process when running your commands.

To debug the `hello:org` command: 
1. Start the inspector
  
If you linked your plugin to the sfdx cli, call your command with the `dev-suspend` switch: 
```sh-session
$ sfdx hello:org -u myOrg@example.com --dev-suspend
```
  
Alternatively, to call your command using the `bin/run` script, set the `NODE_OPTIONS` environment variable to `--inspect-brk` when starting the debugger:
```sh-session
$ NODE_OPTIONS=--inspect-brk bin/run hello:org -u myOrg@example.com
```

2. Set some breakpoints in your command code
3. Click on the Debug icon in the Activity Bar on the side of VS Code to open up the Debug view.
4. In the upper left hand corner of VS Code, verify that the "Attach to Remote" launch configuration has been chosen.
5. Hit the green play button to the left of the "Attach to Remote" launch configuration window. The debugger should now be suspended on the first line of the program. 
6. Hit the green play button at the top middle of VS Code (this play button will be to the right of the play button that you clicked in step #5).
<br><img src=".images/vscodeScreenshot.png" width="480" height="278"><br>
Congrats, you are debugging!

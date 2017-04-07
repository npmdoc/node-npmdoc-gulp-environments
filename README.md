# api documentation for  [gulp-environments (v0.1.2)](https://github.com/gunpowderlabs/gulp-environments#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-environments.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-environments) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-environments.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-environments)
#### A library for easily adding environments (development/production) to Gulp

[![NPM](https://nodei.co/npm/gulp-environments.png?downloads=true)](https://www.npmjs.com/package/gulp-environments)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-environments/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-environments_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-environments/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-environments/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-environments/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Adam Pohorecki",
        "email": "adam@gunpowderlabs.com"
    },
    "bugs": {
        "url": "https://github.com/gunpowderlabs/gulp-environments/issues"
    },
    "dependencies": {
        "gulp-if": "^2.0.1",
        "yargs": "^5.0.0"
    },
    "description": "A library for easily adding environments (development/production) to Gulp",
    "devDependencies": {
        "chai": "^3.0.0",
        "mocha": "^2.2.5"
    },
    "directories": {},
    "dist": {
        "shasum": "8646107392193582aff919d53de3302777ffb6eb",
        "tarball": "https://registry.npmjs.org/gulp-environments/-/gulp-environments-0.1.2.tgz"
    },
    "gitHead": "b7d496267437729585b563f1f9269c05df186414",
    "homepage": "https://github.com/gunpowderlabs/gulp-environments#readme",
    "keywords": [
        "gulp",
        "environments"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "psyho",
            "email": "apohorecki+npm@gmail.com"
        },
        {
            "name": "wrozka",
            "email": "pawelpierzchala@gmail.com"
        }
    ],
    "name": "gulp-environments",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/gunpowderlabs/gulp-environments.git"
    },
    "scripts": {
        "test": "./node_modules/mocha/bin/mocha ./index.js ./test/*.js"
    },
    "version": "0.1.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-environments](#apidoc.module.gulp-environments)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>current (env)](#apidoc.element.gulp-environments.current)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>development (gulpStream)](#apidoc.element.gulp-environments.development)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>make (name)](#apidoc.element.gulp-environments.make)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>production (gulpStream)](#apidoc.element.gulp-environments.production)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>reset ()](#apidoc.element.gulp-environments.reset)

#### [module gulp-environments.development](#apidoc.module.gulp-environments.development)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>development (gulpStream)](#apidoc.element.gulp-environments.development.development)
1.  [function <span class="apidocSignatureSpan">gulp-environments.development.</span>task ()](#apidoc.element.gulp-environments.development.task)

#### [module gulp-environments.production](#apidoc.module.gulp-environments.production)
1.  [function <span class="apidocSignatureSpan">gulp-environments.</span>production (gulpStream)](#apidoc.element.gulp-environments.production.production)
1.  [function <span class="apidocSignatureSpan">gulp-environments.production.</span>task ()](#apidoc.element.gulp-environments.production.task)



# <a name="apidoc.module.gulp-environments"></a>[module gulp-environments](#apidoc.module.gulp-environments)

#### <a name="apidoc.element.gulp-environments.current"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>current (env)](#apidoc.element.gulp-environments.current)
- description and source-code
```javascript
function current(env) {
  if(arguments.length > 0) {
    currentEnv = env;
  } else {
    return currentEnv;
  }
}
```
- example usage
```shell
...

and run it (or make it a dependency of a task that should also be run in that environment):

gulp set-dev build

Finally, you can always set the environment by hand in your task definition:

environments.current(development);

## Other environments

You don't have to limit yourself to using only the two provided environments. You can create other ones by calling (in the example
, we are creating an environment called staging):

var staging = environments.make("staging");
...
```

#### <a name="apidoc.element.gulp-environments.development"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>development (gulpStream)](#apidoc.element.gulp-environments.development)
- description and source-code
```javascript
function envFn(gulpStream) {
  var isCurrentEnv = current().$name === name;

  if(arguments.length === 0) { return isCurrentEnv; }

  return gif(isCurrentEnv, gulpStream);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-environments.make"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>make (name)](#apidoc.element.gulp-environments.make)
- description and source-code
```javascript
function make(name) {
  if(arguments.length < 1) {
    throw "You must provide an name to environments.make()";
  }

  function envFn(gulpStream) {
    var isCurrentEnv = current().$name === name;

    if(arguments.length === 0) { return isCurrentEnv; }

    return gif(isCurrentEnv, gulpStream);
  }

  envFn.$name = name;

  envFn.task = function() {
    current(envFn);
  };

  return envFn;
}
```
- example usage
```shell
...

    environments.current(development);

## Other environments

You don't have to limit yourself to using only the two provided environments. You can create other ones by calling (in the example
, we are creating an environment called staging):

    var staging = environments.make("staging");

## License

MIT

## Author
...
```

#### <a name="apidoc.element.gulp-environments.production"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>production (gulpStream)](#apidoc.element.gulp-environments.production)
- description and source-code
```javascript
function envFn(gulpStream) {
  var isCurrentEnv = current().$name === name;

  if(arguments.length === 0) { return isCurrentEnv; }

  return gif(isCurrentEnv, gulpStream);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-environments.reset"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>reset ()](#apidoc.element.gulp-environments.reset)
- description and source-code
```javascript
function reset() {
  current(make(process.env.NODE_ENV || argv.env || "development"));
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.gulp-environments.development"></a>[module gulp-environments.development](#apidoc.module.gulp-environments.development)

#### <a name="apidoc.element.gulp-environments.development.development"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>development (gulpStream)](#apidoc.element.gulp-environments.development.development)
- description and source-code
```javascript
function envFn(gulpStream) {
  var isCurrentEnv = current().$name === name;

  if(arguments.length === 0) { return isCurrentEnv; }

  return gif(isCurrentEnv, gulpStream);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-environments.development.task"></a>[function <span class="apidocSignatureSpan">gulp-environments.development.</span>task ()](#apidoc.element.gulp-environments.development.task)
- description and source-code
```javascript
task = function () {
  current(envFn);
}
```
- example usage
```shell
...

You can also pass a command line flag --env to set it:

    gulp build --env development

Alternatively, you can define a task that would set the appropriate environment before executing other tasks:

    gulp.task('set-dev', development.task);

and run it (or make it a dependency of a task that should also be run in that environment):

    gulp set-dev build

Finally, you can always set the environment by hand in your task definition:
...
```



# <a name="apidoc.module.gulp-environments.production"></a>[module gulp-environments.production](#apidoc.module.gulp-environments.production)

#### <a name="apidoc.element.gulp-environments.production.production"></a>[function <span class="apidocSignatureSpan">gulp-environments.</span>production (gulpStream)](#apidoc.element.gulp-environments.production.production)
- description and source-code
```javascript
function envFn(gulpStream) {
  var isCurrentEnv = current().$name === name;

  if(arguments.length === 0) { return isCurrentEnv; }

  return gif(isCurrentEnv, gulpStream);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-environments.production.task"></a>[function <span class="apidocSignatureSpan">gulp-environments.production.</span>task ()](#apidoc.element.gulp-environments.production.task)
- description and source-code
```javascript
task = function () {
  current(envFn);
}
```
- example usage
```shell
...

You can also pass a command line flag --env to set it:

    gulp build --env development

Alternatively, you can define a task that would set the appropriate environment before executing other tasks:

    gulp.task('set-dev', development.task);

and run it (or make it a dependency of a task that should also be run in that environment):

    gulp set-dev build

Finally, you can always set the environment by hand in your task definition:
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

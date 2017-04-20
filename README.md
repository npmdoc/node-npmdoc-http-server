# npmdoc-http-server

#### api documentation for  [http-server (v0.9.0)](https://github.com/indexzero/http-server#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-http-server.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-http-server) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-http-server.svg)](https://travis-ci.org/npmdoc/node-npmdoc-http-server)

#### A simple zero-configuration command-line http server

[![NPM](https://nodei.co/npm/http-server.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/http-server)

- [https://npmdoc.github.io/node-npmdoc-http-server/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-http-server/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-http-server/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-http-server/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-http-server/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-http-server/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "bin": {
        "http-server": "./bin/http-server",
        "hs": "./bin/http-server"
    },
    "bugs": {
        "url": "https://github.com/nodeapps/http-server/issues"
    },
    "contributors": [
        {
            "name": "Charlie Robbins"
        },
        {
            "name": "Marak Squires"
        },
        {
            "name": "Charlie McConnell"
        },
        {
            "name": "Joshua Holbrook"
        },
        {
            "name": "Maciej Małecki"
        },
        {
            "name": "Matthew Bergman"
        },
        {
            "name": "brad dunbar"
        },
        {
            "name": "Dominic Tarr"
        },
        {
            "name": "Travis Person"
        },
        {
            "name": "Jinkwon Lee"
        }
    ],
    "dependencies": {
        "colors": "1.0.3",
        "corser": "~2.0.0",
        "ecstatic": "^1.4.0",
        "http-proxy": "^1.8.1",
        "opener": "~1.4.0",
        "optimist": "0.6.x",
        "portfinder": "0.4.x",
        "union": "~0.4.3"
    },
    "description": "A simple zero-configuration command-line http server",
    "devDependencies": {
        "common-style": "^3.0.0",
        "request": "2.49.x",
        "vows": "0.7.x"
    },
    "directories": {},
    "dist": {
        "shasum": "8f1b06bdc733618d4dc42831c7ba1aff4e06001a",
        "tarball": "https://registry.npmjs.org/http-server/-/http-server-0.9.0.tgz"
    },
    "gitHead": "1a8552c5e028bd5500027ee940111133927a4e94",
    "homepage": "https://github.com/indexzero/http-server#readme",
    "keywords": [
        "cli",
        "command"
    ],
    "license": "MIT",
    "main": "./lib/http-server",
    "maintainers": [
        {
            "name": "indexzero"
        }
    ],
    "name": "http-server",
    "optionalDependencies": {},
    "preferGlobal": "true",
    "repository": {
        "type": "git",
        "url": "git://github.com/indexzero/http-server.git"
    },
    "scripts": {
        "pretest": "common bin/http-server lib/ test",
        "start": "node ./bin/http-server",
        "test": "vows --spec --isolate"
    },
    "version": "0.9.0"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

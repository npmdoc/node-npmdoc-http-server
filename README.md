# api documentation for  [http-server (v0.9.0)](https://github.com/indexzero/http-server#readme)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-http-server.svg)](https://travis-ci.org/npmdoc/node-npmdoc-http-server)
#### A simple zero-configuration command-line http server

[![NPM](https://nodei.co/npm/http-server.png?downloads=true)](https://www.npmjs.com/package/http-server)

[![apidoc](https://npmdoc.github.io/node-npmdoc-http-server/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-http_server_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-http-server/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-http-server/build/screen-capture.npmPackageListing.svg)



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
            "name": "Charlie Robbins",
            "email": "charlie.robbins@gmail.com"
        },
        {
            "name": "Marak Squires",
            "email": "marak.squires@gmail.com"
        },
        {
            "name": "Charlie McConnell",
            "email": "charlie@charlieistheman.com"
        },
        {
            "name": "Joshua Holbrook",
            "email": "josh.holbrook@gmail.com"
        },
        {
            "name": "Maciej Małecki",
            "email": "maciej.malecki@notimplemented.org"
        },
        {
            "name": "Matthew Bergman",
            "email": "mzbphoto@gmail.com"
        },
        {
            "name": "brad dunbar",
            "email": "dunbarb2@gmail.com"
        },
        {
            "name": "Dominic Tarr"
        },
        {
            "name": "Travis Person",
            "email": "travis.person@gmail.com"
        },
        {
            "name": "Jinkwon Lee",
            "email": "master@bdyne.net"
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
            "name": "indexzero",
            "email": "charlie.robbins@gmail.com"
        }
    ],
    "name": "http-server",
    "optionalDependencies": {},
    "preferGlobal": "true",
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module http-server](#apidoc.module.http-server)
1.  [function <span class="apidocSignatureSpan">http-server.</span>HTTPServer (options)](#apidoc.element.http-server.HTTPServer)
1.  [function <span class="apidocSignatureSpan">http-server.</span>HttpServer (options)](#apidoc.element.http-server.HttpServer)
1.  [function <span class="apidocSignatureSpan">http-server.</span>createServer (options)](#apidoc.element.http-server.createServer)
1.  object <span class="apidocSignatureSpan">http-server.</span>HTTPServer.prototype

#### [module http-server.HTTPServer](#apidoc.module.http-server.HTTPServer)
1.  [function <span class="apidocSignatureSpan">http-server.</span>HTTPServer (options)](#apidoc.element.http-server.HTTPServer.HTTPServer)

#### [module http-server.HTTPServer.prototype](#apidoc.module.http-server.HTTPServer.prototype)
1.  [function <span class="apidocSignatureSpan">http-server.HTTPServer.prototype.</span>close ()](#apidoc.element.http-server.HTTPServer.prototype.close)
1.  [function <span class="apidocSignatureSpan">http-server.HTTPServer.prototype.</span>listen ()](#apidoc.element.http-server.HTTPServer.prototype.listen)



# <a name="apidoc.module.http-server"></a>[module http-server](#apidoc.module.http-server)

#### <a name="apidoc.element.http-server.HTTPServer"></a>[function <span class="apidocSignatureSpan">http-server.</span>HTTPServer (options)](#apidoc.element.http-server.HTTPServer)
- description and source-code
```javascript
function HttpServer(options) {
  options = options || {};

  if (options.root) {
    this.root = options.root;
  }
  else {
    try {
      fs.lstatSync('./public');
      this.root = './public';
    }
    catch (err) {
      this.root = './';
    }
  }

  this.headers = options.headers || {};

  this.cache = options.cache === undefined ? 3600 : options.cache; // in seconds.
  this.showDir = options.showDir !== 'false';
  this.autoIndex = options.autoIndex !== 'false';
  this.contentType = options.contentType || 'application/octet-stream';

  if (options.ext) {
    this.ext = options.ext === true
      ? 'html'
      : options.ext;
  }

  var before = options.before ? options.before.slice() : [];

  before.push(function (req, res) {
    if (options.logFn) {
      options.logFn(req, res);
    }

    res.emit('next');
  });

  if (options.cors) {
    this.headers['Access-Control-Allow-Origin'] = '*';
    this.headers['Access-Control-Allow-Headers'] = 'Origin, X-Requested-With, Content-Type, Accept, Range';
    if (options.corsHeaders) {
      options.corsHeaders.split(/\s*,\s*/)
          .forEach(function (h) { this.headers['Access-Control-Allow-Headers'] += ', ' + h; }, this);
    }
    before.push(corser.create(options.corsHeaders ? {
      requestHeaders: this.headers['Access-Control-Allow-Headers'].split(/\s*,\s*/)
    } : null));
  }

  if (options.robots) {
    before.push(function (req, res) {
      if (req.url === '/robots.txt') {
        res.setHeader('Content-Type', 'text/plain');
        var robots = options.robots === true
          ? 'User-agent: *\nDisallow: /'
          : options.robots.replace(/\\n/, '\n');

        return res.end(robots);
      }

      res.emit('next');
    });
  }

  before.push(ecstatic({
    root: this.root,
    cache: this.cache,
    showDir: this.showDir,
    autoIndex: this.autoIndex,
    defaultExt: this.ext,
    contentType: this.contentType,
    handleError: typeof options.proxy !== 'string'
  }));

  if (typeof options.proxy === 'string') {
    var proxy = httpProxy.createProxyServer({});
    before.push(function (req, res) {
      proxy.web(req, res, {
        target: options.proxy,
        changeOrigin: true
      });
    });
  }

  var serverOptions = {
    before: before,
    headers: this.headers,
    onError: function (err, req, res) {
      if (options.logFn) {
        options.logFn(req, res, err);
      }

      res.end();
    }
  };

  if (options.https) {
    serverOptions.https = options.https;
  }

  this.server = union.createServer(serverOptions);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.http-server.HttpServer"></a>[function <span class="apidocSignatureSpan">http-server.</span>HttpServer (options)](#apidoc.element.http-server.HttpServer)
- description and source-code
```javascript
function HttpServer(options) {
  options = options || {};

  if (options.root) {
    this.root = options.root;
  }
  else {
    try {
      fs.lstatSync('./public');
      this.root = './public';
    }
    catch (err) {
      this.root = './';
    }
  }

  this.headers = options.headers || {};

  this.cache = options.cache === undefined ? 3600 : options.cache; // in seconds.
  this.showDir = options.showDir !== 'false';
  this.autoIndex = options.autoIndex !== 'false';
  this.contentType = options.contentType || 'application/octet-stream';

  if (options.ext) {
    this.ext = options.ext === true
      ? 'html'
      : options.ext;
  }

  var before = options.before ? options.before.slice() : [];

  before.push(function (req, res) {
    if (options.logFn) {
      options.logFn(req, res);
    }

    res.emit('next');
  });

  if (options.cors) {
    this.headers['Access-Control-Allow-Origin'] = '*';
    this.headers['Access-Control-Allow-Headers'] = 'Origin, X-Requested-With, Content-Type, Accept, Range';
    if (options.corsHeaders) {
      options.corsHeaders.split(/\s*,\s*/)
          .forEach(function (h) { this.headers['Access-Control-Allow-Headers'] += ', ' + h; }, this);
    }
    before.push(corser.create(options.corsHeaders ? {
      requestHeaders: this.headers['Access-Control-Allow-Headers'].split(/\s*,\s*/)
    } : null));
  }

  if (options.robots) {
    before.push(function (req, res) {
      if (req.url === '/robots.txt') {
        res.setHeader('Content-Type', 'text/plain');
        var robots = options.robots === true
          ? 'User-agent: *\nDisallow: /'
          : options.robots.replace(/\\n/, '\n');

        return res.end(robots);
      }

      res.emit('next');
    });
  }

  before.push(ecstatic({
    root: this.root,
    cache: this.cache,
    showDir: this.showDir,
    autoIndex: this.autoIndex,
    defaultExt: this.ext,
    contentType: this.contentType,
    handleError: typeof options.proxy !== 'string'
  }));

  if (typeof options.proxy === 'string') {
    var proxy = httpProxy.createProxyServer({});
    before.push(function (req, res) {
      proxy.web(req, res, {
        target: options.proxy,
        changeOrigin: true
      });
    });
  }

  var serverOptions = {
    before: before,
    headers: this.headers,
    onError: function (err, req, res) {
      if (options.logFn) {
        options.logFn(req, res, err);
      }

      res.end();
    }
  };

  if (options.https) {
    serverOptions.https = options.https;
  }

  this.server = union.createServer(serverOptions);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.http-server.createServer"></a>[function <span class="apidocSignatureSpan">http-server.</span>createServer (options)](#apidoc.element.http-server.createServer)
- description and source-code
```javascript
createServer = function (options) {
  return new HttpServer(options);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.http-server.HTTPServer"></a>[module http-server.HTTPServer](#apidoc.module.http-server.HTTPServer)

#### <a name="apidoc.element.http-server.HTTPServer.HTTPServer"></a>[function <span class="apidocSignatureSpan">http-server.</span>HTTPServer (options)](#apidoc.element.http-server.HTTPServer.HTTPServer)
- description and source-code
```javascript
function HttpServer(options) {
  options = options || {};

  if (options.root) {
    this.root = options.root;
  }
  else {
    try {
      fs.lstatSync('./public');
      this.root = './public';
    }
    catch (err) {
      this.root = './';
    }
  }

  this.headers = options.headers || {};

  this.cache = options.cache === undefined ? 3600 : options.cache; // in seconds.
  this.showDir = options.showDir !== 'false';
  this.autoIndex = options.autoIndex !== 'false';
  this.contentType = options.contentType || 'application/octet-stream';

  if (options.ext) {
    this.ext = options.ext === true
      ? 'html'
      : options.ext;
  }

  var before = options.before ? options.before.slice() : [];

  before.push(function (req, res) {
    if (options.logFn) {
      options.logFn(req, res);
    }

    res.emit('next');
  });

  if (options.cors) {
    this.headers['Access-Control-Allow-Origin'] = '*';
    this.headers['Access-Control-Allow-Headers'] = 'Origin, X-Requested-With, Content-Type, Accept, Range';
    if (options.corsHeaders) {
      options.corsHeaders.split(/\s*,\s*/)
          .forEach(function (h) { this.headers['Access-Control-Allow-Headers'] += ', ' + h; }, this);
    }
    before.push(corser.create(options.corsHeaders ? {
      requestHeaders: this.headers['Access-Control-Allow-Headers'].split(/\s*,\s*/)
    } : null));
  }

  if (options.robots) {
    before.push(function (req, res) {
      if (req.url === '/robots.txt') {
        res.setHeader('Content-Type', 'text/plain');
        var robots = options.robots === true
          ? 'User-agent: *\nDisallow: /'
          : options.robots.replace(/\\n/, '\n');

        return res.end(robots);
      }

      res.emit('next');
    });
  }

  before.push(ecstatic({
    root: this.root,
    cache: this.cache,
    showDir: this.showDir,
    autoIndex: this.autoIndex,
    defaultExt: this.ext,
    contentType: this.contentType,
    handleError: typeof options.proxy !== 'string'
  }));

  if (typeof options.proxy === 'string') {
    var proxy = httpProxy.createProxyServer({});
    before.push(function (req, res) {
      proxy.web(req, res, {
        target: options.proxy,
        changeOrigin: true
      });
    });
  }

  var serverOptions = {
    before: before,
    headers: this.headers,
    onError: function (err, req, res) {
      if (options.logFn) {
        options.logFn(req, res, err);
      }

      res.end();
    }
  };

  if (options.https) {
    serverOptions.https = options.https;
  }

  this.server = union.createServer(serverOptions);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.http-server.HTTPServer.prototype"></a>[module http-server.HTTPServer.prototype](#apidoc.module.http-server.HTTPServer.prototype)

#### <a name="apidoc.element.http-server.HTTPServer.prototype.close"></a>[function <span class="apidocSignatureSpan">http-server.HTTPServer.prototype.</span>close ()](#apidoc.element.http-server.HTTPServer.prototype.close)
- description and source-code
```javascript
close = function () {
  return this.server.close();
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.http-server.HTTPServer.prototype.listen"></a>[function <span class="apidocSignatureSpan">http-server.HTTPServer.prototype.</span>listen ()](#apidoc.element.http-server.HTTPServer.prototype.listen)
- description and source-code
```javascript
listen = function () {
  this.server.listen.apply(this.server, arguments);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

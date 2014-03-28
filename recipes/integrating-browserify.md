# Integrating Browserify with Hapi

Given you are structuring your application using a host application and plugins, then I've found this to be a very effective way of implementing "browserfication" of my JS code.

## Implementation: Host Application

The host application is going to provide the necessary smarts to actually browserify JS source files.  My personal opinion (at this stage) is that you should bring in browserify as a direct dependency of your host application rather than relying on some middleware to do this all for you.  As the recipe logic is currently devoid of any caching it's likely that it might break out into it's own module.

So within your host application, have npm install browserify for you.  I'd recommend running the following:

```
npm install browserify --save
```

You are then going to register a [Hapi method](1) to your host application which will enable it to browserify things:

```js
var Hapi = require('hapi');
var server = Hapi.createServer('localhost', 8000);
var browserify = require('browserify');

function browserifyJS(opts) {
  return function(request, reply) {
    var b = browserify(opts);

    debug('received browserify request for request: ', request.params);
    b.add('./' + request.params.path);
    reply(b.bundle()).type('text/javascript');
  }
}

// register a custom browserify method with Hapi
server.method('browserify', browserifyJS);
```

Now, I think I'm bending the rules on Hapi methods a little here, but it feels like it works so far, so I'm going to stick with it for the moment.

## Implementation: Plugin

Implementation from the plugin side is wonderfully simple.  In your plugin registration code (`exports.register`) simply define a route for processing any JS code:

```js
plugin.route({
  method: 'GET',
  path: endpoint + '/js/{path*}',
  handler: plugin.methods.browserify({ basedir: __dirname + '/public/js' })
});
```

[1]: https://github.com/spumko/hapi/blob/master/docs/Reference.md#server-methods
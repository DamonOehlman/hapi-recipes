# Host App Provides View Layout

This recipe provides you the ability to supply your [view layouts](1) from the host application (the glue that brings all the parts together) and provide generally style-free and layout-free HTML views for your plugins.

The advantage of this approach is that you can provide a consistent UI feel through the host application, but have full control over the inner content at a plugin level.  From my experimentation so far, this feels very powerful and flexible.

## Implementation: Host Application

Within the host application we need to provide some information to the plugins as to where it is they can find the layout templates (I haven't been able to find a simpler way to do this as yet).  This can be done by providing application configuration information as part of [server configuration](2).

For example:

```js
var Hapi = require('hapi');
var pack = new Hapi.Pack();
var web = pack.server(process.env.NODE_PORT || 3000, {
  app: {
    layoutPath: __dirname + '/templates'
  },

  labels: ['web']
});
```

## Implementation: Plugin

Once the host application has defined the `layoutPath` as part of the application configuration information in a server, we can then configure the `layoutPath` in our internal plugin views:

```js
var settings = (plugin.select('web').servers[0] || {}).settings || {};

plugin.views({
  engines: {
    html: 'handlebars'
  },

  path: './templates',

  layout: true,
  layoutPath: (settings.app || {}).layoutPath
});
```

1. https://github.com/spumko/hapi/blob/master/docs/Reference.md#server.config.views

2. https://github.com/spumko/hapi/blob/master/docs/Reference.md#server-options
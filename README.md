# Hapi Recipes

A collection of __in-progress__ development recipes that I've started experimenting with while starting to develop a web app using the following components:

- [Hapi](https://github.com/spumko/hapi)
- [browserify](https://github.com/substack/node-browserify)

Specifically I'm focused on using Hapi's [Plugin Interface](https://github.com/spumko/hapi/blob/master/docs/Reference.md#plugin-interface) to allow me to create functional components of an application that are designed to work within an application "host" server.

Additionally, I'm keen to use effective tools such as browserify with Hapi using minimal abstraction.  As such, I'm largely doing away with intermediate modules that might provide a convenient "Hapi friendly" wrapper to the functionality.  From what I've seen and experienced of Hapi so far, you can achieve what you need to achieve in a few lines of code so the need for custom tool middleware is largely redundant.

## Please Contribute

There is no such thing as an expert.  I am definitely not one.  If you have used an approach that is different to something I've outlined here, then please open an issue so that we can discuss it :)

Also, feel free to fork this repo and add your own recipes!

## The Recipes

- [Host Provides View Layout, Plugins Provide View Content](recipes/hostapp-layout-plugin-content.md)
- [Integrating Browserify](recipes/integrating-browserify.md)

## License

[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/)
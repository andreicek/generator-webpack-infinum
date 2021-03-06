infinitely-static
===================

This is a static page generator with basic support for routing. The idea
behind this tool is to streamline development of static webpages with
the best of Webpack and related tools.

## What is included?

* Linting tools with sane defaults - stylelint and eslint
* Hot reloading in development
* Babel with env preset activated that takes care of polyfills, as well
* JavaScript minification and dead code removal
* SASS compilation, prefixing, and minification
* A library for managing media breakpoints ([media-blender](https://github.com/infinum/media-blender))
* [Handlebars](http://handlebarsjs.com/) as a templating language (with helpers, layouts, and partials)
* Support for routes (flat and nested build structure)

## Getting started

Running this is really simple. You'll need this generator and `yo` installed.

```bash
npm install -g yo generator-infinitely-static
mkdir my-project
cd my-project
git init
yo infinitely-static
```

**Note**: After the project is initialized run `npm install husky --save-dev`.

## Development

When Yeoman finishes you have a working project.

### Running hot reload server

```
npm start
```

### Production build

```
npm run build
```

### Routes

Adding routes is also simple. In the root of the project you will find `routes.json`, containing the initial `index` route. The route configuration also supports nesting and template data.

```javascript
{
  "index": { // points to the template file in app/templates/pages/index.hbs
    "route": "/", // don't forget the trailing slash
    "context": { // data that you can use in the page
      "user": {
        "name": "Super user"
      }
    }
  },
  "contact": {
    "route": "contact/me/" // will generate nested routes
    }
  }
}
```

Afterwards, in your templates you can use the included `{{linkTo}}` helper like this:

```html
<a href="{{linkTo 'index'}}">Home</a>
```

And for the user data you can use the `getDataAsString` helper:

```html
<h1>{{getDataAsString 'user.name'}}</h1>
```

If the data is simple (array, string, Number, etc.) it will be shown as usual, but
if you reference an object you'll get a stringified JSON. But, remember, the data can
be accessed directly by using the `htmlWebpackPlugin.options` object in the template:

```html
<h1>{{htmlWebpackPlugin.options.context.user.name}}</h1>
```

That way you can iterate thru an array specified in the context using the build-in
helpers.

## License

The MIT License

![](https://assets.infinum.co/assets/brand-logo-9e079bfa1875e17c8c1f71d1fee49cf0.svg) © 2016 Infinum Inc.

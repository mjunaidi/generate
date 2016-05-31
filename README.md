# generate [![NPM version](https://img.shields.io/npm/v/generate.svg?style=flat)](https://www.npmjs.com/package/generate) [![NPM downloads](https://img.shields.io/npm/dm/generate.svg?style=flat)](https://npmjs.org/package/generate) [![Build Status](https://img.shields.io/travis/generate/generate.svg?style=flat)](https://travis-ci.org/generate/generate)

Fast, composable, highly pluggable project generator with a user-friendly and expressive API.

You might also be interested in [base](https://github.com/node-base/base).

## TOC

- [Install](#install)
- [What is generate?](#what-is-generate)
- [CLI](#cli)
- [Quickstart](#quickstart)
- [More info](#more-info)
  * [Feature highlights](#feature-highlights)
  * [FAQ](#faq)
- [Related projects](#related-projects)
- [Contributing](#contributing)
- [Building docs](#building-docs)
- [Running tests](#running-tests)
- [Author](#author)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Install

Install globally with [npm](https://www.npmjs.com/)

```sh
$ npm install -g generate
```

## What is generate?

Generate is a new, open source developer framework for rapidly initializing and scaffolding out new code projects. Generate offers a powerful and expressive API that makes it easy and enjoyable to author generators, and an intuitive CLI that helps you stay productive.

**Example**

This example shows two generators working together seamlessly.

![Example of how to generate a gulpfile.js](demo.gif)

**Want to know more?**

You can use generate from the command line, or as a node.js library as a part of your own application.

* Jump to [feature highlights](#feature-highlights)
* Visit the [getting started guide](https://github.com/generate/getting-started)

Continue on, and start generating!

## CLI

**Installing the CLI**

To run generate from the command line, you'll need to install it globally first. You can do that now with the following command:

```sh
$ npm i -g generate
```

This adds the `gen` command to your system path, allowing it to be run from any directory.

You should now be able to use the `gen` command to execute code in a local `generator.js` file, or to execute globally installed generators by their [aliases](#aliases).

## Quickstart

The following intro only skims the surface of what generate has to offer. For a more in-depth introduction, we highly recommend visiting the [getting started guide](https://github.com/generate/getting-started).

**Create a generator**

Add a `generator.js` to the current working directory with the following code:

```js
module.exports = function(app) {
  console.log('success!');
};
```

**Run a generator**

Enter the following command:

```sh
gen
```

If successful, you should see `success!` in the terminal.

**Create a task**

Now, add a task to your generator.

```js
module.exports = function(app) {
  app.task('default', function(cb) {
    console.log('success!');
    cb();
  });
};
```

Now, in the command line, run:

```sh
$ gen
# then try
$ gen default
```

When a local `generator.js` exists, the `gen` command is aliased to automatically run the `default` task if one exists. But you can also run the task with `gen default`.

**Run a task**

Let's try adding more tasks to your generator:

```js
module.exports = function(app) {
  app.task('default', function(cb) {
    console.log('default > success!');
    cb();
  });
  
  app.task('foo', function(cb) {
    console.log('foo > success!');
    cb();
  });

  app.task('bar', function(cb) {
    console.log('bar > success!');
    cb();
  });
};
```

Now, in the command line, run:

```sh
$ gen
# then try
$ gen foo
# then try
$ gen foo bar
```

**Run task dependencies**

Now update your code to the following:

```js
module.exports = function(app) {
  app.task('default', ['foo', 'bar']);
  
  app.task('foo', function(cb) {
    console.log('foo > success!');
    cb();
  });

  app.task('bar', function(cb) {
    console.log('bar > success!');
    cb();
  });
};
```

And run:

```sh
$ gen
```

You're now a master at running tasks with generate! You can do anything with generate tasks that you can do with [gulp](http://gulpjs.com) tasks (we use and support gulp libraries after all!).

**Next steps**

But generate does much more than this. For a more in-depth introduction, we highly recommend visiting the [getting started guide](https://github.com/generate/getting-started).

## More info

### Feature highlights

Generate offers an elegant and robust suite of methods, carefully organized to help you accomplish common activities in less time, including:

* **unparalleled flow control**: through the use of [generators](https://github.com/generate/getting-started), [sub-generators](https://github.com/generate/getting-started) and [tasks](https://github.com/generate/getting-started)
* **templates, scaffolds and boilerplates**: generate a single file, initialize an entire project, or provide ad-hoc "components" throughout the duration of a project using any combination of [templates, scaffolds and boilerplates](#templates-scaffolds-and-boilerplates).
* **any engine**: use any template engine to render templates, including [handlebars](http://www.handlebarsjs.com/), [lodash](https://lodash.com/), [swig](https://github.com/paularmstrong/swig) and [pug](http://jade-lang.com)
* **prompts**: asks you for data when it can't find what it needs, and it's easy to customize prompts for any data you want.
* **data**: gathers data from the user's environment to populate "hints" in user prompts and render templates
* **streams**: interact with the file system, with full support for [gulp](http://gulpjs.com) and [assemble](https://github.com/assemble/assemble) plugins
* **smart plugins**: Generate is built on [base](https://github.com/node-base/base), so any "smart" plugin can be used
* **stores**: persist configuration settings, global defaults, project-specific defaults, answers to prompts, and so on.

Visit the [getting started guide](https://github.com/generate/getting-started) to learn more.

### FAQ

<a name="aliases">

**What's an alias, and what do they do?**

Generate tries to find globally installed generators using an "alias" first, falling back on the generator's full name if not found by its alias.

A generator's alias is created by stripping the substring `generate-` from the _full name_ of generator. Thus, when publishing a generator the naming convention `generate-foo` should be used (where `foo` is the alias, and `generate-foo` is the full name).

Note that **no dots may be used in published generator names**. Aside from that, any characters considered valid by npm are fine.

## Related projects

Generate shares a common architecture and plugin ecosystem with the following libraries:

* [assemble](https://www.npmjs.com/package/assemble): Assemble is a powerful, extendable and easy to use static site generator for node.js. Used… [more](https://www.npmjs.com/package/assemble) | [homepage](https://github.com/assemble/assemble)
* [base](https://www.npmjs.com/package/base): base is the foundation for creating modular, unit testable and highly pluggable node.js applications, starting… [more](https://www.npmjs.com/package/base) | [homepage](https://github.com/node-base/base)
* [update](https://www.npmjs.com/package/update): Easily keep anything in your project up-to-date by installing the updaters you want to use… [more](https://www.npmjs.com/package/update) | [homepage](https://github.com/update/update)
* [verb](https://www.npmjs.com/package/verb): Documentation generator for GitHub projects. Verb is extremely powerful, easy to use, and is used… [more](https://www.npmjs.com/package/verb) | [homepage](https://github.com/verbose/verb)

## Contributing

This document was generated by [verb](https://github.com/verbose/verb), please don't edit directly. Any changes to the readme must be made in [.verb.md](.verb.md). See [Building Docs](#building-docs).

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/generate/generate/issues/new).

## Building docs

Generate readme and API documentation with [verb](https://github.com/verbose/verb):

```sh
$ npm install -g verb verb-readme-generator && verb
```

## Running tests

Install dev dependencies:

```sh
$ npm install -d && npm test
```

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT license](https://github.com/generate/generate/blob/master/LICENSE).

***

_This file was generated by [verb](https://github.com/verbose/verb), v0.9.0, on May 30, 2016._
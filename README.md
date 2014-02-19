Asimov
=================
**A modern framework for building your frontend**

Asimov is a rethinking of frontend frameworks in a modern style. The aim is to move away from today's all encompassing frameworks to a modular components approach.

# Table of Contents

1. [Why Asimov](#why-asimov)
  * [The problem](#the-problem)
  * [Our solution](#our-solution)
  * [Built for today](#build-for-today)
    * [Technology behind Asimov](#technology-behind-asimov)
2. [Getting started](#getting-started)
  * [System requirements](#system-requirements)
  * [Use it like bootstrap](#use-it-like-bootstrap)
  * [Direct integration](#direct-integration)
3. [Architecture](#archeticure)
4. [Core](#core)
  * [Settings](#core-settings)
    * [Aliases](#aliases)
    * [Lazys](#lazys)
    * [Functions](#functions)
      * [get](#get)
      * [set](#set)
      * [set-default](#set-default)
      * [lazy](#lazy)
    * [Mixins](#mixins)
5. [Components](#components)
  * [Using a component](#component-usage)
  * [Anatomy of a component](#components-anatomy)
    * [Settings](#component-output)
    * [Functions](#component-functions)
    * [Mixins](#component-mixins)
    * [Output](#component-output)
  * [Writing your first component](#component-create)
6. [Themes](#themes)
  * [Using a theme](#theme-usage)
  * [Anatomy of a theme](#themes-anatomy)
    * [Settings](#theme-output)
    * [Functions](#theme-functions)
    * [Mixins](#theme-mixins)
    * [Components](#theme-components)
    * [Output](#theme-output)
  * [Writing your first theme](#theme-create)
7. [FAQ](#faq)
  * [Why the strange import paths?](#why-the-strange-import-paths)
  * [Why not namespace under Asimov?](#why-not-namespace-under-asimov)
8. [License](#license)

## Why Asimov

Over recent years we've experienced rapid increase in the complexity of frontend engineering.

With the increased complexity grew a need for ways to easily build good looking responsive sites. A lot of projects have taken on the challenge, with a couple noteable successes in [bootstrap](http://getboostrap.com) and [foundation](http://foundation.zurb.com).

Asimov is a re-thinking of current frontend frameworks that attempts to address some of the [new problems](#problems) we've created.

### The problem

Traditionally frontend frameworks have taken the kitchen sink approach. What starts off as a humble set of sane defaults, grows over time into forms, dropdowns, modals etc.. The larger a framework gets the more difficult it becomes to use only certain parts of a framework.

As this growth happens a framework will inevitably develop its own theme which can be hard to separate from its individual components. That coupling between theme and structure can, in some cases, make developing your own distinct visual style very difficult. The result is your site looks notably similiar to many others.

### The solution

Framework growth, and coupling between theme and structure are two problems Asimov tries to solve.

At its heart Asimov is an eco-system of small single purpose components, that are composed into a framework. You can pick and choose which components you need, or use an existing collection of components. You can then choose to compile those components into css and js files for distribution, ala bootstrap, or import them directly into your existing application.

To avoid the tight coupling between theme and structure we've adopted many of the great ideas created by [Nicole Sullivan](https://twitter.com/stubbornella) and the [OOCSS](https://github.com/stubbornella/oocss/wiki) team, thanks team!

Primarily, Asimov components adopts the concept of separating structure and skin (theme), which the OOCSS team describes as:

> This means to define repeating visual features (like background and border styles) as separate “skins” that you can mix-and-match with your various objects to achieve a large amount of visual variety without much code.

Although the Asimov implementation is different, the idea remains the same.

### Built for today

We felt it was important to use the latest generation of tools and techniques to tackle the current day problems. With that in mind the Asimov project has been influenced by work done by many great minds.

#### Technology behind Asimov

We're proud to have built on the shoulders of giants!

To build Asimov use

- [Sass](http://sass-lang.com)
- [Bower](http://bower.io)
- Some [OOCSS](https://github.com/stubbornella/oocss/wiki) concepts
- Some [BEM](http://bem.info/method/definitions/) concepts
- [RequireJS](http://requirejs.org)
- [Grunt](http://gruntjs.com) __optional__

Asimov has also been influenced by these great projects

- [Bootstrap](http://getbootstrap.com)
- [Foundation](http://foundation.zurb.com)
- [Topcoat](http://topcoat.io)
- [SUIT](https://github.com/suitcss)


## Getting started

Your projects can consume Asimov in two ways, by using a [pre-compiled distribution](#use-it-like-bootstrap) or by importing components directly into your [existing Sass projects](#direct-integration).

Compiling a collection of components and a their theming variable to a static distribution is done with [themes](#themes). Using themes allows for easy sharing of compiled assets, theming variables, and version controlling - however using themes is optional. You can just as easily bower install Asimov components [directly into your project](#direct-integration) and use Sass `@import` to load components and/or their mixins.

### System requirements

Before you proceed you'll need to install the following on your system:

- Git
- Ruby 1.9+
- NodeJS 0.8.0+

You'll also need bower to install Asimov components:

```bash
sudo npm install bower -g --save-dev
```

Sass 3.3 to compile Asimov, either via `gem`

```bash
gem install sass --pre
```

or `bundler` by adding the following to your `Gemfile`

```bash
gem "sass", "~> 3.3.0.rc.4"
```

### Use it like bootstrap

Asimov themes are collection of components and pre-set theming variables that can compiled to static assets that you can include into your markup the same as you would any other project. This is the easiest, and recommended way to consume Asimov in your project. [TODO: link to Isaac any other themes when we have some].

To install a theme download its `dist` folder into a publicly accessible directory of your project, or use [bower](http://bower.io) to do that for you.

If you would also like to [include](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#including_a_mixin) or [extend](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#extend) Asimov components you can do so by **also** [directly integrating](#direct-integration) a theme or component into your project.

### Direct integration

If you're already using Sass and bower you can bower install Asimov components and configure your theme variables directly within your project. If you go down this path there a things you need to know:

1. you'll need to add the bowered asimov components to [Sass's load-path](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#import) so they can be imported
2. component css will only be generated if it has been `@import`ed into a compiled file
3. if components require javascript you will need to add the bowered asimov components to [requirejs's paths config](http://requirejs.org/docs/api.html#config-paths)

__If you're already using a [theme's distribution files](#direct-integration) only the first point is required__

**Warning: if you're using a theme's distribution files and also bower installing the theme or any of its components make sure you're using the same or compatible versions. Asimov uses semver 2.0 for version control, you can learn all about it [here](http://semver.org/spec/v2.0.0.html)**

Once the Sass load-path has been configured you can `@import` components with the path `<component-name>/(mixin,component)/<component-name>` (__[Why the strange import paths?](#why-the-strange-import-paths)__) eg:

#### Output an entire component

This will output the entire grid component.

```scss
@import "asimov/asimov";
@import "grid/components/grid";
```

#### Using a component's mixins

This will mix `grid-row` into `.my-div`, but not output the entire grid component itself. So although `my-div` knows how to active a grid row the `.row` class wont be available to other dom elements.

```scss
@import "asimov/asimov";
@import "grid/components/grid";

.my-div {
  @include grid-row;
}
```

When using any Asimov functions, mixins, or components in your Sass files you currently need to `@import "asimov/asimov";` to bootstrap Asimov.


## Architecture

Unlike some frontend frameworks Asimov is not one project, but a group of projects that work together: [asimov-core](https://github.com/asimov/asimov-core), [asimov-build](https://github.com/asimov/asimov-build), asimov components _[TODO: link to component directory when ready]_, and themes _[TODO: link to theme directory when ready]_. 

Asimov core is the base set of Sass and javascript function that are utilised by all the other Asimov projects. Check out the [Core](#core) documentation to learn more.

Asimov build is the build logic for compiling Asimov themes. If you choose to [direct integration](#direct-integration) over using a theme Asimov build is a template of the what you'll need to compile your Asimov components. At the moment it relies on [Grunt](http://gruntjs.com) but the goal is to be set of scripts that are agnostic to how they're executed.

Components are the real work horses. That's where the mixins you consume, and the css you serve are defined. Components are self-contained peices with all the css, javascript, fonts, images and other assets they need to render. Components can also depend on other components. This means composing sophisticated components can be done with very little code since a lot of the grunt work may have already been done for you.

Themes are simply a collection of components and theming variables. Themes can be bower installed into your project, or compiled into a distribution with asimov-build.

All said and done the Asimov architecure is very similiar other module or plugin based projects like Grunt.

![Asimov architecure](../docs/as-markdown/images/asimov-architecture.png?raw=true)


## Core

The backbone of Asimov's theming power is the settings API. All every peice of the Asimov eco-system interacts with settings API, and it lives within Asimov core.

### Settings

The settings API is the interface for Asimov's internal settings data store. With the settings API you can retrieve and store any valid Sass literal, via the [get](#get) and [set](#set) functions.

Components will try to `get` settings so they can theme themselves eg:

```scss
// a button component

.button {
  display: block;
  ...
  font-size: get('button-component/font-size');
  background: get('button-component/background');
}
```

If there is not value set yet `get` will return `null`. (__[Why do you return null?](#why-the-strange-import-paths)__)

#### Aliases

#### Lazys

### Functions

#### get

Gets `$key`s value.

| param    | type   |
:----------|:-------|
| `$key`   | String |

In order reference a nested key, treat it's parents as a directory, separating them by a  `/` eg.

```scss
$settings: set(("foo": (
    "bar": (
        "baz": "test",
     ),
));

@debug(get("foo/bar/baz"));
```

#### set

Sets `$key`s value to `$value`.

| param    | type          |
:----------|:--------------|
| `$key`   | String or Map |
| `$value` | Literal       |

If `$key` is a `String` then `$value` is recursively merged with `$key`s current value.  
The new value for `$key` is returned.

If `$key` is a `Map` then `$key` is recursively merged with settings and `$value` is ignored.  
A copy of the updated settings map is returned.

#### set-default

Sets `$key`s value to `$value` only if it currently has no value. This emulates Sass's native [!default](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#variable_defaults_).

| param    | type          |
:----------|:--------------|
| `$key`   | String or Map |
| `$value` | Literal       |

If `$key` is a `String` then `$value` is recursively merged with `$key`s current value.  
The new value for `$key` is returned.

If `$key` is a `Map` then `$key` is recursively merged with settings and `$value` is ignored.  
A copy of the updated settings map is returned.

#### lazy

Serializes a call to `$func` with arguments `$args` that can be later evaluated by [get](#get).  
If the value of `get($key)` is a lazy, it will evaluated and the returned value is returned.  
The primary use case is to evaluate aliased values at runtime.

| param   | type   |
:---------|:-------|
| `$func` | String |
| `$args` | Map    |

### Mixins

#### responsive-property

This mixin outputs `$property: get($key);` where `$key` is a map who's keys are breakpoint names returned by `get("breakpoints")` eg:

```scss
$settings: ("my-component": (
  "background": (
    "mobile": #f00,
    "tablet": #0f0,
    "desktop": #00f,
  ),
));

.foo {
  @include responsive-property("my-component/background", $background-color);
}

// outputs (using the `mobile`, `tablet` and `desktop` breakpoints sample data);

@media (min-width: 0) and (max-width: 599px) {
  .foo {
    background-color: #f00;
  }
}
@media (min-width: 600px) and (max-width: 899px) {
  .foo {
    background-color: #0f0;
  }
}
@media (min-width: 900px) {
  .foo {
    background-color: #00f;
  }
}
```

| param       | type   |
:-------------|:-------|
| `$key`      | String |
| `$property` | String |


## Components

### Using a component

To use a component in your project you need to first install it via bower.  
You can find a list of official public components in the [Asimov github organisation](https://github.com/search?q=contrib+user%3Aasimov&type=Repositories&ref=searchresults).

```bash
$ bower install asimov/<repository> --save
```

### Anatomy of a component

#### Settings

#### Functions

#### Mixins

#### Output

### Writing your first component


## Themes

TBA

### Using a theme

TBA

### Anatomy of a theme

TBA

#### Settings

TBA

#### Functions

TBA

#### Mixins

TBA

#### Components

TBA

#### Output

TBA

### Writing your first theme

TBA



























## FAQ

I'm sure you've got a lot of questions. Asimov is the accumulation of a bunch of great from some really smart people. As a result there's a lot to cover, and some required background knowledge. We've tried our best below to explain how and why we did some of the things we did. If there's something that's still unclear or you could be explained better please open [an issue](https://github.com/asimov/asimov.io/issues) to help us fix it! :)

### Why the strange import paths?

The reason we repeat the component name in import paths is acheive a type of namespacing. It's unrealistic to expect all projects wanting to use Asimov won't already have Sass to css of their own. We've been mindful of this when building Asimov so some decisions have been made to ease the integration process.

It's likely a project will already have a `mixins/button` file. With Sass's import model, only one of these files would importable, which would make integration much harder. We needed to namespace Asimov components from any existing Sass.

### Why not namespace under Asimov?

We could have. This what popular Sass libraries like bourbon and foundation do.

The reason we chose not to do namespace under Asimov is because of the distributed nature of Asimov components. No one person owns all Asimov components. This is one of the great things about Asimov, but we've also got to be mindful of it when making these kinds of choices.

For example if two people were to create button components that we're very different, they'd both likely have an `asimov/mixins/button` file. Which file should be loaded when importing `asimov/mixins/button`? Now you're in a pickle :( By allowing users to choose their component's namespace these problems are less likely to appear, and much easier to resolve if they do.



## License

Made available under the [MIT License (MIT)](https://github.com/asimov/asimov.io/blob/master/LICENSE).


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
2. [Getting started](#intro-getting-started)
  * [Use it like bootstrap](#use-it-like-bootstrap)
  * [Direct integration](#direct-integration)
3. [Architecture](#archeticure)
4. [Core](#core)
  * [Settings](#core-settings)
  * [API](#core-api)
    * [Functions](#core-functions)
    * [Mixins](#core-mixins)
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

# Why Asimov

Over recent years we've experienced rapid increase in the complexity of frontend engineering.

With the increased complexity grew a need for ways to easily build good looking responsive sites. A lot of projects have taken on the challenge, with a couple noteable successes in [bootstrap](http://getboostrap.com) and [foundation](http://foundation.zurb.com).

Asimov is a re-thinking of current frontend frameworks that attempts to address some of the [new problems](#problems) we've created.

## The problem

Traditionally frontend frameworks have taken the kitchen sink approach. What starts off as a humble set of sane defaults, grows over time into forms, dropdowns, modals etc.. The larger a framework gets the more difficult it becomes to use only certain parts of a framework.

As this growth happens a framework will inevitably develop its own theme which can be hard to separate from its individual components. That coupling between theme and structure can, in some cases, make developing your own distinct visual style very difficult. The result is your site looks notably similiar to many others.

## The solution

Framework growth, and coupling between theme and structure are two problems Asimov tries to solve.

At its heart Asimov is an eco-system of small single purpose components, that are composed into a framework. You can pick and choose which components you need, or use an existing collection of components. You can then choose to compile those components into css and js files for distribution, ala bootstrap, or import them directly into your existing application.

To avoid the tight coupling between theme and structure we've adopted many of the great ideas created by [Nicole Sullivan](https://twitter.com/stubbornella) and the [OOCSS](https://github.com/stubbornella/oocss/wiki) team, thanks team!

Primarily, Asimov components adopts the concept of separating structure and skin (theme), which the OOCSS team describes as:

> This means to define repeating visual features (like background and border styles) as separate “skins” that you can mix-and-match with your various objects to achieve a large amount of visual variety without much code.

Although the Asimov implementation is different, the idea remains the same.

## Built for today

We're proud to have built on the shoulders of giants.

We felt it was important to use the latest generation of tools and techniques to tackle the current day problems. With that in mind the Asimov project has been influenced by work done by many great minds.


# Getting started

Your projects can consume Asimov in two ways, by using a [pre-compiled distribution](#use-it-like-bootstrap) or by importing components directly into your [existing Sass projects](#direct-integration).

Compiling a collection of components and a their theming variable to a static distribution is done with [themes](#themes). Using themes allows for easy sharing of compiled assets, theming variables, and version controlling - however using themes is optional. You can just as easily bower install Asimov components [directly into your project](#direct-integration) and use Sass `@import` to load components and/or their mixins.

## Use it like bootstrap

Asimov themes are collection of components and pre-set theming variables that can compiled to static assets that you can include into your markup the same as you would any other project. This is the easiest, and recommended way to consume Asimov in your project. [TODO: link to Isaac any other themes when we have some].

To install a theme download its `dist` folder into a publicly accessible directory of your project, or use [bower](http://bower.io) to do that for you.

If you would also like to [include](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#including_a_mixin) or [extend](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#extend) Asimov components you can do so by **also** [directly integrating](#direct-integration) a theme or component into your project.

## Direct integration

If you're already using Sass and bower you can bower install Asimov components and configure your theme variables directly within your project. If you go down this path there a things you need to know:

1. you'll need to add the bowered asimov components to [Sass's load-path](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#import) so they can be imported
2. component css will only be generated if it has been `@import`ed into a compiled file
3. if components require javascript you will need to add the bowered asimov components to [requirejs's paths config](http://requirejs.org/docs/api.html#config-paths)

__If you're already using a [theme's distribution files](#direct-integration) only the first point is required__

**Warning: if you're using a theme's distribution files and also bower installing the theme or any of its components make sure you're using the same or compatible versions. Asimov uses semver 2.0 for version control, you can learn all about it [here](http://semver.org/spec/v2.0.0.html)**

Once the Sass load-path has been configured you can `@import` components with the path `<component-name>/(mixin,component)/<component-name>` (__[Why the strange import paths?](#why-the-strange-import-paths)__) eg:

### Output an entire component

This will output the entire grid component.

```scss
@import "asimov/asimov";
@import "grid/components/grid";
```

### Using a component's mixins

This will mix `grid-row` into `.my-div`, but not output the entire grid component itself. So although `my-div` knows how to active a grid row the `.row` class wont be available to other dom elements.

```scss
@import "asimov/asimov";
@import "grid/components/grid";

.my-div {
  @include grid-row;
}
```

When using any Asimov functions, mixins, or components in your Sass files you currently need to `@import "asimov/asimov";` to bootstrap Asimov.

































# FAQ

I'm sure you've got a lot of questions. Asimov is the accumulation of a bunch of great from some really smart people. As a result there's a lot to cover, and some required background knowledge. We've tried our best below to explain how and why we did some of the things we did. If there's something that's still unclear or you could be explained better please open [an issue](https://github.com/asimov/asimov.io/issues) to help us fix it! :)

## Why the strange import paths?

The reason we repeat the component name in import paths is acheive a type of namespacing. It's unrealistic to expect all projects wanting to use Asimov won't already have Sass to css of their own. We've been mindful of this when building Asimov so some decisions have been made to ease the integration process.

It's likely a project will already have a `mixins/button` file. With Sass's import model, only one of these files would importable, which would make integration much harder. We needed to namespace Asimov components from any existing Sass.

## Why not namespace under Asimov?

We could have. This what popular Sass libraries like bourbon and foundation do.

The reason we chose not to do namespace under Asimov is because of the distributed nature of Asimov components. No one person owns all Asimov components. This is one of the great things about Asimov, but we've also got to be mindful of it when making these kinds of choices.

For example if two people were to create button components that we're very different, they'd both likely have an `asimov/mixins/button` file. Which file should be loaded when importing `asimov/mixins/button`? Now you're in a pickle :( By allowing users to choose their component's namespace these problems are less likely to appear, and much easier to resolve if they do.



# License

Made available under the [MIT License (MIT)](https://github.com/asimov/asimov.io/blob/master/LICENSE).


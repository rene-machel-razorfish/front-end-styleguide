# Razorfish Front End Style Guide

## Preface
> Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live. ~Martin Golding


Some people claim their code doesn't need documentation - it would explain itself.
Some people claim their code doesn’t need structure - rules would hinder their creativity.
Some people claim their code doesn’t need testing - it won’t change.
Well, that’s just not true. Coding is not “writing the code” is about maintaining the code. The more readable, structured, tested our code is, the easier it is to maintain and to extend.

A consistent style guide, a complete set of automated tests which are enforced and automated as much as possible helps to improve the overall quality and maintainability of every project. If you're working with a common setup in a familiar structure you already have a head start in every project. It's easier to browse, locate and fix bugs if you instantly know what is happening.
Think about the other developers stepping in to assist you in the last sprint and maintaining the code in the next years.
Just think about yourself when you have to change a feature you wrote two months ago - consistent code will certainly save time in the long haul.


## Scope
This document will outline the general project structure and define the basic rules for writing CSS, HTML, JavaScript and all that matters from a presentation layer perspective.
These rules are mandatory. Do not skip the commit-hooks, do not ignore the validation errors. They are part of the “definition of done”.

## Setup

### Requirements
You'll need at least

- [Node.js][nodejs] and [Node Packet Manager (npm)][npm]
- [Grunt.js][gruntjs]
- [Bower][bower]
- [Git][git]


<!--
- [chai]
- [mocha]
- [sinon]
 -->

Assuming that you have all the required tools installed, just run: `$ npm install`.

## Revision Control
We are using [Git][git] and the [git-flow][git-flow] branching-model. If you are not familiar with git, or just need a reference: take a look at the [Pro-Git Book][git-book].
We believe that the source control is for source files only. Don't add “compiled”-files (`release`/`build`/`minified`) or “third-party-libraries”, e.g. no `node_modules` / `bower_components` / `*.min.*` to the repository.
If you're project uses as css-pre/post-processor such as sass or myth - do not add the compiled/processed files either.
This just results in merge conflicts and defeats the purpose of ”revision control”.
Every commit needs a commit message. Keep them short and simple but verbose and refer to the JIRA if possible.
Please keep in mind that as soon as you commit to a “public”-branch (not your private “feature-branch”) everyone else depends on your code. To make sure you do not accidentally break the build, we have a `git-hook which validates and tests the files.


## Licenses
When working with third-party-items (script/widget/framework/fonts etc.), check for their license. Use only items that are released under the **MIT** or **GPL**-License. Otherwise, make sure you actually have the rights to use it.  Preserve the original copyright notice and a link to the original source.
If you're using “webfonts” never “just use this file”. Verify with the technical lead or the project manager that they own a proper license specifically for this project.

## TL;DR

- Always use a proper work flow, take a look at the [git-workflows][Atlassian Git Workflows] or just stick to the default [git-flow][git-flow].
- Commit as often as possible.
- Use short and simple but verbose commit messages. If possible, refer to the JIRA.
- Do not commit to the master-branch unless you're entitled to.
- Use [bower][bower] for dependency management.
- No “compiled” files inside the repository (`node_modules`, `bower_components` etc).
- The default language is English. Even for variable and function naming.
- Preserve the license, author and version.
- Intend using Tabs.


## Build & Deployment
Automation simplifies a lot, the less you have to worry about minification, compilation, unit testing, linting, the easier your job becomes. The CI-Server creates the build-packages and deploys them automatically so you don't have to worry about this.
Remember: During the build, all css and javascript files will be concatenated, minified, and *validated* - an error will break the build.

### Grunt
As mentioned before, we're using [grunt.js][gruntjs]. The Razorfish-Boilerplate contains a lot of pre-configured tasks. Just type `$ grunt --help` to see a list or take a look at `./grunt/tasks/`.

To add a new file to the project, edit the “sources.scripts.project” / “sources.scripts.vendor” / “sources.styles.project” / “sources.styles.vendor” properties. They will distribute the files to all the tasks, in the order you entered them and vendor-files before project-files. Afterwards, type `$ grunt create-loader` / `$ grunt create-loader:styles` / `$ grunt create-loader:scripts`.
Please note: the default development setting will use the original files. If you create a “release” with `$ grunt release` the minified files are used there.


### TL;DR
- Always use a build system and a deployment strategy.
- Failing tests or validation errors will break your build.
- Deploy only minified and concatenated files.
- Deploy as less files as possible.
- To add css or js files: update the source-property in the pacakge.json and run `$ grunt create-loader`


## Coding Style
> All code in any code-base should look like a single person typed it, no matter how many people contributed. idiomatic.js

### TL;DR
- Be consistent.
- Prefer readability.
- Prefer simplicity.
- Don't repeat yourself.
- Use real tabs.
- Use UTF-8 for everything. Consider using [EditorConfig][editorconfig].
- Write smart code.
- Write meaningful comments. A lot.
- Think about performance. Cache as much as possible.
- No dead code. Delete legacy content.
- Test everything. Every time.

### Comments
Well commented code is extremely important. Take your time to describe components, how they work, their limitations, and the way they are constructed. Never leave others guessing about the purpose of uncommon or non-obvious code. The more “advanced” your code feels, the more commentary it needs.
Every file requires a description. Every function a block comment with it's purpose, the arguments and the return value.
Additionally, use inline comments to state your intentions - think about these as annotations to your source code.
We will generate a complete documentation based on your comments. Take a look at the `./docs/`-folder and get a feeling for your comments.


## HTML
Write semantic HTML. Always use elements for what they have been created for. For example, use `heading` elements for headings, `p` elements for paragraphs, `a` elements for anchors, etc. Strictly keep structure (markup), presentation (styling), and behavior (scripting) apart, and try to keep the interaction between the three to an absolute minimum. Follow the principles of [Progressive Enhancement][progressive_enhancement] and opt for “mobile first”.
Look at the “Browser-Matrix” and test your code on every useragent / viewport that is required. Test early and often during development. An “internet-explorer-test” for the first time at the end of your development is just not acceptable.
We’re using UTF-8, make sure your IDE is on board. Besides: there is no need to use entity references like &mdash;, &rdquo;, or &#x263a; anymore.

### TL;DR
- Use HTML5 with the minimal Doctype: `<!DOCTYPE html>`.
- Follow the principles of [Progressive Enhancement][progressive-enhancement].
- Go for “mobile first”.
- Separate structure from presentation from behavior.
- Use semantic HTML - use elements for what they have been created for.
- Use as few elements as possible. Never clutter the document.
- Avoid cascading `<div>` tags.
- Always put double quotes around attributes.
- Close all elements. Except self-closing ones.
- Use valid HTML code.
- *Lint* and *test* your files.


## CSS

### TL;DR
- Write comments.
- Read [Scalable and Modular Architecture for CSS][smacss] for a deeper understanding.
- Use one file per `module` or 'component'. Follow the naming-conventions.
- Minimize HTTP-Requests. Use [CSS Sprites][css-sprites] and [Icon Fonts][icon-fonts].
- Avoid camelCase, underscores and cryptic name.
- Write [efficient selectors][efficient-selectors]. Don't tag-qualify.
- Keep selectors as simple and short as possible. Max three levels deep,
- Avoid inline styling.
- Use one file per module. Every module should be independent.
- Intend using Tabs.
- *Lint* your files


### Architecture
We like the ideas of [Scalable and Modular Architecture for CSS][smaccs].

> There are five types of categories:
> - Base
> - Layout
> - Module
> - State
> - Theme

#### Base rules `./styles/base/`
 > Essentially, a base style says that wherever this element is on the page, it should look like this.

The base rules are mostly:
- [normalize-css][normalize.css], which is part of the `bower_components`
- `reset.css`: some basic resets and `box-sizing: border-box;`
- `fonts.css`: your webfonts
- `typography.css`: your default font-styles. Keep a [vertical rhythm][css-vertical-rhythm] and strife for readability.
- `base.css`: additional basic styles
- `legacy.css`: special styles for legacy user agents such as IE8


#### Layout rules `./styles/layout/`
 > Layout rules divide the page into sections. Layouts hold one or more modules together.

The layout rules are mostly:
- `grid.css`:  the overall gid

#### Modules rules `./styles/modules/`
 > Modules are the reusable, modular parts of our design.

This is the main part of your site. Use one file per module and stick to the naming conventions.
Modules might inherit styles. For example: a lot of your modules should have a `.base-module`class to inherit the basic styling.
Keep all styles for a specific module in __one__ file, e.g.: place state rules next to the module rules.

There's at least
 - `_template.css`: a basic template
 - `base.css`: default styles for all modules.

For starters: Look at the `_template.css`.

#### State rules
> They are ways to describe how our modules or layouts will look when in a particular state.

Place state rules next to the module rules to which they apply. Keep all styles for a specific module in __one__ file.
Prefix state rules with `is-` or `has-`. They are "shared" beween CSS and JavaScript: but do not use them for selecting an element in your scripts. That's what the `js-` classnames are for.

Acceptable pairs are:
```CSS
.has-error
.is-valid

.is-active
.is-inactive

.is-enabled
.is-disabled

.is-visible
.is-hidden

.is-selected
.is-unselected
```

#### IDs and classes
Rule of thumb: don't use IDs for styling your document. If there's a reason, talk to your team. Namespace IDs with the project prefix to avoid collisions, e.g.: `rf--header`.

#### Naming-Conventions
Avoid presentational or cryptic names, always use IDs and class names that reflect the purpose of the element. Do not use presentational names, e.g.: use `.has-error`instead of `.red`.

Stick to full English words for your semantic class names. Don't use wicked acronyms. Use only hyphens to separate words:
two for a block and one otherwise: `.folder—file` / `.folder-file--purpose`: `.layout-grid` and `layout-grid--size-5`

Every class name should reflect it's purpose and it's position. By sticking to the `folder-file--purpose`-schema you're letting your fellow developers know __what__ the class is for and __where__ to find it.

Every “structural” class needs to follow this convention.


```CSS
/* navigation types */
/* primary: aka "main" */
.navigation-primary {}

/** each type can have different navigations depths  */
.level-first {}
.level-second {}
.level-third {}
.level-fourth {}

/* secondary: aka "sub" */
.navigation-secondary {}
/* tertiary: aka "sub-sub" */
.navigation-tertiary {}
/* quaternary: aka "sub-sub-sub" */
.navigation-quaternary {}
/* meta navigation, usually privacy-policy , terms of service etc */
.navigation-meta {}
/* the so called "social icons" */
.navigation-social {}

```

Remember: Consistency is key, look at the `template.css`

###### Classnames as JS-Hooks
If you need to find an element by it's `classname`. Never use a class which is used for styling. Insert a class just for this purpose and prefix it with `js-`.

Remember: Never reference `.js-` prefixed class names inside your css files.


#### Performance

Use [CSS-Sprites][css-sprites], [Icon-Fonts][icon-fonts] and write [efficient selectors][efficient-selectors].
Don't over qualify your selectors keep them as simple as possible and max three levels deep. Don't tag-qualify, never write `div#foo {…}` or `div.foo {…}`and avoid the universal selector `*`.

##### Example
```CSS
	#foo {…}			/* ID (Fastest) */
	body.foo #bar {…}		/* ID - overqualified: avoid! */
	.foo {…}			/* Class */
	ul li a.foo {…}			/* Class - tag-qualified: avoid*/
	ul {…}				/* Tag */
	ul li a {…}			/* Tag */
	* {…}				/* Universal - avoid! */
	#foo [title=‚bar’] {…}		/* Attribute */
	a:hover{…}			/* Pseudo-atttribute (Slowest) */
```

### Comments
Please don't let your fellow developers guess what you did. Structure your CSS-file into sections and explain what you wan'T to accomplish. Be verbose.

### Whitespace
- Use one selector per line.
- Use one rule per line.
- Put one space after `:` in property declarations.
- Put one space before `{` in rule declarations.
- Put line breaks between rule sets.
- Use a semicolon after every declaration.
- Intend your CSS just one level deep.


### Validation
Use `$ grunt validate:styles` or `$ grunt csslint:project`.
Every file will be linted during the build. We’re using [CSS Lint][csslint] for some simple checks. Please take a look at the [CSS Lint Reference] [csslint-doc]for a complete documentation. You will find the default rule set in your `.csslintrc’-file.

### Best Practice
```css

/**
 * @file layout/grid.css
 *
 * @description
 *
 * Styles for the sitespecific grid
 *
 * @example
 * section.layout-grid--wrapper
 *  section.layout-grid--size-6
 *  section.layout-grid--size-3
 *  section.layout-grid--size-3
 */

	/* basic grid wrapper: defines the width of the grid */
	.layout-grid--wrapper {
		background: #fff;
		margin: 0 10px;
		width: 100%;
	}

	/* 33% wide grid element */
	.layout-grid--size-3 {
		width: 33%;
	}

	/* 66% wide grid element */
	.layout-grid--size-6 {
		width: 66%;
	}


 ```


## SASS

### TL;DR
- Speak to your project lead beforehand!
- Use `/* */` for comment blocks (instead of `//` ).
- Avoid unnecessary nesting. Not more than two levels deep. If you find yourself going further, think about reorganizing your rules. Most likely it is due to the layout of your file - not because of the specificity needed.
- Avoid large numbers of nested rules. Avoid nesting that spreads over more than 20 lines.
- Always place `@extend` statements on the first lines of a declaration block.
- If you introduce a new framework such as `compass`, `bourbon` make sure you __know__ it. Avoid duplicate functionalities.

#### Mixins
Place your custom code in `_mixins.*`. Before writing a new mixing, check if it's not already there. Either in `_mixing.*` or as a part of your frameworks e.g. `compass`, `bourbon` etc. Always document your mixins with at least a short description, the arguments and the return value.
Do not use representation in your variables, use generic names that communicate purpose not layout. Never write `$white = white`, e.g. think about `$color-primary = #fff` instead.


## JavaScript

### TL;DR
- Follow the principles of [unobstrusive javascript][js-unobtrusive]
- Use a [JSDoc][js-doc]-compatible comment-block for every function.
- Use only `js-`-classnames for accessing an element.
- Use one file per `module` / `component` / `class` / `widget`, use `namespaces` to organize your code.
- Use the [“revealing-module-pattern”][js-module-patterns]: for your modules.
- Avoid anonymus-callbacks.
- Never omit curly braces or semicolons.
- Avoid `this` unless you're sure what it refers to.
- Avoid changing the `protoype`-chain.
- Intend using tabs.

### Architecture
Use a decoupled approach (`pub/sub`, `event-driven`, `mediator`) and use one file per module. Every module should be independent.
Take a look at the templates inside the `scripts`-folder.
Stick to the their structure: a well organized project enables the next developer to quickly dive into your code.
Attach all DOM-Events in `_addEvents`. Use event delegation and under no circumstances use anonymous callback-functions for your events.
Your public-API should expose as less functions as possible and break down your code in smaller pieces. Never just write “one large function”.
Never let javascript and CSS share selectors. Use specific classnames if you need to access an element via JavaScript. Prefix these with `.js—` and never reference them in your css files.
Take a look at [clean code][clean-code], [JavaScript Design Patterns][js-essential-patterns] and [Eloquent JavaScript][js-eloquent].

### Comments
Every file need a description. Every function requires a [JSDoc][js-doc]-compatible block comment with a short description, the arguments and the return value.
Use inline comments (with `//`) to state your intentions.
They are preceded by a blank line and they go over the line / block they refer to. Comment everything that is not obvious and break your longer functions into logical sections.
Think about these as annotations to your source code.

### Validation
Every file will be linted. We're using [JSHint][jshint] with an inline configuration and the `.jshintrc` file. Please take a look at [JSHint documentation][jshint-doc]. It is required to specify global `vars' in every file, but don’t worry: there are boilerplates in your `scripts`-folder.
Every file will be checked for compliance with the coding styles. Please consult the `.jscsrc` file and the [JSCS][jscs-doc] for an in-depth explanation of each rule.

### Automated Tests
There are different types of automated tests for every project such as “smoke tests”, “user acceptance tests”, “unit tests”, “specs” depending on your project. You can find them inside the `tests`-folder. You'll most likely be dealing with the specs. We're using [Mocha][mocha] with [Chai][chai] and [Sinon][sinon] or [Jasmine 2.0][jasmine]. If you like BDD or TDD go for it - chai offers interfaces for every style.
If you're working with external APIs it's mandatory to have proper tests but please talk to your tech lead.
If you're working with a module / class / package that already has test coverage, do not break them and under no circumstances just remove them for your own convenience. They are written for a reason.

### Variables
Avoid global variables. Always use `var` to declare them. Use only one `var` declaration per scope. Place it at the top of their scope and declare each on a newline. Remember: only the declarations get [hoisted][js-hoisting] to the top of their scope, not their assignment.

Names should be full English words. Don't use wicked acronyms or one letter `vars` (except for iterators such as `_i`). Be descriptive enough so that everyone understands your intention.  Use a leading underscore when naming `_private` properties/variables/functions and suffix `arguments_`. Remember: the code will be automatically optimized later.

### Whitespace
We use hard tabs everywhere, but smart tabs are okay. Use one space after `if`/`else`/`for`/`while`/`try` and `function`. They always have braces and always go on multiple lines.


### Best Practice
```JavaScript

	/**
	 * foo description
	 * @param  {Object} oHash_ some data
	 * @return {Object}         oHash_ again
	 */
	function foo (oHash_) {

		var
			_i = 0,
			_isFoo = true,
 			_$elements = jQuery(“div”)
		;

		if (condition) {
			// …
		} else {
			// …
		}

		for ( ; _i < 10; _i++ ) {
			// …
		}

		while (_i—) {
			// …
		}

		switch (oHash_.foo) {

 			default:
				// …
			break;

		}

		return oHash_;
	}

```

### jQuery

### TL;DR
- Use `jQuery` instead of `$`.
- Use `jQuery.ajax` over `jQuery.get|post`.
- Use `jQuery.on` not `jQuery.bind|delegate|live`, no anonymous callbacks.
- Prefix jQuery elements or collections with `$`.
- Prefix jQuery object variables with a `$`.
- Cache jQuery lookups.
- Use indentation when chaining methods.
- Use as few third-party-plugins as possible. Check their licenses.

### Plugins
Use as few third-party plugins as possible. Check their licenses. We can not use anything without a proper license. Don't bend this rule, so you can use your favorite plugin. Consider if writing your own functionality is not the faster and better option in the long haul. Truth is: your requirements will change and - under no circumstance - monkey-patch the code. Every third-party element need to be upgradeable.
Finally: It is required to use `bower` with every third-party item.

### Best practice
```JS
_$elements
    .addClass("foo")
    .children()
			.addClass(“ba”r)
    .end()
    .appendTo("body");
```

## Questions
If in doubt contact [martin.krause@razorfish.de](mailto:martin.krause@razorfish.de)

[nodejs]: http://nodejs.org/
[npm]: http://nodejs.org/
[gruntjs]: http://gruntjs.com
[bower]: https://bower.io
[grunt]: https://gruntjs.org
[chai]: http://chaijs.com/
[mocha]: http://visionmedia.github.io/mocha/
[sinon]: http://sinonjs.org/
[jasmine]: http://sinonjs.org/


[progressive_enhancement]: http://en.wikipedia.org/wiki/Progressive_enhancement

[editorconfig]: http://editorconfig.org/
[smacss]: https://smacss.com/

[js-unobtrusive]: http://en.wikipedia.org/wiki/Unobtrusive_JavaScript

[csslint-rules]: https://github.com/CSSLint/csslint/wiki/Rules
[css-sprites]: http://alistapart.com/article/sprites
[icon-fonts]: http://www.sitepoint.com/introduction-icon-fonts-font-awesome-icomoon/

[git]: http://git-scm.com/book
[git-flow]: http://nvie.com/posts/a-successful-git-branching-model
[git-book]: http://git-scm.com/book
[git-workflows]: https://www.atlassian.com/git/tutorials/comparing-workflows


[clean-code]: https://www.ufm.edu/images/0/04/Clean_Code.pdf

[jshint]: http://www.jshint.com/
[jshint-doc]: http://www.jshint.com/docs/
[js-unobtrusive]: http://en.wikipedia.org/wiki/Unobtrusive_JavaScript
[js-hoisting]: http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html


[js-module-patterns]: http://toddmotto.com/mastering-the-module-pattern/
[js-essential-patterns]: http://addyosmani.com/resources/essentialjsdesignpatterns/book/
[js-eloquent]: http://eloquentjavascript.net/

[efficient selectors]: http://csswizardry.com/2011/09/writing-efficient-css-selectors
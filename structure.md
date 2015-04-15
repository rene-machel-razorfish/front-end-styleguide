# Project Structure
```
	/assets
	  ├── /fonts
	  ├── /imgs *
	  │     ├── /x1
	  │     └── /x2
	  │     ├── /1024x786
	  │     └── /2048x1572
	  ├── /pdfs
	  ├── /sprites
	  ├── /sounds
	  ├── /svgs
	  └── /videos
	  │
	[/bower_components]
	  │     ├── /razorfish-germany-front-end-styleguide
	  │     ├── /jQuery
	  │     └── /normalize.css
	  │     └── …
	 /docs
	  │     
	 /grunt
	  │     ├── /templates
	  │     └── /tasks
	 /mock
	  │
	 [/node_modules]
	  │     ├── /bower
	  │     ├── /chai
	  │     ├── /grunt
	  │     └── /mocha
	  │     └── …
	/scripts
	  ├── /_templates
	  ├── /base
	  │     ├── application.js
	  │     ├── config.js
	  │     └── core.js
	  │     └── …
	  ├── /build
	  │     └── scripts.js
	  ├── /modules
	  │     └── …
	/styles
	  ├── /base
	  │     ├── base.css
	  │     ├── fonts.css
	  │     ├── grid.css
	  │     ├── legacy.css
	  │     ├── reset.css
	  │     ├── typography.css
	  │     └── …
	  ├── /modules
	  │     ├── base.css
	  │     ├── footer.css
	  │     ├── header.css
	  │     └── …
	  ├── /build
	  │     └── styles.css
	/tests
	  ├── /mock
	  │     └── …
	  ├── /smoke
	  │     └── …
	  ├── /specs
	  │     ├── namespace.html
	  │     ├── namespace.spec.js
	  │     └── …
	  ├── /uat
	  │     └── …
	  │
	(/vendor)
	  │
	index.html
	favicon.ico
	apple-touch-icon*
	Gruntfile.js
	package.json
	README.md
	robots.txt
```

## /assets
 All domain related assets. The `imgs` folder is for bitmap-images, the `svgs` folder for vector-images. Image-sprites should be placed inside `sprites`. Please use folder names to separate responsive/retina images. Decide if you prefer “factor” (`x1`,`x2`) or “resolution” (`1024x786`,`2048x1572`) based names. Do not use a device name such as “ipad”, “iphone” or “desktop”.

## /bower_components
Everything that is managed by bower. This should be every third-party library.
f you add some, keep in mind to check their license - we can not use anything without a proper license.
If in doubt, look at [OSS Licenses](http://choosealicense.com/licenses/)

## /docs
Looking for documentation? Here you should find it.

## /grunt
All grunt-tasks. One file per task.

## /mock
Mock-data, usually as `JSON`

## /scripts
All (java)script files. Organised in `base` and `modules`. Please use a “one file for one feature” approach and take a look at the templates in `_template`. There's also a `build` folder if you're building minimised files locally.

## /styles
 All *css files. If you like myth, sass or less this is the place to store them. Again, organised in `base` and `modules`. Please use a “one file for one feature” approach. There's also a `build` folder if you're building minimised files locally.

## /tests
We like automated testing. We prefer BDD using Mocha with Chai and Sinon or Jasmine. Use DalekJS/NightwatchJs/NightmareJs for acceptance testing. Please integrate them in your build process.

## /vendor
All the third-party-elements which are not managed by bower. Same rules as all other third-party-components.
If your script requires a css file (or if you want to add just a css file) place them both inside the `vendor` subfolder. Makes it easier to update, replace or remove it. Really.

# Contribution
Feel free to add or change anything.
But please: talk to Marin Krause or your technical lead so they can update the documentation and explain your ideas and modifications to the next developer.


- [Martin Krause](mailto:martin.krause@razorfish.de)

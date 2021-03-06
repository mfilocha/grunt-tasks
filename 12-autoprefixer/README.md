## [Blog post](http://grunt-tasks.com/autoprefixer/ "autoprefixer")

Grunt AutoPrefixer is a grunt plugin that parses all your css files in your web app and adds vendor specifix prefixes like -webkit- or -moz depending upon [Can I Use](http://caniuse.com/).
Its extremely easy to setup and requires little configuration and is recommended by Google and is actively used by Twitter.

## Some of the examples that this plugin can add :-

The following css property applied on an anchor element
```css
:fullscreen a {
	display: flex;
	transition: 1s all;
}
```

will be automatically converted to

```css
:-webkit-full-screen a {
	display: -webkit-box;
	display: -webkit-flex;
	display: flex;
	-webkit-transition: 1s all;
	        transition: 1s all;
}
:-moz-full-screen a {
	display: flex;
	transition: 1s all;
}
:-ms-fullscreen a {
	display: -ms-flexbox;
	display: flex;
	transition: 1s all;
}
:fullscreen a {
	display: -webkit-box;
	display: -webkit-flex;
	display: -ms-flexbox;
	display: flex;
	-webkit-transition: 1s all;
	        transition: 1s all;
}
```

It requires autoprefixer-core to be explicitly declared.
To start using this in your build configuration first install it
`npm install grunt-postcss autoprefixer-core --save-dev`

Here's the grunt file that we have used:
```js
module.exports = function(grunt) {

  var autoprefixer = require('autoprefixer-core');
  require('load-grunt-tasks')(grunt);

  grunt.initConfig({
      postcss: {
        options: {
          processors: [
            autoprefixer({
              browers: ['> 0.5%', 'last 2 versions', 'Firefox ESR', 'Opera 12.1']
            }).postcss
          ]
        },
        dist: {
				files: {
					'dist/': 'css/*.css'
				}
        }
      }
  });

  grunt.registerTask('default', ['postcss']);
};
```

After running grunt on the sample.css inside folder, its replaced by the vendor prefixed version.

Another great grunt plugin that does the same thing is [grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer).
Its easier to install
`npm install grunt-autoprefixer autoprefixer-core --save-dev`

According to this configuration:
```js
autoprefixer: {
	options: {
		browsers: ['last 2 versions', 'ie 8', 'ie 9', '> 1%']
	},
	main: {
		expand: true,
		flatten: true,
		src: 'css/*.css',
		dest: 'dist/'
	}
}
```
On running Grunt this time, it will scan css/sample.css and vendor prefixes to dist/sample.css.
This is a much better option to keep your source files as clean as possible without browser prefixes or some weird browser behaviours.
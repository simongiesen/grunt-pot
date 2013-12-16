# grunt-pot

> Scan files and creates a .pot file using xgettext.

## Getting Started
This plugin requires Grunt `~0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-pot --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-pot');
```

## The "pot" task

### Overview
In your project's Gruntfile, add a section named `pot` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  pot: {
    options: {
      // Specify options
    },
    files: {
      // Specify files to scan
    },
  },
})
```

### Options

#### text_domain
Type: `String`
Default value: (Your package name)

This is the text domain of your project. Currently it is only used to generate the destination file name: `[text-domain].pot`.

#### dest
Type: `String`
Default value: False

Either a path to a folder (with trailing slash) for the generated `.pot` to be placed or a file path. When using a folder, the filename is generated using the text domain.

#### overwrite
Type: `Bool`
Default value: True

When true, append to pre-existing `.pot` file, rather than overwriting it.

#### keywords
Type: `Array`
Default value: (none)

An array of strings ('keywords'). Each keyword specifies a gettext function to scan for:

```
keywords: ['gettext', '__'], //functions to look for
```

By default `xgettext` looks for strings in the *first argument* of each keyword. However you can specify a different argument with `id:argnum`. `xgettext` then uses the `argnum`-th argument.  If keyword is of the form `id:argnum1,argnum2`, `xgettext` looks for strings in the `argnum1`-th and in the `argnum2`-th argument of the call, and treats them as singular/plural variants for a message with plural handling.

```
keywords: [ 'gettext', '__', 'dgettext:2', 'ngettext:1,2' ]
```

If keyword is of the form `id:contextargnumc,argnum` or `id:argnum,contextargnumc`, `xgettext` treats strings in the `contextargnum`-th argument as a context specifier. 

```
keywords: [ 'gettext', '__', 'pgettext:1c,2']
```

#### package_name
Type: `String`
Default value: (name specified in your `package.json`)

This is the name that appears in the header msgid.

#### package_version
Type: `String`
Default value: (version specified in your `package.json`)

This is the version that appears in the header msgid

#### msgid_bugs_address
Type: `String`
Default value: (none)

The email (to report bugs to) that appears in the header msgid 

#### omit_header
Type: `Bool`
Default value: `false`

Whether to omit the header. It is recommended to keep this `false`.

#### comment_tag
Type: `String`
Default value: `/`

Comments immediately above a listed keyword which begin with this tag will be included as a comment in the generate `.pot` file. This is useful for providing hints or guidance for translators. For example, in your parsed file(s) you might have:

```
/// TRANSLATORS: This should be translated as a shorthand for YEAR-MONTH-DAY using 4, 2 and 2 digits.
echo gettext("yyyy-mm-dd");
```

### Usage Examples

```js
grunt.initConfig({
  pot: {
      options:{
	  text_domain: 'my-text-domain', //Your text domain. Produces my-text-domain.pot
	  dest: 'languages/', //directory to place the pot file
	  keywords: ['gettext', '__'], //functions to look for
	},
	files:{
	  src:  [ '**/*.php' ], //Parse all php files
	  expand: true,
       }
  },
})
```

```js
grunt.initConfig({
  pot: {
      options:{
	  text_domain: 'my-text-domain', //Your text domain. Produces my-text-domain.pot
	  dest: 'languages/', //directory to place the pot file
	  keywords: [ 'gettext', 'ngettext:1,2' ], //functions to look for
	},
	files:{
	  src:  [ '**/*.php' ], //Parse all php files
	  expand: true,
       }
  },
})
```


## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_

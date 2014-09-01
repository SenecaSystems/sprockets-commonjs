This library adds CommonJS support to [Sprockets](https://github.com/sstephenson/sprockets).

## This is a fork, since the original was not published for ages.

Also this includes the changes from wazeHQ/sprockets-commonjs to allow you transparent requires without the `.module`-part in filename.

    # in Gemfile
    gem 'sprockets-commonjs-mindreframer', '~> 0.1', require: 'sprockets-commonjs'

    # install
    $ bundle install


## What is CommonJS?

The CommonJS module format is a way of encapsulating JavaScript libraries, ensuring they have to explicitly require and export properties they use. In a nutshell:

1. You require in files using `require()`:

    var Asset = require('models/asset');

2. You export properties using `module.exports`:

    var Asset = function(){ /* ... */ };
    module.exports = Asset;

## This library

This library adds CommonJS support to Sprockets, so it can wrap up JavaScript files as modules, and serve them appropriately.

This is done transparently by checking for `require('...')` or `module.exports = ...`-statements in the source-code.


Sprockets will then wrap up the JS library when it's requested, with the following:

    require.define({'library/name': function(exports, require, module){ /* Your library */ }});

`require.define()` is defined inside `commonjs.js`, which will be included, if any CommonJS modules were found.


One caveat to the approach this library takes, is that dependencies loaded through `require()` will not be added to the dependency graph. This library will not parse the AST tree for require calls. This decision has been made for a variety of reasons, but it does mean you need to require files through both CommonJS and Sprockets.

## Usage

1. Add `gem 'sprockets-commonjs-mindreframer', '~> 0.1', require: 'sprockets-commonjs'` to your `Gemfile`
2. Configure Sprockets::CommonJS.module_paths, e.g.:
    `Sprockets::CommonJS.module_paths += [Rails.root.to_s]`

3. Require all the modules, e.g.: `//= require_tree ./models`
4. Or, require individual modules, e.g.: `//= require users`

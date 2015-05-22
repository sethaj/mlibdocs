# MLibrary Ruby Development

### Environment Overview

* We use [bundler](http://bundler.io/) to manage gems.
* We manage ruby verisons with [rbenv](http://rbenv.org).
* We serve ruby applications from [application servers](application_servers.md) behind an [apache](http://httpd.apache.org) reverse proxy.

### Get Started
[Making a new app.](tutorials/basic_ruby_app.md)

### Local reference works

* [Our local gemserver](http://gems.www.lib.umich.edu/) needs to be sourced at the top of your Gemfile (see the [sample gemfile](samples/sample_gemfile.md)). (Info on the [gemserver](gemserver.md)).
* [Recommended gems](recommended_gems.md) for various tasks. If you're not sure what to use, pick from this list.
* Recommended [style considerations](style.md).

### Sample files

* A [sample gemfile](samples/sample_gemfile.md) which specifies dependencies for a basic sinatra application that uses a mix of local gems and gems from rubygems.org.

### Using rbenv

* [Information about our rbenv installation](rbenv.md)

### Managing this site

* [Orphaned pages](orphaned-pages.md)
* [Missing pages](missing-pages.md)

# MLibrary Ruby Development

### Environment Overview

* We use [bundler](http://bundler.io/) to manage gems.
* We use the [jruby](http://jruby.org/) ruby implimentation hosted on the [TorqueBox](http://torquebox.org) application server behind an [apache](http://httpd.apache.org) reverse proxy.
* We keep [mri](https://www.ruby-lang.org/en/) on the dev servers as well for development/debugging purposes.
* We manage ruby verisons with [rbenv](http://rbenv.org).

### Get Started
[Making a new app.](tutorials/basic_torquebox_app.md)

## Local reference works

* [Our local gemserver](http://gems.www.lib.umich.edu/) needs to be sourced at the top of your Gemfile (see the [sample gemfile](samples/sample_gemfile.md)). (Info on the [gemserver](gemserver.md)).
* [List of production machines](list_of_production_machines.md), so you know where you need to put your code (one copy on each filesystem) and where you need to deploy to torquebox (every production machine).
* [Recommended gems](recommended_gems.md) for various tasks. If you're not sure what to use, pick from this list.
* [Deploying multiple applications to the same context](multi_deploy.md) -- ways you can use a single context to deploy multiple related applications.

## Sample files

* A [sample gemfile](samples/sample_gemfile.md) which specifies dependencies for a basic sinatra application that uses a mix of local gems and gems from rubygems.org.

## Using rbenv

* [Information about our rbenv installation](rbenv.md)

## Managing this site

* [Orphaned pages](orphaned-pages.md)

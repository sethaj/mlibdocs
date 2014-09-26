# MLibrary Ruby Development

### Environment Overview

We use [rbenv](https://github.com/sstephenson/rbenv) to manage different ruby version.
We use [bundler](http://bundler.io/) to manage gems.
We use the [jruby](http://jruby.org/) ruby implimentation hosted on the [TorqueBox](http://torquebox.org) application server behind an [apache](http://httpd.apache.org) reverse proxy.
We keep [mri](https://www.ruby-lang.org/en/) on the dev servers as well for development/debugging purposes.
We manage ruby verisons with [rbenv](http://rbenv.org).

### Get Started
[Making a new app.](basic_torquebox_app.md)

## Local reference works

* [Our local gemserver](http://gems.www.lib.umich.edu/) needs to be sourced at the top of your Gemfile (see the [sample gemfile](samples/sample_gemfile.md)). (Info on the [gemserver](gemserver.md)).
* [List of production machines](list_of_production_machines.md), so you know where you need to put your code (one copy on each filesystem) and where you need to deploy to torquebox (every production machine).
* [Recommended gems](recommended_gems.md) for various tasks. If you're not sure what to use, pick from this list.
* [Local gems](local_gems.md) that expose or use parts of our specific environment.
* [Deploying multiple applications to the same context](multi_deploy.md) -- ways you can use a single context to deploy multiple related applications.

## Sample files

* A [sample gemfile](samples/sample_gemfile.md)

## Picking a local ruby environment (using rbenv)

*Current production ruby is JRuby-1.7x*

* List available ruby versions (JRuby and MRI) with `rbenv versions`
* Choose a ruby version to use with `rbenv shell <full_version_string>` (e.g, `rbenv shell jruby-1.7.15`)

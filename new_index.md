# Using Ruby and Rails at the University Library

## Local reference works

* [Our local gemserver](http://gems.www.lib.umich.edu/) needs to be sourced at the top of your Gemfile (see the [sample gemfile](samples/sample_gemfile.md))
* [List of production machines](list_of_production_machines.md), so you know where you need to put your code (one copy on each filesystem) and where you need to deploy to torquebox (every production machine).
* [Recommended gems](recommended_gems.md) for various tasks. If you're not sure what to use, pick from this list.
* [Local gems](local_gems.md) that expose or use parts of our specific environment.
* [Deploying multiple applications to the same context](multi_deploy.md) -- ways you can use a single context to deploy multiple related applications.

## Sample files

* A [sample gemfile](samples/sample_gemfile.md)

## Picking a local ruby environment

*Current production ruby is JRuby-1.7x*

* List available ruby versions (JRuby and MRI) with `rbenv versions`
* Choose a ruby version to use with `rbenv local <full_version_string>` (e.g, `rbenv local jruby-1.7.15`)

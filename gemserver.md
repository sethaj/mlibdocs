We have a Geminabox-based gemserver at http://gems.www.lib.umich.edu.

## Access control to the gemserver

Access control is layered for access to the gem server.

* Layer 1: Apache front-end acl (i.e. libauth).
  * Unauthenticated access is granted to the .43 subnet, development and production servers.
  * Cosign authenticated access is granted to library staff.
* Layer 2: In application access control to specific paths and specific http request methods.
  * Anyone can do a GET request
  * POST/PUT requests require:
    * Development server IP
    * Production server IP
    * Membership in the mlibrary-ruby-on-rails group in mcommunity

The reasoning for this access control:  Anyone on a server can do the work they need to do, and may share gems.  Anyone developing on their local machine can also get read access to gems.  If all else fails, you can upload gems from your browser.  People who don't know what they're doing can't accidentally trash our gems.

## Using the gemserver from a Gemfile

~~~ ruby
source 'http://gems.www.lib.umich.edu'
~~~

## Pushing to the gemserver from a rake task:

Rakefile:

~~~ ruby
require "bundler/gem_tasks"
require 'lit/tasks/gem'
~~~

Using the rake task:

~~~ bash
$ bundle exec rake -T
rake build        # Build <gemname>-<version>.gem into the pkg directory
rake install      # Build and install <gemname>-<version>.gem into system gems
rake lit:release  # Release to the lit gemserver
rake release      # Create tag v<version> and build and push <gemname>-<version>.gem to...
$ LIT_GEMSERVER=http://gems.www.lib.umich.edu bundle exec rake lit:release
<gemname> <version> built to pkg/<gemname>-<version>.gem.
... some status message ...
~~~

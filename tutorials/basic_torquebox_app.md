# Running a basic ruby web application under torquebox

Running a ruby application in the MLibrary/HT environment requires a little more front-end work than for a basic PHP or Perl-CGI system, due to their being more dependencies involved.

## Step 0. Get an application running

We'll just use a very simple Sintra application that does nothing but say "hello world".

You can do this on your local machine if you have a ruby installed.

Our entire application will consist of three files:
* a `Gemfile` which lists all the application's depedencies
* `simpleapp.rb`, the main sinatra file
* and a `config.ru` file, which holds configuration information that dictates how the application is started and served.

~~~ ruby
# Gemfile
source 'https://rubygems.org' # universal rubygem repo
source 'http://gems.www.lib.umich.edu' # our local rubgems repo

gem 'sinatra'
~~~

We only need one depndancy for something this simple: the `sinatra` gem.

Now, we set it up to do something.

~~~ ruby
# simpleapp.rb

require 'sinatra/base'
class SimpleApp < Sinatra::Base
  enable :logging
  get '/' do
    "Hello world!"
  end
end
~~~

And finally, the `config.ru`

~~~ ruby
# config.ru
require_relative 'simpleapp.rb'

map '/' do      # Map simpleapp at the root
  run SimpleApp
end
~~~

If you put these three files in a directory and run `bundle install --path .bundle` followed by `rackup`, you'll get a local web server that will serve up the text 'Hello World' when you hit the root URL.

## Step 1. Get a *context* from LIT Core Services

Most developers already have a "test" context like `/tb/www-dev/dueberb.mirlyn.lib/testapp`.

Our setup involves the normal Apache server forwarding certain requests to the local Torquebox instance. For this to work, Core Services needs to set up a *context* -- a unique id (that so happens to look like a directory path) that is used to identify URLs that need redirecting to Torquebox.

A *context* might look like:

    /tb/www-dev/dueberb.mirlyn.lib/testapp

Again, note that while it *looks* like a directory, it's not. By local convention, though, you can determine that any requests to `http://dueberb.mirlyn.lib.umich.edu/testapp/` will be forwarded to Torquebox for further processing.

## Step 2. Get your code on a test server (malt or punch)

This is exactly as straightforward as you'd might expect.

* Put your code in a subdirectory you control on your test server (let's say `malt`)
* In that directory, run `bundle install --path .bundle`

The latter command will do a local install of any gems you need into `./.bundle`, as defined in your `Gemfile`. On production machines, Core Services will be taking care of gems, but for testing, each application maintains it's own little gem path under `.bundle`.

To make sure it's working, run `rackup`

This will once again start a little web server just for your application on a weird port. You likely won't be able to interact with it, but you'll see it error out if there are problems. Hit `Ctrl-C` to quit.

## Step 3. Create a -knob.yml file in /l/local/torquebox/deployments

Torquebox is controlled by the creation and deletion of files in `/l/local/torquebox/deployments/`. Every application has a file that ends in `-knob.yml` that dictates the configuration of the application.

The [torquebox documentation of the knobfile](http://torquebox.org/builds/LATEST/html-docs/deployment-descriptors.html) isn't a whole lot more illuminating than this sample file.

~~~ yaml
# dueberb-simpleapp-knob.yml
#
# By local convention, name your -knob file with the form
#    <uniqname>-<appname>-knob.yml
#

application:
  # root: the absolute filesystem path to the directory that contains
  # your config.ru file
  root: /www-dev/dueberb.www.lib/simpleapp

environment:
  # Any key-value pairs here will be available in the environment (accessed
  # in ruby via, e.g., ENV['RAILS_ENV'])

  # This is the place to put "secret" information -- database names and
  # passwords, machine names and ports, etc. Use of the -knob.yml file
  # to store sensitive information means it'll be easier to put
  # our code in public git repositories.

  # This is *also* a good place to put machine-specific stuff -- anything
  # that might, for whatever reason, be dependent on the particular host
  # you're running on (e.g, the name of the solr server local to this
  # datacenter)
  RAILS_ENV: development
  RAILS_RELATIVE_URL_ROOT: /
  DB_NAME: mysimpledb
  DB_USER: mysimpledb
  DB_PASS: likeImGoing_toTELLu

web:
  # The all-important contenxt. URLs assocaited with this contenxt will
  # be mapped to the application defined in this -knobfile.
  context: /tb/www-dev/dueberb.mirlyn.lib/testapp/
~~~


## Step 4. Deploy, test, and undeploy

Using this sample app as an example:

* **Deploy**. `touch /l/local/torquebox/deployments/dueberb-simpleapp-knob.yml.dodeploy`
* **Wait** until `dueberb-simpleapp-knob.yml.deployed` appears in the deployments directory.
* **Test** by hitting the URL (in this case, `http://dueberb.mirlyn.lib.umich.edu/testapp/`)
* **Undeploy** with `rm dueberb-simpleapp-knob.yml.deployed`

Any changes you make to your code necessitate an undeploy/deploy cycle.

## Step 5. Get your code onto the production servers

Once you're happy and ready to put into production, get your code into whatever its production directory is going to be *on all the filesystems for your production environments*. That means one machine **at each datacenter**. www.lib developers can use, e.g., `stout` and `riesling`. HT developers might use `moxie-1` and `rootbeer-1`.

## Step 6. Point Core Services at your `Gemfile` and `Gemfile.lock`

Unlike on the test systems, you don't have the necessary permissions to install gems on the production machines. Tell Core Services where your `Gemfile` and `Gemfile.lock` files are (on the filesystem, or better yet in a public github repo) and someone there will take care of the installation.

## Step 7: Deploy on *all servers*

For (re)deployment, you need to go through the necessary steps (from Step 4, above) on each and every machine in the production pool. That's probably at least four machines. Check out [the list of production machines](../list_of_production_machines.md) to make sure you get them all.

Remember, you need to:

* get your *code* on every *filesystem*
* get your `-knob.yml` file on every *machine* in
* touch/delete variations on your `-knob.yml`-file to deploy/undeploy *on every machine* in `/l/local/torquebox/deployments/`


A simple bash script that ssh's into each machine in turn might look like:

~~~ bash
# Example from 10/10/2014.  There's talk of putting server names in a list somewhere.
for i in stout doppel pilsner riesling chianti asti brut ;
do
  ssh $i "touch /l/local/torquebox/deployments/dueberb-mirlyn-api-knob.yml.dodeploy"
done
~~~

## And...

...in theory, you're all set.

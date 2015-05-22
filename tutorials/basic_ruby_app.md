# Running a basic ruby web application

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

## Step 1. Get a path/port assigned from LIT Core Services

We're in a transitional period right now; we don't have a process around getting an application set up at the moment.

## Step 2. Get your code on a test server (malt or punch)

This is exactly as straightforward as you'd might expect.

* Put your code in a subdirectory you control on your test server (let's say `malt`)
* In that directory, run `bundle install --path .bundle`

The latter command will do a local install of any gems you need into `./.bundle`, as defined in your `Gemfile`. On production machines, Core Services will be taking care of gems, but for testing, each application maintains it's own little gem path under `.bundle`.

To make sure it's working, run `rackup`

This will once again start a little web server just for your application on a weird port. You likely won't be able to interact with it, but you'll see it error out if there are problems. Hit `Ctrl-C` to quit.

## Step 3. Get your code registered with the application server

We're in a transitional period right now; we don't have a process around getting an application set up at the moment.

## Step 4. Deploy, test, and undeploy

We're in a transitional period right now; we don't have a process around getting an application set up at the moment.

## Step 5. Get your code onto the production servers

Once you're happy and ready to put into production, get your code into whatever its production directory is going to be *on all the filesystems for your production environments*. That means one machine **at each datacenter**. www.lib developers can use, e.g., `stout` and `riesling`. HT developers might use `moxie-1` and `rootbeer-1`.

## Step 6. Point Core Services at your `Gemfile` and `Gemfile.lock`

Unlike on the test systems, you don't have the necessary permissions to install gems on the production machines. Tell Core Services where your `Gemfile` and `Gemfile.lock` files are (on the filesystem, or better yet in a public github repo) and someone there will take care of the installation.

## Step 7: Deploy on *all servers*

For (re)deployment, you need to go through the necessary steps (from Step 4, above) on each and every machine in the production pool. That's probably at least four machines.

Remember, you need to:

* get your *code* on every *filesystem*

## And...

...in theory, you're all set.

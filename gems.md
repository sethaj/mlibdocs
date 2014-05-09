We have a communal [gemserver](gemserver.md) available for locally developed gems.

# Locally developed gems

### lit

For the support of common tasks or infrastructure.

* lit - base gem
* lit/rack - a collection of rack support gems
* lit/rack/env - rack middleware layer for modifying the env variable in config.ru.
* lit/rack/remote_user - rack middleware layer for pulling the remote user from the servlet request into the env variable.
* lit/rack/access_control - rack middleware layer for providing access control.
* lit/tasks/gem - Rake task for lit:release to push a .gem file to a local gemserver.

# Old document

We still need to decide how exactly Gems will be managed. Points we are shooting for are:

* Use [Bundler][http://gembundler.com) to manage gem version requirements.
* Don't depend on exact gem versions where possible.
* Install gems in your dev space (how?!) for evaluation purposes.
* Contact [Core Services](mailto:lit-cs-sysadmin@umich.edu) to request system wide installation of new gems ''before'' [deploying](deploying.md) the code that needs the gem.

## Base Gems
List of basic gems that are assumed to be needed indefinitely for all/many/most apps
* rails
* yard*
* simplecov*
* ruby-prof*

## Dev only

Gems not listed here or in a gemfile of a deployed app will be deleted. You have been warned.

Dependencies really start adding up. There are also a few superfluous gems that we might keep around in dev just so <tt>rails new</tt> doesn't complain (e.g. jdbcsqlite3). Here is a list of the gems I have installed so far.

* actionmailer (3.2.8)
* actionpack (3.2.8)
* activemodel (3.2.8)
* activerecord (3.2.8)
* activerecord-jdbc-adapter (1.2.2)
* activerecord-jdbcmysql-adapter (1.2.2)
* activerecord-jdbcsqlite3-adapter (1.2.2)
* activeresource (3.2.8)
* activesupport (3.2.8)
* arel (3.0.2)
* blankslate (2.1.2.4)
* bond (0.4.2 java)
* bouncy-castle-java (1.5.0146.1)
* builder (3.0.3)
* bundler (1.2.1)
* clj (0.0.5.6)
* coderay (1.0.7)
* coffee-rails (3.2.2)
* coffee-script (2.2.0)
* coffee-script-source (1.3.3)
* erubis (2.7.0)
* execjs (1.4.0)
* haml (3.1.7)
* hike (1.2.1)
* i18n (0.6.1)
* jdbc-mysql (5.1.13)
* jdbc-sqlite3 (3.7.2)
* jmx (0.9)
* journey (1.0.4)
* jquery-rails (2.1.3)
* jruby-launcher (1.0.15 java)
* jruby-openssl (0.7.7)
* json (1.7.5 java, 1.5.1 java)
* mail (2.4.4)
* method_source (0.8)
* mime-types (1.19)
* multi_json (1.3.6, 1.0.4)
* nokogiri (1.5.5 java)
* polyglot (0.3.3)
* pry (0.9.10 java)
* rack (1.4.1)
* rack-accept (0.4.5)
* rack-cache (1.2)
* rack-protection (1.2.0)
* rack-ssl (1.3.2)
* rack-test (0.6.2)
* rails (3.2.8)
* railties (3.2.8)
* rake (0.9.2.2)
* rdoc (3.12)
* ripl (0.5.1)
* ripl-multi_line (0.3.0)
* sass (3.2.1, 3.1.21)
* sass-rails (3.2.5)
* sinatra (1.3.3, 1.2.6)
* slop (3.3.3)
* spoon (0.0.1)
* sprockets (2.1.3)
* therubyrhino (2.0.1)
* therubyrhino_jar (1.7.4)
* thor (0.16.0, 0.14.6)
* tilt (1.3.3)
* tobias-rack-webconsole (0.1.4)
* tobias-sinatra-url-for (0.2.1)
* torquebox (2.1.2)
* torquebox-backstage (1.0.7)
* torquebox-cache (2.1.2 java)
* torquebox-configure (2.1.2 java)
* torquebox-core (2.1.2 java)
* torquebox-messaging (2.1.2 java)
* torquebox-naming (2.1.2 java)
* torquebox-rake-support (2.1.2)
* torquebox-security (2.1.2 java)
* torquebox-server (2.1.2 java)
* torquebox-stomp (2.1.2)
* torquebox-transactions (2.1.2)
* torquebox-web (2.1.2 java)
* torquebox-webconsole (0.1.0)
* treetop (1.4.10)
* tzinfo (0.3.33)
* uglifier (1.3.0)
* yard (0.8.2.1)

## Local Gems

Create a [Gemfile](http://gembundler.com/gemfile.html)

~~~ bash
 export GEM_PATH=~/gems
 bundler install --path=$GEM_PATH
 git add gemfile
 git add gemfile.lock
~~~

## Signed Gems

[http://docs.rubygems.org/read/chapter/21](http://docs.rubygems.org/read/chapter/21)

## Hosting Gems

For gems we may want to host ourselves.
[http://docs.rubygems.org/read/chapter/18](http://docs.rubygems.org/read/chapter/18)

[Chapter 18](http://www.techsoftcomputing.com/rubygems/read/chapter/18.html)

> ... it is also fairly east to serve gems from static files on an existing web server. Here's what you need to do.
>
> Create a directory in the public files area of your web server (we will call that directory `BASEDIR` in the following instructions). \\
> Create the subdirectory `BASEDIR/gems`. \\
> Copy any gems you wish to serve into the `BASEDIR/gems` subdirectory. \\
> Run the `gem generate_index` command in order to generate the `yaml` and `yaml.Z` files needed by the RubyGems client. The command will look something like this: \\
> `gem generate_index -d BASEDIR`
>
> That's it. The URL for the server will be whatever URL references `BASEDIR`. Just rerun the `gem generate_index` command whenever you add (or remove) gems from the server.

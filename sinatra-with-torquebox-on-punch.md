
Create directory
----------------
```cd /htapps/sethajoh.babel
mkdir -p testapp/sinatra_test
cd testapp/sinatra_test```

Create app.rb
-------------
```require 'sinatra/base'

class MyApp < Sinatra::Base
  get '/' do
    'Hello world!'
  end
end```

Create config.ru
----------------
```require './app'
run MyApp```

Create Gemfile
--------------
```source 'https://rubygems.org'
gem 'sinatra'```

Run Bundle install
------------------
`bundle install --path .bundle --binstubs`

Test that sinatra is working
----------------------------
```bin/rackup
`^C```

Go to deployments
-----------------
`cd /l/local/torquebox/deployments`

Create the knob file (sethajoh_test_project-knob.yml)
-----------------------------------------------------
```---
application:
  root: /htapps/sethajoh.babel/testapp/sinatra_test
environment:
  RAILS_ENV: {}
  RAILS_RELATIVE_URL_ROOT: /
web:
  context: /tb/htapps/sethajoh.babel/testapp```

I don't think it matters what the knob file is called, as long as it's in the
format `*-knob.yml`. 

The context needs to match what's in the the apache
config in order to work. All devs on punch should have a /testapp virtual
host they can use for torquebox apps.

Create the dodeploy file
------------------------
`touch sethajoh_test_project-knob.yml.dodeploy`

Verify deployment, you should see a file called `sethajoh_test_project-knob.yml.deploy`
after a few seconds.

Make sure you're pointing to punch, in your local /etc/hosts add
----------------------------------------------------------------
141.213.128.180 sethajoh.babel.hathitrust.org

NOTE: you need to be on the VPN for any of this to work

In your browser go to:
----------------------
http://sethajoh.babel.hathitrust.org/testapp

That's it.

To undeploy
-----------
`rm sethajoh_test_project-knob.yml.deploy`



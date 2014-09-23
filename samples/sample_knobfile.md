
~~~ yaml
# dueberb-sipleapp-knob.yml
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

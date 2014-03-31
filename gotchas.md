I don't have access to the production environment, but these are problems I encountered running a Hello-World style rails app on my Ubuntu desktop.  We can weed these out if they don't happen in our environment.

* Naming knob files:  Knob files must end in -knob.yml Otherwise Torqubox thinks they're .war files and will try to unzip them.
* ruby version in deployed WAR was different from the ruby version in my development area.  I had to create/edit a config file for bundler to get it to set the right ruby version. — Probably an issue with JRuby 1.6.x, this should be fixed by using 1.7, also Torquebox will make the WAR issue moot
* development version ran as me/had deployed version ran as tomcat user.  If you read/write to files (i.e. use a file for a database or something like a default Hello-World rails application would do) then you may have permissions problems.


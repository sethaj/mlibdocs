* Code location
Your app root should be /$PATH_FOR_VHOST/appname (for most vhosts) or /$PATH_FOR_VHOST/jruby/appname (vhosts with legacy directory structure of /cgi,/php,etc at top level). Examples:
HathiTrust: /htapps/babel/appname
lib-www: /www/www.lib/jruby/instruction-request
MBlem: /www/www.mblem/mblem

== Before deploying to produciton
All gems will be managed in produciton by Core Services. If your current Gemfile.lock is not satisfied in production, notify Core Services. Note where your Gemfile and Gemfile.lock can be found (i.e. location of the git repo and the git tag/branch).

== Capistrano
We reccomend deploying with Capistrano. In this case your app root (as specified in your knob file) will and in appname/current.

See also: [hosting environment/Web stack](hosting-environment.md) 


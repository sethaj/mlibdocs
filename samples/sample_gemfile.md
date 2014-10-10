A sample Gemfile. Note that sourcing the local gemserver comes *last*.

~~~ ruby
source 'https://rubygems.org'
source 'http://gems.www.lib.umich.edu'

gem 'sinatra'
gem 'sinatra-contrib'
gem 'sinatra-jsonp'
gem 'json'
gem 'library_stdnums'

# mirlyn_id_api is locally developed and sourced
gem 'mirlyn_id_api', '>= 0.0.7'

~~~

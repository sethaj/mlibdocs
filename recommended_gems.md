### What are the recommended gems to use to implement feature X?

* html templating: [slim](http://slim-lang.com)?
* css frameworking: [sass](http://sass-lang.com)
* authorization: [pundit](https://github.com/elabs/pundit)
* authentication: [sorcery](http://rubygems.org/gems/sorcery)
* single sign on: [singular](http://gems.www.lib.umich.edu/)
* protection: beyond what rails does, or outside of rails
* * csrf/xss type stuff: [rack-protection](https://github.com/sinatra/rack-protection)
* File uploads?: Paperclip? Carrier Wave? Both look flakey.
   Paperclip: fields on a model
   Carrierwave: 
   Can Fedora do this for us?
* Existing CSS frameworks:
    * Currently either Foundation or Bootstrap BUT please consult with the accessibility specialist in Library Web Systems about which features can be used safely (example: we do not want anyone using icon fonts for accessibility reasons).
    * Eventually our own internal framework, Falafel, will be the prefered choice.
* Testing: ???
* JS frameworks: JQuery (eventually it will be JQuery + Falafel, our internal front-end framework)
* XML processing: Nokogiri is expected.  OGA may be relevant in the future.
* Debugging: [pry](http://pryrepl.org/) is recommended

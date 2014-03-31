## Markup

Ruby uses 'Embedded Ruby' or [Erb](http://www.stuartellis.eu/articles/erb/) by default. There is nothing wrong with erb. Erb is fine. There are however many html templating options to choose from. One favorite is [haml](http://haml.info/) which has been around for a few years and has quite widespread acceptance.

In your Gemfile, add `gem 'haml'` then run `bundle install`. Instead of writing markup to a file such as `app/views/layouts/application.html.erb` it's `app/views/layouts/application.html.haml`. Rails takes care of the rest.

Haml code tends to be more compact than erb. Like python, haml uses whitespace to delineate blocks.

Here's the [haml vs. erb showdown](http://haml.info). Haml is arguably "cleaner", but that's perhaps a matter of taste.

~~~ haml
#profile
  .left.column
    #date= print_date
    #address= current_user.address
  .right.column
    #email= current_user.email
    #bio= current_user.bio
~~~

~~~ erb
<div id="profile">
  <div class="left column">
    <div id="date"><%= print_date %></div>
    <div id="address"><%= current_user.address %></div>
  </div>
  <div class="right column">
    <div id="email"><%= current_user.email %></div>
    <div id="bio"><%= current_user.bio %></div>
  </div>
</div>
~~~

## CSS preprocessing

Maintaining css can be a drag. Rails 3.2 comes with the [sass css pre-processer](http://sass-lang.com/) to make life a little easier. You'll notice that the `gem 'sass-rails'` is already in a new project's default Gemfile. Sass (like all css preprocessers) lets you create variables, do math and other useful things 'inside' css.  Because rails uses sass by default in it's [asset pipline](http://guides.rubyonrails.org/asset_pipeline.html), there's no need to run `sass-watch` to compile your .scss files into .css for the browser. 

Sass = highly recommended '''unless you are using...'''


## Bootstrap

Twitter's freely available and Apache licensed Bootstrap [http://twitter.github.com/bootstrap/] is a html/css/js framework that can give you sane defaults to help you get your project off the ground quickly and without being too ugly. Add 'twitter-bootstrap-rails' to your Gemfile in the :assets group and <code>bundle install</code> as usual to get started. Then:

~~~ bash
$ rails g bootstrap:install
~~~

* Customize your layout file `apps/views/layouts/application.layout.haml`. See the [Bootstrap grid documentation](http://twitter.github.com/bootstrap/scaffolding.html) for details.
* Add the following to your head to use the response features:
   `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
* Take advantage of [Twitter Components](http://twitter.github.com/bootstrap/components.html) and [JavaScript](http://twitter.github.com/bootstrap/javascript.html) functionality.


'''Problems with Bootstrap''': There may be accessibility issues with using Bootstrap. This may be getting better with newer releases. Also, Bootstrap plays better with the [LESS css preprocesser](http://lesscss.org/) as opposed to using sass ("The Bootstrap API is via less", need to confirm how this works...). If you are using Bootstrap, you should probably be using LESS and not sass.


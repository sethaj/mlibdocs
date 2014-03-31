## Scope

You should be here if you're an experienced software developer who is new to ruby.  The goal of this document is not to be a Ruby tutorial in and of itself, but rather to point at some of the many existing documents on the web which you should find helpful filling in gaps between what you already know, and what you will know once you are experienced working in Ruby.


## Getting Started

### On My Ubuntu 12.04 Desktop

We'll be using [rbenv](https://github.com/sstephenson/rbenv) in development and I presume production, so if you want a similar setup we recommend the same.  Either there's differences between system wide versions of rbenv and local versions, or differences between the 0.2.0 that Ubuntu provides and the 0.3.0 that you can get from github, but I ended up installing the version from github, following hints from [https://gist.github.com/2627011 this gist].

~~~ bash
cd
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
~~~


~~~ bash
mkdir -p ~/.rbenv/plugins
cd ~/.rbenv/plugins
git clone git://github.com/sstephenson/ruby-build.git
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
~~~ 

I also had to repeat some of those for my .bash_profile.  I used to know when each would be included, but the differences elude me now.  I seem to recall that .bashrc is for non-interactive sessions.  I'm sure the manpage for bash has that information, but that's not what this page is about.

~~~ bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bash_profile
~~~

Not necessarily part of ruby, but needed later to get the mysql2 gem.  This package wasn't included in ubuntu by default:

~~~ bash
apt-get install libmysqlclient-dev
~~~


~~~ bash
rbenv install 1.9.3-p194
rbenv global 1.9.3-p194
ruby -v
gem install rails
gem install mysql2 
~~~


## Introductions from other languages

[ruby-lang.org's introduction](http://www.ruby-lang.org/en/documentation/ruby-from-other-languages/) might be a bit light on details if you want to jump into code right after reading, but it covers a broad spectrum of topics.

[The Programming Ruby book](http://www.ruby-doc.org/docs/ProgrammingRuby/html/index.html The Programming Ruby book) is a little old by now.  The scope and the tone seem ideal though.  This version covers version 1.6.  But there is a 2nd (1.8) and 3rd (1.9) edition available for purchase.

[Learn Ruby and Rails](http://www.learnrubyandrails.com/) (Link suggested by Bill)

[Technotopia Ruby Essentials](http://www.techotopia.com/index.php/Ruby_Essentials) Far too many ads for my taste, but it had quick answers to my earliest questions.

## Language Concepts


### Symbols
I was somewhat confused by all those `:identifier` things I saw in the ruby code I picked up.  I don't recall seeing anything like them in the simple perl I used, and I'm pretty sure PHP doesn't do anything like it.  Looks like they're [symbols](http://www.troubleshooters.com/codecorn/ruby/symbols.htm), I found this explanation quite handy.

### Variables

Unlike PHP or PERL, Ruby doesn't have to prefix variables with $ or @ for the parser to recognize them as a variable.  Ruby does have that as an option, though, to indicate scope:

> Although $ and @ are used as the first character in variable names sometimes, rather than indicating type, they indicate scope ($ for globals, @ for object instance, and @@ for class attributes).

[Quote from: "To Ruby from Perl"](http://www.ruby-lang.org/en/documentation/ruby-from-other-languages/to-ruby-from-perl/)

There's a nice overview on variables at [RunPaint.org](http://ruby.runpaint.org/variables RunPaint.org).

### Blocks

Blocks are used a little differently in Ruby than I've encountered in other languages.  They are enclosed with do ... end or { ... } which is pretty standard.  Inside a block things work like you might expect in other languages regarding variable scoping and flow control, but there's an extra feature in that you can implicitly associate a block with a function call.  I say implicitly because the block isn't passed in the argument list, but is on the same line after the argument list.

[http://rubylearning.com/satishtalim/ruby_blocks.html RubyLearning.com's Ruby Blocks page] helped me come to my current understanding of how blocks work in Ruby

==Branching==

You can get standard conditional statements:

<source lang="ruby">
if ...
  x 
elsif ... 
  y
else 
  z
end


unless ... 
  x
else
  y
end
</source>

There's also an inline form:

<source lang="ruby">
if ... then x
elsif ... then y
else z
end
</source>

And postfix conditionals:

<source lang="ruby">
x if ...
x unless ...
</source>

And instead of switch ... case ... default, you get case ... when ... then ... else.

[http://ruby.runpaint.org/flow RunPaint] has more examples in their chapter on flow control.

==Loops==

Before I understood how blocks worked, I thought Ruby had really strange and specialized loop syntax.  You'll see things like:

<source lang="ruby">
1.upto(10) do |i|
 ...
end
</source>

The do ... end is a block being passed to the upto function.  The Integer#upto function then is yielding control to your block with the appropriate value for i set. That way your loop control code stays is readable and stays out of your way really nicely.

You still get the standard looping structues: while, until, and for though:

While:
<source lang="ruby">
while condition
...
end

... while condition
</source>

Until:

<source lang="ruby">
until condition
...
end

... until condition
</source>

For:

<source lang="ruby">
for element in x .. y
 ...
end
</source>

[http://ruby.runpaint.org/flow RunPaint] has a lot more to say.

==Functions==

Some links specific to functions here.

==Objects==

Some links specifics to objects here.


## General Style -- the Github ruby style guide

The [github ruby style guide](https://github.com/styleguide/ruby) should be the 
basis for just about everything, with the exception that we'll be using 
[YARD](http://yardoc.org) over TomDoc. 

Here are a few additions to make things easier to read:

### Files and IO

When possible, pass a block to `File#open` or `File#new` -- the file will 
automatically be closed at the end of the block.

~~~ ruby
  File.open('myfile.txt') do |f|
     f.each_line do |line|
      line.chomp!
      f.puts line.split(/|/).join("\t")
     end
  end
~~~

### Exceptions

#### Don't use exceptions for flow control

~~~ ruby
  # This is bad
  begin
    while true
       item = iter.next
       raise MyException if iter.nil?
     end
   rescue MyException => e
    puts "oops. found one"
   end
  end
~~~

Use exceptions only for something exceptional.  For example, in the above you could 
easily handle the case using standard code, instead of an exception.      

#### Always use the three-argument option for `raise`

Most of the time you'll see `raise MyException` by itself. There are two additional 
(optional) arguments: a value, and a backtrace object.

~~~ ruby
  File.open('myfile').each_line do |line|
    if line =~ /something_horrible/
      raise MyException, "found something horrible", nil
~~~


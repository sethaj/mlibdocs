# Orphaned Pages

These are the pages I've identified as orphaned.  

* [Debuggers](debuggers.md)
* [Deployment](deployment.md)
* [Git Tutorial](git-tutorial.md)
* [Hosting Environment](hosting-environment.md)
* [New Index](new_index.md)
* [Middleware](middleware.md)
* [Rails Tutorial](rails-tutorial.md)
* [Ruby Templating](ruby-templating.md)
* [Ruby Testing](ruby-testing.md)
* [Sinatra](sinatra-with-torquebox-on-punch.md)
* [Style](style.md)

Code I used to find orphaned pages:

```
for i in *.md
do
  echo "> " "$i"
  grep -r "$i" * | egrep -v ^orphaned-pages.md:
  echo
done
```

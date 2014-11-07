# Orphaned Pages

This page is maintained by hand.  Orphaned content was removed or merged on 11/7.

~~~ sh
# Code I used to find orphaned pages:
for i in *.md
do
  echo "> " "$i"
  grep -r "$i" * | egrep -v ^orphaned-pages.md:
  echo
done
~~~

We have a communal [gemserver](gemserver.md) available for locally developed gems.

### lit

A gem For the support of common tasks or infrastructure.

* lit - base gem
* lit/rack - a collection of gems to help running rack applications.
* lit/rack/env - A rack middleware layer for modifying the env variable in config.ru.
* lit/rack/remote_user - A rack middleware layer for pulling the remote user from the servlet request into the env variable.
* lit/rack/access_control - rack middleware layer for providing access control.
* lit/tasks - a collection of gems to provide rake tasks.
* lit/tasks/gem - Rake task for lit:release to push a .gem file to a local gemserver.

TODO:

* lit/tasks/sign - Rake task for signing gems

### singular

For supporting single-sign-on in Rails.

## Signed Gems

[http://docs.rubygems.org/read/chapter/21](http://docs.rubygems.org/read/chapter/21)

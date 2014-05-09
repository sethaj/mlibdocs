# Gemserver

We have a Geminabox-based gemserver at http://gems.www.lib.umich.edu.

## Access control to the gemserver

Access control is layered, for access to the gem server.

* Apache front-end acl, so libauth.
  * Unauthenticated access is granted to the .43 subnet, development and production servers.
  * Cosign authenticated access is granted to library staff.
* In application access control to specific paths and specific http request methods
  * Anyone can do a GET request
  * POST/PUT requests require:
    * Development server IP
    * Production server IP
    * Membership in the mlibrary-ruby-on-rails group in mcommunity

The reasoning is:  Anyone on a server can do the work they need to do to share gems.  Anyone developing on a local box can also do what work they need to do.  People who don't know what they're doing can't accidentally trash our gems.

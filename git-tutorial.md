This is less a tutorial than a look at how git is used in the HathiTrust development environment with perl (mainly).

For a tutorial See [man git](http://www.kernel.org/pub/software/scm/git/docs/gittutorial.html)

Always do the following:

~~~ bash
 $ git config --global user.name 'John Doe'
 $ git config --global user.email johndoe@example.com
~~~

If it's not in git, it didn't happen.

If it isn't signed, we don't trust it (perhaps a bit too draconian). Minimally every commit should have a log message that includes the committer's info.

Rdist, not git, is not used for deployment. May not be the right deployment model for Ruby/Rails. Git is used for staging to test hosts that emulate the production environment in terms of module versions and web environment.

## Repository models

### Central repo, writable by all
A collection of central repositories of record (/htapps/repos/app1,...) hosted on local servers. Developers clone, commit to /htapps/developer.babel/app1 and push back to central.

### Managed central repo
Another model might be for each developer to maintain a bare public repo that they push to and send pull requests to the central repo admin.  May be necessary for developers who do not have write access to the central repos because their access to the Full Data is limited by account privileges to just the Sample Data. [*]
 
[*] Issue:

Access to the HathiTrust data repository (page images, etc.) and rights database is flavored and will affect how developer code that accesses the Data is managed:

 Sample: subset of full repo consisting of only public-domain + sandbox rights database.
 Full: full repo + full rights database.

## Two models for shared libraries

Submodules: sub-projects (embedded git repositories. pointers, actually) in the super project, independently updated within the developers local repository, updates to submodule versions selectively published to the upstream.

APIs to shared code: no inline code library sharing.

## Some resources

* [Introduction to Distributed Version Control, Stephanie Collett](http://www.slideshare.net/scollett/intro-to-distributed-version-control-3288584)
* [The Git Comminity Book](http://book.git-scm.com/index.html)
* [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/) (I kind of like this one)
* [RailsConf Git Talk](http://gitcasts.com/posts/railsconf-git-talk#idc-cover)
* [Pro Git, Scott Chacon](http://progit.org/book/)
* [Version Control with Git, John Loeliger](http://proquest.safaribooksonline.com/9780596158187)
* [Git Cheat Sheets](http://github.com/guides/git-cheat-sheet)
* [Git Interfaces, Front-ends and Tools](https://git.wiki.kernel.org/index.php/Interfaces,_frontends,_and_tools)


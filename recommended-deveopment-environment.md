A recommendation for a VM image used locally by developers and using Vagrant.

Advantages:  Using native tools.  Low-latency.  Growl notifications when unit tests break.

## Problems?  
* Backups are currently only setup for development servers.
* * Maybe a crontab to rsync to a development location?
* (Albert) Using Virtualbox's native shared file system support on Linux, I've seen some weird behavior.  Some files created on the host were unreadable on my guest machine.  I know vagrant documentation mentions using nfs on the host for improved performance.  Is that overkill, expected, reasonable, or a big security issue?


## Alternatives/Things we've done with varying levels of success:

* rsync to desktop, rsync back
* git clone to desktop, push back
* sshfs + mount file systems

Will always need test + beta sites that are not on desktops, but do we need development if we do ask for local virtual machines?

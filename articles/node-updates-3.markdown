Title: Node Updates
Author: Kingdon Barrett
Date: Tue Mar 4 2013 18:41:00 GMT-0500 (EST)
Node: v0.8.21

New article for a new Node.JS version.  Welcome to Node v0.8.21.  (Soon.)

## Content

I am in the process of compiling a new Node v0.8.21.  The node server on martyfunkhouser runs in `forever` mode and I expect that means I will always continue using the same node version until it is manually restarted, but maybe forever will surprise me and start using the new version sooner.

Node seems to core dump on a fairly regular basis (this would probably be fixed eventually) but I never see it down, thanks to forever.  I guess next time I find a node.core, I will be able to know if I ever needed to restart `forever` or if forever will eventually pull in the new node on its own, thanks to segfart.

There is no process in place to upgrade npm modules non-interactively.  (The node update is not really automatic either, but it happens for free whenever I do a `portmaster -a`, which is pretty much every day since it is such an easy process, and very worthwhile on FreeBSD.)


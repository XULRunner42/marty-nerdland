Title: Urbit/Docker Tool
Author: Kingdon Barrett
Date: Thu Nov 3 2013 11:33:39 (EST)
Node: v0.10.21

Normal behavior when running vere on an already active pier is to bring down
the ships of the running vere and start again at its last saved checkpoint.

When re-running an (old, stopped) image in docker of an active (running) pier
or ship, you could encounter problems since the serial of the arvo checkpoints
in the old image is (potentially) behind the latest serial of the running pier.

## We Needed This at Barcamp

To counter this behavior, the urbinit script is "locking" in the `~/.dlock`
directory, which only permits a ship to run when its lock file has been cleared
after a successful stop and commit of the ship's last running pier back to a
`$SHIP`-named image.

You can download `urbinit` and its sister scripts from <a href="//downloads.nerdland.info/urbinit/urbinit-0.3.tar.xz">downloads.nerdland.info</a>.

Slides from my talk are also at <a href="//downloads.nerdland.info/Slides-20131101-Barcamp-CoreOS-Urbit.odp">downloads.nerdland.info/Slides-20131101-Barcamp-CoreOS-Urbit.odp</a>.

Another mirror of my newly released files from downloads.nerdland.info:

* <a href="/urbinit-0.3.tar.xz">urbinit-0.3.tar.xz</a>
* <a href="/urbinit-0.3.tar.xz.md5.txt">urbinit-0.3.tar.xz.md5</a>: 24b051adb61bc1119d25f263b219e9d9  urbinit-0.3.tar.xz
* <a href="/urbinit-0.2.tar.xz">urbinit-0.2.tar.xz</a>
* <a href="/urbinit-0.2.tar.xz.md5.txt">urbinit-0.2.tar.xz.md5</a>: aed056d9cc04a22457d8e5389d38e3d4  urbinit-0.2.tar.xz
* <a href="/urbinit-0.1.tar.xz">urbinit-0.1.tar.xz</a>
* <a href="/urbinit-0.1.tar.xz.md5.txt">urbinit-0.1.tar.xz.md5</a>: 1b3c2b51cf7081050a5c9f9c8aaf122a  urbinit-0.1.tar.xz

It is new so there is no LICENSE file.  I hereby bestow at least <a
href="http://opensource.org/licenses/MIT">MIT</a> level of freedom for the
above links on all who read this announcement.

These are just wrapper scripts I use to more easily control urbit using docker.

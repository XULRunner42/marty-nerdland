Title: Node Updates
Author: Kingdon Barrett
Date: Thu Jul 15 2013 22:19:34 (EDT)
Node: v0.10.13

New article for a new Node.JS version.  Today brings Node v0.10.13 to FreeBSD.

## Content

I set up nagios on my raspberry pi!  Version 3.4.1 (shame it wasn't 3.14).  Performance is very impressive and the setup was a snap, only took me about two or three hours with `check_mk` to get everything all set up.

My configuration is a little sloppy; I think there are some things I'm doing by hand in nagios configs that I should let `check_mk` take care of for me.  A lot of the bits therefore are not under pnp4nagios, which I have not learned to configure for myself.

But I set up rrdcached on the advice of `keith_` from irc (freenode/#nagios) and my load average has come down to about 1.7 from 3.8, meanwhile I am counting higher, up to 94 checks on 4 (5) hosts.  The reason for the discrepancy (is it 4 hosts or 5?) is that I have Localhost (`check_mk`) vs localhost (default pre-configured nagios checks), I kept them both.

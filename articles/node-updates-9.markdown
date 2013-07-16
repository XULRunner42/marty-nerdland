Title: Nagios Monitoring with rrdtool
Author: Kingdon Barrett
Date: Thu Jul 15 2013 22:19:34 (EDT)
Node: v0.10.13

Today brings Node v0.10.13 to FreeBSD.  Here's a little bit of what I've been working on at home… Nagios core monitoring of my home network for fun and profit!  All on a Raspberry Pi Model B, running Raspbian 7.1 (Wheezy).

## Nagios

Today I set up nagios on my raspberry pi!  Version 3.4.1 (shame it wasn't 3.14).  Performance is very impressive and the setup was a snap, only took me about two or three hours with `check_mk` to get everything set up.

My configuration is a little sloppy; I'm using `check_mk` to do most of my configuration, which simplifies a lot.  I haven't set monitoring of [MySQL with Nagios][] using `check_mk`; I only set up the MySQL checks following the [Nagios HostGroups][] documentation from Ubuntu.  No alerts are configured for any services, these are not business-critical processes.

## Performance Graphs with `check_mk`

Doing things by hand in nagios configs should be discouraged, I would rather let `check_mk` take care of as much as possible.  I have not learned to configure `pnp4nagios`, therefore all of those bits I've set up by hand do not include graphs over time or collection of data using `rrdtool`.  More good reasons.

But I set up rrdcached on the advice of `keith_` from irc (freenode/#nagios) and my sustained load average has come down to about 1.7 from 3.8.  Meanwhile I am counting higher, up to 94 checks on 4(/5) hosts.  (4 hosts or 5?) I have `Localhost` (`check_mk`) vs `localhost` (default pre-configured nagios checks).

The checks that are common are slightly different so I kept them both.

[MySQL with Nagios]: http://mathias-kettner.de/checkmk_mysql.html
[Nagios HostGroups]: https://help.ubuntu.com/10.04/serverguide/nagios.html

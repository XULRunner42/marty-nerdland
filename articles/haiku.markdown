Title: Haiku Stuff
Author: Kingdon Barrett
Date: Tue Jun 18 2013 10:19:00 (EDT)
Node: v0.10.13

Haiku is really great, and I have some links I didn't want to lose!  There are
apparently VirtualBox Guest additions for Haiku.  I haven't been able to get
them to work, but here's the thread:

## Content

There is a [thread from 2011][] supposedly only works with the [gcc4 builds][]
of Haiku, but I wasn't able to get it to build.  There are also [gcc4 hybrid
builds][] that might work, I don't know any of the nuances of Haiku.  The code
for the additions is [here][] on Github, or [here2][].

Also, you can see mentions of the code moving into the VirtualBox tree now,
under the stewardship of Oracle where it was last reported to build OK nearly 9
months ago in the comments on the [scgtrp blog][] that I found by Googling.

<del>PS. we are on Node v0.10.8 now, in FreeBSD land.</del>

PPS. I learned of [lebuzz][] which is a blog covering the latest BUZZ about BeOS and Haiku Multimedia.  Looks interesting.

PPPS. I found [this ticket][] that shows Haiku folks care enough to document bugs
on platforms that care enough to share unit tests with developers.  There are
some Haiku developers investigating KVM, Virtio, QXL, Spice, and Xen support as
well as memory ballooning.

[thread from 2011]: http://www.freelists.org/post/haiku-development/RFC-GSOC-2011-VirtualBox-guest-additions-added-to-official-optional-packages
[gcc4 builds]: http://haiku-files.org/unsupported-builds/x86-gcc4/
[gcc4 hybrid builds]: http://www.haiku-files.org/unsupported-builds/x86-gcc4hybrid/
[here]: https://github.com/scgtrp/vbox-haiku/
[here2]: https://github.com/mmadia/vbox-haiku
[scgtrp blog]: https://www.haiku-os.org/blog/scgtrp/2011-09-05_vbox_guest_additions_slightly_late_final_progress_report
[lebuzz]: http://lebuzzin.wordpress.com/
[this ticket]: https://dev.haiku-os.org/ticket/8052

Title: Latest Android on the TF101
Author: Kingdon Barrett
Date: Mon Jul 29 2013 08:35:04 (EDT)
Node: v0.10.15

Today brings Node v0.10.15 to FreeBSD.

I have been talking with KatKiss' timduru about his new ROM to continue the TeamEOS line.  Sounds like the EOS devs made a mess for him to clean by forking everything and now that their team has gone defunct and their repositories are offline, it's a pain to sort out which repos were legitimate forks and which ones have not really diverged at all from AOSP proper so should still have their refs pointed to android.googlesource.com.

## Android 4.3

We're not sure what's new in Android 4.3 because nobody has been able to boot it.  I'm sure that's not globally true (supposedly it has gone out to all of the Nexus 7 devices already), so if anyone wants to share their experiences and tell us what's new, I would happily entertain a discussion.

Here are the links:

* [My First 4.3 Build][] - UNTESTED
* [KatKiss JB 4.2.2 ROM][]
* [timduru's TF101 Page][]

If anyone has a copy of the latest EOS source (and some decent bandwidth such that you'd be willing and able to let me take a clone), or if you have a favorite build of your own, please speak up since I am just itching to start producing nightly builds again.

I will follow timduru's source if nobody can hook me up with the actual git repos for the last July 4 build of EOS4 for TF101.  I was really hoping to be able to review some changes, and I'm afraid there might be a lot more of them if I'm comparing KatKiss vs. AOSP, as opposed to EOS4 vs. KatKiss.

Unfortunately I was never tracking the source code for EOS4.  As anyone may know (or maybe nobody remembers) the last time I produced nightly builds was approximately Froyo-x86, so [quite some time ago][].  I am looking forward to getting back into it.  Maybe timduru could use a bug tracker.

[My First 4.3 Build]: http://downloads.nerdland.info/full_tf101-ota-eng.kbarrett.zip
[KatKiss JB 4.2.2 ROM]: http://forum.xda-developers.com/showthread.php?t=2362764
[timduru's TF101 page]: http://public.timduru.org/Android/tf101/KatKiss/
[quite some time ago]: https://groups.google.com/forum/#!topic/android-x86/2PahNO90i2E

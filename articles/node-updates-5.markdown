Title: YebMinder Project Status
Author: Kingdon Barrett
Date: Mon Dec  2 2013 22:35:23 GMT-0500 (EST)
Node: v0.10.21

Mohela, Mint, Beeminute, Credit Cards, Student Loan, Email; all of these
consume my attention for a minimum of 10 minutes a day, lacking a team of
robots to keep track and bring me those important regular status reports.

## Enter YebMinder — Automate Bee-reporting

I'll build on the Rails project distributed via Beeminder's GitHub, URLminder,
which is used to track the number of words [on this very page][].

As a starting point, I have the [20-minutes][] graph which is kept up-to-date
by a cron job that runs frequently, and is only careful not to move the data
point more than once in a day, no matter how many redundant hosts are running
the code, or how often.

### Bitcoin Mining

Also there is the [new-bitcoins-2][] graph, that shows both mining income and
any other motion of my wallet balance.  That runs less frequently and updates
as many times as it catches a newer balance than what it's seen most recently,
indicating new activity in a day.  This is in contrast, without any respect to
the current state of the graph or data points that were already reported.

### Mint.com

I'll also try to scrape enough data from Mint.com to learn about my account
balances, since Mint collects all of my account data, but doesn't provide any
API to access it, we have [mint-exporter][] to start from.

If it even still works, mint-exporter was only dumping transaction CSV lists
when I tried it last, and never reported on your actual balance.  Balances
should be (but aren't always exactly) moving parallel with transaction records,
and sometimes (in the case of student loan or credit cards with servicers
supporting online payment) you can predict, determine, schedule, and even
reconcile these account data with the data from other various sources.

### Gmail

Finally, I'll try to reproduce the features of [GmailZero][], with a slightly
different focus… looking at unread messages too.  Considering even mail that
doesn't sit in the inbox, but is actually untagged or has tags other than those
tags in a "blessed" list, since some e-mails obviously should be kept.

### Final Goals

Something like a report of final success would be:

No more Beeminder mail (unless something is going wrong)... data reported at an
appropriate time of day to pre-empt the regular beeminder mails, and a daily
summary mail, or dashboard page that also may suggest how I could adjust each
of my goals to be less (or more) conservative, given the progress I'm making,
to keep me moving in the right direction and also keeping Akrasia satisfied.

[Loanminder Progress]: /loanminder-progress
[Loanminder Progress part 2]: /loanminder-progress-part-two
[URLminder]: https://github.com/beeminder/urlminder
[on this very page]: //www.beeminder.com/yebyenw/goals/node-updates-5
[20-minutes]: https://www.beeminder.com/yebyenw/20-minutes
[new-bitcoins-2]: https://www.beeminder.com/yebyenw/goals/new-bitcoins-2
[mint-exporter]: https://github.com/toddmazierski/mint-exporter
[GmailZero]: https://www.beeminder.com/gmailzero

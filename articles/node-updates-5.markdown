Title: YebMinder Project
Author: Kingdon Barrett
Date: Mon Dec  2 2013 22:35:23 GMT-0500 (EST)
Node: v0.10.21

Mohela, Mint, Beeminute, Credit Cards, Student Loan, Email; all of these
consume my attention for a minimum of 10 minutes a day, lacking a team of
robots to keep track and bring me those important regular status reports.

I'll build on the Rails project distributed via Beeminder's GitHub, URLminder,
which is used to track the number of words [on this very page][].

## Enter YebMinder — Automate Bee-reporting

I am not a Rails guru; I didn't know exactly where to start adding code into
the large Rails base of URLminder.  So to get a head start on requirements
without Rails, I created the [20-minutes][] graph which is kept up-to-date by a
cron job that runs frequently.  It looks at the data from Beeminder API and is
careful not to move the data point more than once in a day, no matter how many
redundant hosts are running the code, or how often.

The code [is here][].  It's not a "distributed system" in any sense; it's not
really tracking anything, except for regular daily motion in a (currently
positive) direction.

### Bitcoin Mining

Then there is the [new-bitcoins-2][] graph, that shows both mining income and
any other motion of my wallet balance.  That runs less frequently and updates
as many times as it catches a newer balance than what it's seen most recently,
indicating new activity in a day.  The updates stop when blockexplorer stops,
and this week blockexplorer stopped updating.  Hopefully it comes back!

The graph is supposed to show that I haven't cashed out my mining output, which
is below the yellow line.

### Mint.com

I'll scrape enough data from Mint.com to learn about my account balances, since
Mint collects all of my account data, but doesn't provide any API to access it,
we have [mint-exporter][] to start from.

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

A final goal is antithetical to the trello/GTD philosophy, which is that you
make ongoing progress by moving cards to the done pile, and you don't quit.
You just do it every day.

The goal is to keep moving in the right direction and keep Akrasia satisfied.
Also to collect [these cards][] and eventually find someone to bill for them.

[Loanminder Progress]: /loanminder-progress
[Loanminder Progress part 2]: /loanminder-progress-part-two
[URLminder]: https://github.com/beeminder/urlminder
[on this very page]: //www.beeminder.com/yebyenw/goals/node-updates-5
[20-minutes]: https://www.beeminder.com/yebyenw/20-minutes
[new-bitcoins-2]: https://www.beeminder.com/yebyenw/goals/new-bitcoins-2
[mint-exporter]: https://github.com/toddmazierski/mint-exporter
[GmailZero]: https://www.beeminder.com/gmailzero
[is here]: /beeminute-20-minutes-code
[these cards]: /yebminder-these-cards

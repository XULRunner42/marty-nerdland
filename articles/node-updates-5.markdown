Title: URLminder Fork
Author: Kingdon Barrett
Date: Mon Dec  2 2013 22:35:23 GMT-0500 (EST)
Node: v0.10.21

Mohela, Mint, Beeminute, Credit Cards, Student Loan, Email; all of these
consume my attention for a minimum of 10 minutes a day, lacking a team of
robots to keep track and bring me those important regular status reports.

I'll build on the Rails project distributed via Beeminder's GitHub, URLminder,
which is used to track the number of words [on this very page][].  My repo is
[YebMinder][].

## YebMinder — Automate Bee-reporting

I am not a Rails guru; I didn't know exactly where to start adding code into
the large Rails base of URLminder.  So to get a head start on requirements
without Rails, I created the [20-minutes][] graph which is kept up-to-date by a
cron job that runs frequently.  It looks at the data from Beeminder API and is
careful not to move the data point more than once in a day, no matter how many
redundant hosts are running the code, or how often.

The code [is here][].  It's not a "distributed system" in any sense; it's not
really tracking anything, except for regular daily motion in a (currently
positive) direction.  It's like the minimum code to scale a Beeminder user.

### Bitcoin Mining

Then there is the [new-bitcoins-2][] graph, that shows both mining income and
any other motion of my wallet balance.  That runs less frequently and updates
as many times as it catches a newer balance than what it's seen most recently,
indicating new activity in a day.  It's easy to track a wallet address balance,
since the transactions and balance are tallied by free web services.

The graph is supposed to show that I haven't cashed out my mining output, which
is below the yellow line.

### Mint.com

I'll scrape enough data from Mint.com to learn about my account balances, since
Mint collects all of my account data, but doesn't provide any API to access it.
The [mint-exporter][] is a great place to start from.  The data it provides is
just a CSV feed where the transactions could change in either date, amount, or
in description but `original_description` should be guaranteed not to change.

The mint-exporter is only dumping transaction CSV lists, and never reports on
your actual balance.  Balances tally on the Mint website; perhaps intuitively
they should be moving in parallel with transaction records (but aren't always
exactly).  I plan to predict, determine, schedule, and even reconcile accounts
with the data from other various sources.  YebMinder will eventually make all
of my scheduled payments for me.

### Gmail

Finally, I'll try to reproduce the features of [GmailZero][], with a slightly
different focus… counting even unread messages.  That is, considering even mail
that doesn't sit in the inbox, but is actually untagged or has tags other than
those tags in a "blessed" list.  Also, there is nothing magical about a number
zero; some e-mails obviously must be kept, and tags are not always the answer.

### Final Goals

"He told me to get a big wall calendar that has a whole year on one page and
hang it on a prominent wall. The next step was to get a big red magic marker."
You just do it every day.

The goal is to keep moving in the right direction and keep Akrasia satisfied.
Also to collect [these cards][] and eventually find someone to bill for them.

[Loanminder Progress]: /loanminder-progress
[Loanminder Progress part 2]: /loanminder-progress-part-two
[URLminder]: https://github.com/beeminder/urlminder
[YebMinder]: http://github.com/yebyen/YebMinder
[on this very page]: //www.beeminder.com/yebyenw/goals/node-updates-5
[20-minutes]: https://www.beeminder.com/yebyenw/20-minutes
[new-bitcoins-2]: https://www.beeminder.com/yebyenw/goals/new-bitcoins-2
[mint-exporter]: https://github.com/toddmazierski/mint-exporter
[GmailZero]: https://www.beeminder.com/gmailzero
[is here]: /beeminute-20-minutes-code
[these cards]: /yebminder-these-cards

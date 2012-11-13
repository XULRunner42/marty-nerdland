Title: Loanminder Progress
Author: Kingdon Barrett
Date: Mon Nov 12 2012 20:03:00 GMT-0500 (EST)
Node: v0.8.14

Loanminder project is meant to integrate all of my financial information with the beeminder platform and produce reminders (or prevent them) in the form of regular beeminder alerts.  My original plan was to create a goal to spend 5 times each month, to help me avoid the fees of minimum balance requirements.  That's not much help without an automated dart thrower plotting data on the chart each time you spend.  Enter mint-exporter.

## mint-exporter

The mint-exporter is going to consume your password, and if memory serves it's meant to be taken from keyboard input on the console.  If not, it's stored in a file, and each execution produces a csv output with records of all your transactions as they are counted by your banks.  You might want to consume this data in several ways, tracking progress on a budget of scheduled transactions for example, or simply counting transactions to track progress along the path toward the goal number of transactions.

### BeeMinder

You can sign up for your own account with [beeminder][] and try their service.  I recommend it.  The goal in our case is to get new data points and chart them approximately daily.  If you have a loan website with payment scheduling, you can count the number of days you wait to reconcile transactions and finally-verify that they were processed successfully, resulting in a reduction of principal on the graph and a corresponding decreased cash balance on one of your accounts.

The software should make it possible to see this done against the web services for each run, with an audit trail, and it should effectively schedule your payments for you.  Data on the way to beeminder or final reconciliation is kept in yaml files, occasionally moved from queue to some final state, and archived once finally reconciled.

Here's an example of a graph and a goal using BeeMinder: [20-minutes][].  It is intentionally left a mystery what kind of data belongs to this graph, for illustrative purposes.  At the time of this writing, the data points' values build up increasing in a linear fashion, to a "mound" where it flattens out, presumably intending to turn itself back down at a much later date.

## Conclusion

The successful conclusion of this experiment has hooks to pull data from two financial web service sources, a process that reconciles each data source into a "final" and archive state, and successfully adds two numbers to suggest a payment schedule.

It should also maintain a persistent state that acts at least as well as slave counter to fight duplicating events, and a counter so that account balances are able to be reflected accurately in summary e-mails that are suggesting a payment.

For a copy of this blog, contact [kingdon][].  Thanks for reading!

[kingdon]: mailto:kingdon@tuesdaystudios.com
[20-minutes]: http://beeminder.com/yebyenw/goals/20-minutes
[beeminder]: http://beeminder.com


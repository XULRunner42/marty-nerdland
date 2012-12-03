Title: Loanminder Progress part 2
Author: Kingdon Barrett
Date: Sun Dec 2 2012 14:50:00 GMT-0500 (EST)
Node: v0.8.14

Last month's [article on Loanminder][] project set out to connect two Financial web services, but my personal affinity to hold the money in my hand made it three, with [BlockExplorer][] integration tracking my [beeminder][] [Christmas bitcoins graph][].  My last sprint was cut short because of my repeated attempts to connect through the identity verification gateway at Mohela.

## Recap

I locked my password, did not wait patiently for the reset e-mail, and hard locked the account when I tried and failed to reconnect too many times in quick succession.  I settled on a sqlite database maintained locally for the task of keeping a persistent tab of current balance, which presents additional challenges when I have multiple target platforms that will be sharing the same pool of accounts.

I implemented capybara-webkit on blockexplorer (wild overkill) because I didn't have any other use for a mechanize gem that would not support javascript-enabled data sources.  It (did I ?)

### Bitcoin Income

Most of the bitcoin sites I care about do not depend on AJAX for data presentation.  The [slush's mining pool][] website, which tracks real-time "Proof of Work" and provides current statistics about pool mining user's accumulated earnings, enough to gauge "when is the next payment coming" without setting the threshold so low that your profits are subsumed by tx fees for being small, and too frequent.

The [BlockExplorer][] website similarly does not present AJAX, taking in a Bitcoin address and replying back with a table that shows the history of receipt and payout on that address.  You can see my [Christmas bitcoins graph][] is kept current in a non-spammy way, because the sqlite database is tracking the latest data point reported, and they are currently so far apart that they do not usually repeat within 7 days.

Without that sqlite database, we would be (temporarily) lost, since the Beeminder API does not provide access to the data that makes up the graphs.  We could be quickly found again by hooking up capybara-webkit to the Beeminder user interface (website) which reports on data points on the "Data" tab.  Again, no AJAX necessary.  In this simple instance, it's not necessary, thanks to the sqlite database.  Even if two clients are running on the same graph, the values can be reported again, this is not an "auto-sum" chart like the other Bitcoin graphs, and submitted data is not necessarily correlated to a delta.

If you're the one who's lost now, try to forget about it, the Bitcoin code is just a distraction.  The software is meant to work on automatically paying your bills for you; at least if you have a student loan account with [Mohela][], and that's what bill you wanted to track paying with Beeminder.

### Expansion of Scope

#### Planned Features:

- Don't spam notifications
- Raise confirmation by e-mail when login fails twice.  Stop trying, and cry out once a week.
- Add two numbers together from the payoff calculator page and determine the loans' balance.
- Make a graph of that (aggregate) showing the current total and historical balance at Mohela.
- Upload the 6 (12) original data points to update the 6 already existing graphs.
- Use two concurrent clients on disjoint systems to explore "second opinion"

The "second opinion" means there is a special treatment when two remote clients are operating on the same data at the same time (or slightly disjoint).  A single client that runs several times in a day hearing no "second opinion" on the report channel does not consider any second opinions.  It has only internal logic and any information from database or primary "web service" sources to decide what to do.

Tablet user might not have access to the report channel (if that meant connecting ssh and receiving e-mail from martyfunkhouser).  Still working alone, it could detect a scheduled transaction on the webservice and "skip" scheduling another similar one, or schedule another one later to "vote" in a way that would make similar behaving drones take note of another worker on the queue, and become more lazy.

All processes are therefore smart enough to not use up the month's quota of work on their own, or with a partner, in a single day or even in the first half of a week, even with crosstalk and no backchannels, but greedy processes might try to guess how much extra, and optimistically schedule shares from a generous budget so the process can run less and less each month, or even take a vacation every few weeks.

##### martyfunkhouser.csh.rit.edu

The e-mail received at martyfunkhouser is supposed to be automated.  I don't check this inbox every day.

It should make sense though, that a program whose goal is to schedule and process payments should have a report channel, and that channel should be able to influence the knowledge of the program like the data presented in the normal way, from the remote web service.  The drone instance that runs on martyfunkhouser will do this.  The default configuration is to send e-mail when reporting data.  We will be reporting on a lot more than just the current balance of Bitcoin in the next Loanminder iteration.

Mohela payments take several days to process anyway, so when the drone schedules the payment, it should check the payment queue on the web service for any other scheduled payments.  I think you could configure the drones (one on my tablet and the other on martyfunkhouser) to interfere constructively with each other, or carefully avoiding crosstalk if they are ever able to detect the other one working.  It's likely that is not possible with multi-day processing and long update lags, but Mohela could surprise us.

Two concurrent drones might each detect a "recommending payout" condition, where each announce or schedule the same payment on the same day, without detecting the redundant work, or detecting it but not cancelling the payment because it's counted and noted as still under quota.  (Or other possibility, respond by cancelling it.  Just remember, to imagine what a bad idea that is... if they're both running at the same time, and if each clone or drone can still only cancel it's own payment when it detects the other one working... what happens if both detect each other and each cancel their own payment, leaving none?  What then, eh?)

Having dodged that, then each wait two or three days to hear that payment was applied twice, and adjust their strategy to compensate.  Suggested approach: next pass, each can make the next scheduled payment twice as distant, with only half the payload to anticipate receiving crosstalk from the other worker, who should detect the crosstalk and adjust his own behavior in the same way.  The two working together only get everything done just one day sooner.

#### Why two drones?

I wanted two unrelated workers without a backchannel to be responsible for paying these bills, because one could fail and those bills still have to be paid.  It's not necessary that both drones apply the same work separately depending on each other, if each can instantly detect the work of the other and fulfill the promises in queue, no strategic rollback/adjustment would be likely to be needed.

The goal is to schedule 7 or 8 payments in 15 days or so, which should not be hard for a program that runs 6 times each day, all month!  Even if it's on two disjoint systems, separated by geography and network.

The tricky part is getting them both to simply leave the other half of the month alone.

Even if the transactions are not detected for 3 or 4 days after they occurred, the fact that there are meant to be 7 or 8 of them means that they were small and unlikely to individually break the allowance of the bank account buffer, if two drones managed to try the same payment schedule at exactly the same time.  Otherwise, or before and after that, their detection can influence the future payments that are yet to be scheduled, and plan to make them more appropriate (smaller) fractions so that large or multiple transactions are less frequently needed; still the budget or quota is exhausted and a vacation is occasionally took.

## Conclusion

The successful conclusion of this experiment has hooks to pull data from two financial web service sources, a process that reconciles each data source into a "final" and archive state, and successfully adds two numbers to suggest a payment schedule.

It should also maintain a persistent state that acts at least as well as slave counter to fight duplicating events, and a counter so that account balances are able to be reflected accurately in summary e-mails that are suggesting a payment.

### Old promises

Last week's article to revisit:

The mint-exporter is going to consume your password, and if memory serves it's meant to be taken from keyboard input on the console.  If not, it's stored in a file, and each execution produces a csv output with records of all your transactions as they are counted by your banks.  You might want to consume this data in several ways, tracking progress on a budget of scheduled transactions for example, or simply counting transactions to track progress along the path toward the goal number of transactions.


You can sign up for your own account with [beeminder][] and try their service.  I recommend it.  The goal in our case is to get new data points and chart them approximately daily.  If you have a loan website with payment scheduling, you can count the number of days you wait to reconcile transactions and finally-verify that they were processed successfully, resulting in a reduction of principal on the graph and a corresponding decreased cash balance on one of your accounts.

The software should make it possible to see this done against the web services for each run, with an audit trail, and it should effectively schedule your payments for you.  Data on the way to beeminder or final reconciliation is kept in yaml files, occasionally moved from queue to some final state, and archived once finally reconciled.

Here's an example of a graph and a goal using BeeMinder: 20-minutes.  It is intentionally left a mystery what kind of data belongs to this graph, for illustrative purposes.  At the time of this writing, the data points' values build up increasing in a linear fashion, to a "mound" where it flattens out, presumably intending to turn itself back down at a much later date.

[article on Loanminder]: http://marty.nerdland.info/loanminder-progress
[BlockExplorer]: http://blockexplorer.com/
[Christmas bitcoins graph]: http://beeminder.com/yebyenw/goals/christmas-bitcoins
[beeminder]: http://beeminder.com
[slush's mining pool]: http://mining.bitcoin.cz
[Mohela]: http://mohela.com

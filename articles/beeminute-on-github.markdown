Title: The Exciting Conclusion of: BeeMinute
Author: Kingdon Barrett
Date: Tue May  20 2014 22:08:06 GMT-0400 (EDT)
Node: v0.10.26

Finally a follow-up article with the missing code from my earlier story,
[BeeMinute][].  If you are inclined toward GitHub pages or if otherwise you
want, just skip to the code in [yebyen/BeeMinute][].

I haven't had much time to write a serious wall of text to go with the code in
the article, but the code seems complete enough to deploy from at the moment.
Read more for the rest of the story of that code.

## The Code

The `beedata.rb` file, the mystery `require` that was left out from the story
of [BeeMinute][] for added dramatic tension so very long ago, without further
ado:

    #!/usr/bin/env ruby
    require 'ap'
    require 'sequel'
    require 'date'
    require './beedata_secret'

    DB = Sequel.connect('sqlite://beegraph.sqlite')

    =begin
    },
        [145] {
             "timestamp" => 1349539200,
                 "value" => 100.0,
               "comment" => "Unfroze today",
                    "id" => "50707be486f224476b00001d",
            "updated_at" => 1349549028,
             "requestid" => nil
        },
        [146] {
             "timestamp" => 1349539200,
                 "value" => 100.0,
               "comment" => "initial datapoint of 100 on the 6th",
                    "id" => "50707b6886f224476b000016",
            "updated_at" => 1349548904,
             "requestid" => nil
    =end

    # beedata(arr): arr has newest beeminder data in no particular order
    # (records are usually newest first, data structured as the two above)
    def beedata(arr)
      #ap arr
      ms = DB[:minutes]

      newest_date = nil
      last_value = nil

      arr.each do |d|
        m = ms.where(:id => d['id']).first
        #puts "timestamp.to_date: #{Time.at(d['timestamp']).to_date}"

        record_date = Time.at(d['updated_at']).to_date

        unless m.nil?
          # Already seen this value, not news to this process.
          #puts "found: #{m[:value]} in database with matching id"
        else
          ms.insert(:timestamp => d['timestamp'], :value => d['value'],
                    :comment => d['comment'], :id => d['id'],
                    :updated_at => d['updated_at'],
                    :requestid => d['requestid'])

          #puts "New entry for: #{record_date}"
          if newest_date.nil? or record_date>newest_date
            newest_date = record_date
            last_value = d['value']
          end
        end

        # When data point is already in local cache, nothing to do but find
        # it, read the date updated_at, and store it if newer than any other.
        unless m.nil?
          mt = m[:updated_at]     # data from local cache
          dt = d['updated_at']    # data from beeminder

          record_date = Time.at(m[:updated_at]).to_date

          # The database has a newer date than previously seen
          if newest_date.nil? or record_date>newest_date
            newest_date = record_date
            last_value = m[:value]
          end

          # We do not expect recorded values to ever be changed
          puts "beeminder data has been modified!"    if dt > mt
          Kernel.exit(1)                              if dt > mt
        end
      end

      now_date = Time.now.to_date
      if newest_date.nil? or now_date > newest_date
        print "time to update beeminder data, "

        unless now_date > Date.parse('2013-09-21')
          new_value = last_value-1
        else
          unless now.date > Date.parse('2014-05-01')
            new_value = last_value-1
          else
            new_value = last_value+1
          end
        end
        puts "sending: #{new_value}"
        cmd = "beemind -t #{AUTH_TOKEN} 20-minutes #{new_value} 'from beeminute auto'"
        puts cmd.gsub(AUTH_TOKEN, "[AUTH TOKEN]")
        `#{cmd}`
      end
    end

At the top, this comment after the `=begin` section... this is a short snippet
from the json data structure that comes out of BeeMinder when the bash-`README`
I grabbed from our last chat about [BeeMinute][] hits the JSON API endpoint
with that Token you got from BeeMinder.

(You have a [BeeMinder][] account, right?)

The effect of the `beedata` method is to increment or decrement the data values
for a particular graph once every day, so long as it's called with some of your
most recent data values from the graph, at least once every that often.

You could call this script 500 times a day or once, but it's only going to
update your graph once a day.  That's to help fulfill the promise of BeeMinder.
If you wanted to use a smarter tracking code that doesn't just move the data in
the desired direction so long as the computer stays up, you'd go ahead and fix
this method, or refactor the architecture into something better that lets you
easily track more than one thing.  You may even want to get error messages from
it when things go wrong (before BeeMinder would e-mail to warn you about some
impending emergency.)

---

Factored out the secret into a separate file, `beedata_secret.rb` (excluded
from GitHub):

    #!/usr/bin/env ruby
    AUTH_TOKEN = 'SECRETCODESATBEEHIVE'

And finally, a Gemfile:

    source 'https://rubygems.org'
    gem 'beeminder'
    gem 'awesome_print', :require => 'ap'
    gem 'sequel'
    gem 'sqlite3'

That's it!  The code is at [yebyen/BeeMinute][] on GitHub.  Thanks all for
following, stay tuned for next time.

[BeeMinute]: /beeminute-20-minutes-code
[yebyen/BeeMinute]: //github.com/yebyen/BeeMinute
[BeeMinder]: //www.beeminder.com

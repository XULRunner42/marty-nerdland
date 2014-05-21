Title: BeeMinute
Author: Kingdon Barrett
Date: Wed Jan  1 2014 20:51:18 GMT-0500 (EST)
Node: v0.10.21

I'm finally going to try and exercise the code highlighting feature of Markdown
in Wheat!  Get ready... here goes:

	#!/usr/bin/env bash
	BE='bundle exec'
	RU='rvm'
	
	RVM_ENVIR=/home/yousir/.rvm/scripts/rvm
	RUBY_VERS=2.0.0
	
	   API="https://www.beeminder.com/api/v1"
	  JSON="goals/20-minutes/datapoints.json"
	  TOKEN="auth_token=Beeminder_API_Secret"
	curl -s "$API/users/yebyenw/$JSON?$TOKEN" > 20-minutes.json
	
	 .  $RVM_ENVIR
	$RU $RUBY_VERS
	  ./20graph.rb

The README file above is an executable (bash script), meant to be run by cron
job.  It runs curl and a ruby script, instead of any ruby HTTP library.  Much
easier than adding Rails.  It serves a small purpose and has few dependencies.
Just reading a JSON file and parsing its data.  My JSON is already up to 64k.

	49    10          * * * cd ~/go-work/beeminute; ./README

## The Code

The `20graph.rb` file, with all comments removed:

	require 'json'
	require 'ap'
	require './beedata'
	
	u = 'yebyenw'
	g = '20-minutes'
	
	url = "https://www.beeminder.com/api/v1/users/#{u}/goals/#{g}/datapoints.json"
	
	data = IO.read('./20-minutes.json')
	result = JSON.parse(data)
	
	beedata([result[0],result[1],result[2]])

The same (original, with comments); still not containing any secrets:

	#!/usr/bin/env ruby
	# 20graph.rb
	# Read the state of GET /users/u/goals/g/datapoints.json
	
	require 'rubygems'
	require 'json'
	#require 'net/http'
	#require 'net/https'
	require 'ap'
	require './beedata'
	#require 'sequel'
	
	def graph
	    u = 'yebyenw'
	    g = '20-minutes'
	
	=begin
	def news_search(query, results=10, start=1)
	    base_url = "http://search.yahooapis.com/NewsSearchService/V1/newsSearch?appid=YahooDemo&output=json"
	    url = "#{base_url}&query=#{URI.encode(query)}&results=#{results}&start=#{start}"
	    resp = Net::HTTP.get_response(URI.parse(url))
	    data = resp.body
	
	    # we convert the returned JSON data to native Ruby
	    # data structure - a hash
	    result = JSON.parse(data)
	
	    # if the hash has 'Error' as a key, we raise an error
	    if result.has_key? 'Error'
	        raise "web service error" 
	    end return result 
	end
	=end
	
	url = "https://www.beeminder.com/api/v1/users/#{u}/goals/#{g}/datapoints.json"
	
	=begin
	p url
	https = Net::HTTP.new(url, Net::HTTP.https_default_port)
	
	https.use_ssl = true
	https.ssl_timeout = 2
	https.verify_mode = OpenSSL::SSL::VERIFY_PEER
	https.ca_file = '/usr/share/curl/curl-ca-bundle.crt'
	https.verify_depth = 2
	#https.enable_post_connection_check = true
	
	#Net::HTTP.use_ssl = true
	#resp = Net::HTTP.get_response(URI.parse(url))
	#data = resp.body
	
	data = ""
	https.start do |http|
	    request = Net::HTTP::Get.new(url)
	    response = https.request(request)
	    data = response.body
	    #resp = https.get_response(URI.parse(url))
	end
	result = JSON.parse(data)
	=end
	
	    data = IO.read('./20-minutes.json')
	    result = JSON.parse(data)
	
	    beedata([result[0],result[1],result[2]])
	
	    # ap result
	end
	
	graph

No secrets here, the API secret is contained in the README of this contraption.
There is some commented code with an idea of what it would look like if the web
service calls were self-contained in the ruby binary, but the code I found did
not work for me, maybe it was outdated.

In a [coming post][], the definition of this function call is revealed:

	beedata([result[0],result[1],result[2]])

It contains another important snippet, where the hard work is done of checking
if data has been seen already and submitting it through the API client only if
it has not.  It also uses sequel to keep the necessary persistent state.

	:<<EOF
	sqlite> .schema
	CREATE TABLE items ( id integer NOT NULL PRIMARY KEY AUTOINCREMENT, 
	    name varchar(255),
	    price double precision);
	CREATE TABLE minutes ( timestamp INT, 
	    value DOUBLE,
	    comment STRING, 
	    id STRING,
	    updated_at INT,
	    requestid);
	EOF


Since the value is monotonically increasing and predictable, it is not a
parameter of the function `beedata`, it is calculated in-house and stored in a
sqlite database.  The table is called `minutes` and it has a sister, unused
table called `items` that we can use later or just for an example.

[coming post]: /beeminute-on-github

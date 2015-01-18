---
layout: post
title: "Testing Javascript in Rails"
date: 2012-09-25
categories: blog
---

This post is inspired by Derek Hammer's [testing coffeescript for rails with jasmine](http://www.derekhammer.com/2012/02/18/testing-coffeescript-for-rails-with-jasmine.html). His solution was great for getting my team started, but we both agreed it wasn't ideal. I'm still not entirely happy with the final solution because you do need to start a rails server. However, I have made that as painless as possible.

## The Setup

First, you will need to be using a version of Rails with the Asset Pipeline. This means Rails 3.1+

Second, we are going to be using PhantomJS to run the tests. Install [PhantomJS](http://phantomjs.org/) with your favourite package manager (homebrew for me).

```bash
brew install phantomjs
```

Now we are ready to begin. I am going to go through this with a new project, but there should be no difficulty in adding this to an existing rails project.

```bash
rails new example_project
```

Next, update the gemfile. I use RSpec, but that is just a personal preference.

```ruby
group :development, :test do
  gem "rspec-rails"
  gem 'jasminerice'
end
```

Install RSpec

```bash
bundle install
rails generate rspec:install
```

Now we need to setup the testing folder. Create a folder under spec called 'javascripts' and then add the following spec helper file to it. Ignore the console reporter part for now.

```coffeescript
#= require application
#= require_tree ./
#= require jasmine.ConsoleReporter
```

Now you should be able to load up your tests in a browser by starting your rails server and navigating to [localhost/jasmine](http://localhost:3000/jasmine)


Let's add a CoffeeScript class with a jasmine spec

```coffeescript
class window.Example
  load: ->
    'Hello'
```

```coffeescript
describe 'Example', =>
  describe 'load', =>
    it 'should return hello', =>
      example = new window.Example()
      expect(example.load()).toBe('hello')
```

If everything worked correctly, [localhost/jasmine](http://localhost:3000/jasmine) should now show your failing spec. Before you fix it, let's continue with getting jasmine working from the command line.

Remember that console reporter? We will we need to add that to report the jasmine test output to the terminal. Let's place it in the vendor folder (vendor/assets/javascripts).

```javascript
(function(jasmine, console) {

  if (!jasmine) { throw "jasmine library isn't loaded!"; }
  if (!console || !console.log) { throw "console isn't present!"; }

  var colorMap = {
    "red" : 31,
    "green" : 32,
    "yellow" : 33,
    "purple" : 34,
    "pink" : 35,
    "turquoise" : 36
  };

  jasmine.ConsoleReporter= function() {
    window.jasmineErrorCount = undefined;
  };

  jasmine.ConsoleReporter.prototype = {

    reportRunnerStarting: function(runner) {
      this.startTime = new Date().getTime();
      this.executedSpecs = 0;
      this.passedSpecs = 0;
    },

    reportSpecStarting: function(spec) {
      this.executedSpecs++;
    },

    reportSpecResults: function(spec) {
      var results = spec.results();
      if (results.passed()) {
        this.passedSpecs++;
        return;
      }

      this.log("\n" + spec.getFullName(), "red");

      var resultItems = results.getItems();
      for (var i = 0; i < resultItems.length; i++) {
        var result = resultItems[i];
        if (result.type == 'log') {
          this.log(result, "yellow");
        } else if (result.type == 'expect' && result.passed && !result.passed()) {
          this.log(result.message, "red");
          if (result.trace.stack) {
            this.log(result.trace.stack, "yellow");
          }
        }
      }
    },

    reportRunnerResults: function(runner) {
      var failureCount = this.executedSpecs - this.passedSpecs;
      var specDetails = this.executedSpecs + (this.executedSpecs === 1 ? " spec, " : " specs, ");
      var failureDetails = failureCount + (failureCount === 1 ? " failure\n" : " failures\n");
      var color = failureCount > 0 ? "red" : "green";
      var duration = new Date().getTime() - this.startTime;

      this.log("\nFinished in " + (duration/1000) + " seconds\n");
      this.log(specDetails + failureDetails, color);

      window.jasmineErrorCount = failureCount;
    },

    colorizeText: function(text, color) {
      var colorCode = colorMap[color];
      return "\033[" + colorCode + "m" + text + "\033[0m";
    },

    log: function(output, color) {
      var text = (color != undefined) ? this.colorizeText(output, color) : output;
      console.log(text);
    }

  };

})(jasmine, console);
```

We are almost finished. Next we need to add a rake task to run the javascript tests. Add the following under lib/tasks

```ruby
require 'rubygems'

namespace :jasmine do
  desc "Runs the jasmine tests"
  task :spec => [:start_server] do
    unless system("which phantomjs > /dev/null 2>&1")
      abort "PhantomJS is not installed. Download from http://phantomjs.org"
    end

    sh "phantomjs lib/tasks/phantomjs_runner.coffee http://localhost:5555/jasmine"
    specs_passed = $?.success?
    Rake::Task['jasmine:stop_server'].execute
    fail('Jasmine Specs Failed') unless specs_passed
  end

  desc "starts the jasmine server"
  task :start_server do
    # empty log file
    File.open('log/jasmine.log', 'w') {|file| file.truncate(0) }

    # start jasmine server
    sh "rails server --port=5555 >log/jasmine.log 2>&1 &"

    20.times do |i|
      log_contents = File.read('log/jasmine.log')
      if log_contents.length == 0
        puts "waiting for server to start..."
      else
        sleep 0.5
        break
      end
      sleep 0.5
    end
  end

  desc "stops the jasmine server"
  task :stop_server do
    `ps aux | grep port=5555 | awk '{print $2}' | tail -n 1 | xargs kill -9`
  end
end

task :spec do
  Rake::Task['jasmine:spec'].invoke
end
```

Finally add the phantomjs runner under lib/tasks as well.

```coffeescript
# Script Begin
if phantom.args.length == 0
  console.log "Need a url as the argument"
  phantom.exit 1

reportWatcher =
  run: (page, max_tries=10) ->
    tries = 0

    callback = =>
      tries = @incrementTries(tries, max_tries)
      @checkForReportCompletion(page)

    setTimeout callback, 100

  incrementTries: (tries, max_tries) ->
    phantom.exit 1 if tries == max_tries
    tries + 1

  getErrorCount: (page) ->
    page.evaluate ->
      window.jasmineErrorCount

  checkForReportCompletion: (page) ->
    errorCount = @getErrorCount(page)
    if errorCount == undefined then return
    if errorCount == 0 then phantom.exit 0 else phantom.exit 1

address = phantom.args[0]
page = new WebPage()

page.onConsoleMessage = (msg) ->
  console.log msg

page.onError = (msg, trace) ->
  console.log msg
  trace.forEach (item) ->
    console.log " #{item.file}:#{item.line}"

page.onInitialized = =>
  page.evaluate =>
    window.onload = =>
      jasmine.getEnv().addReporter(new jasmine.ConsoleReporter())

# open test page and wait for completion
page.open address, (status) ->
  if status != 'success'
    console.log 'Unable to access network'
    phantom.exit 1

  reportWatcher.run(page);
```

That's it. Run the following:

```bash
rake jasmine:spec
```

You should now see the same test failure from before. Fix the case in 'Hello' and you will have your first passing JavaScript test.

## Note

WEBrick may cause you some issues with stopping/starting. I used thin (gem 'thin' in your Gemfile) and the issue went away.

I have a [project](https://github.com/tylermercier/headless_jasmine) on github which this is based off of. Check it out if you want to get something similar setup outside of rails.

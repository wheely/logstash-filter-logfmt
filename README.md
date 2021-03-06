# Logstash Logfmt Parser Plugin
[![Build Status](https://travis-ci.org/wheely/logstash-filter-logfmt.svg?branch=master)](https://travis-ci.org/wheely/logstash-filter-logfmt)


This is a plugin for [Logstash](https://github.com/elasticsearch/logstash), allowing logstash to parse logfmt-formatted messages.

It is fully free and fully open source. The license is Apache 2.0, meaning you are pretty much free to use it however you want in whatever way.

## Documentation

Logstash provides infrastructure to automatically generate documentation for this plugin. We use the asciidoc format to write documentation so any comments in the source code will be first converted into asciidoc and then into html. All plugin documentation are placed under one [central location](http://www.elasticsearch.org/guide/en/logstash/current/).

- For formatting code or config example, you can use the asciidoc `[source,ruby]` directive
- For more asciidoc formatting tips, see the excellent reference here https://github.com/elasticsearch/docs#asciidoc-guide

## Need Help?

Need help? Try #logstash on freenode IRC or the https://discuss.elastic.co/c/logstash discussion forum.

## Developing

### 1. Plugin Developement and Testing

#### Code
- To get started, you'll need JRuby with the Bundler gem installed.

- Create a new plugin or clone and existing from the GitHub [logstash-plugins](https://github.com/logstash-plugins) organization.

- Install dependencies
```sh
bundle install
```

#### Test

```sh
bundle exec rspec
```

The Logstash code required to run the tests/specs is specified in the `Gemfile` by the line similar to:
```ruby
gem "logstash", :github => "elasticsearch/logstash", :branch => "1.5"
```
To test against another version or a local Logstash, edit the `Gemfile` to specify an alternative location, for example:
```ruby
gem "logstash", :github => "elasticsearch/logstash", :ref => "master"
```
```ruby
gem "logstash", :path => "/your/local/logstash"
```

Then update your dependencies and run your tests:

```sh
bundle install
bundle exec rspec
```

### 2. Running your unpublished Plugin in Logstash

#### 2.1 Run in a local Logstash clone

- Edit Logstash `tools/Gemfile` and add the local plugin path, for example:
```ruby
gem "logstash-filter-logfmt", :path => "/your/local/logstash-filter-logfmt"
```
- Update Logstash dependencies
```sh
rake vendor:gems
```
- Run Logstash with your plugin
```sh
bin/logstash -e 'filter {logfmt { source => "message" }}'
```
At this point any modifications to the plugin code will be applied to this local Logstash setup. After modifying the plugin, simply rerun Logstash.

#### 2.2 Run in an installed Logstash

- Build your plugin gem
```sh
gem build logstash-filter-logfmt.gemspec
```
- Install the plugin from the Logstash home
```sh
bin/plugin install /your/local/plugin/logstash-filter-logfmt.gem
```
- Start Logstash and proceed to test the plugin

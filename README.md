# EM-REST-Client


This gem allows to use different HTTP implementation in RestClient with next adapters:

* `:net_http` - Net::HTTP (default, blocking I/O)
* `:em_http` - EventMachine::HttpRequest (non-blocking I/0)


## Installation

Add this line to your application's Gemfile:

```ruby
gem 'em-rest-client'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install em-rest-client

## Usage


You may specify adapter for each request:

```ruby
RestClient.get('https://www.google.com')
RestClient.get('https://www.google.com', adapter: :em_http)
```

Or you may specify adapter globaly:

```ruby
RestClient.adapter = :em_http
RestClient.get('https://www.google.com')
```

## Notes

When EventMachine is already running we assume that you are responsible for Fiber allocation.
You can add `Rack::FiberPool` to your application middleware and it automatically provides a Fiber for each incoming HTTP request. It creates pool of Fibers and re-use fiber for each incoming HTTP request. Also you can control the connection pool size.


## Testing

* `BUNDLE_GEMFILE=gemfiles/1_8_0 bundle exec rspec`
* `BUNDLE_GEMFILE=gemfiles/2_0_0 bundle exec rspec`

## Authors

* [Andriy Yanko](http://ayanko.github.io)

## References

* https://github.com/rest-client/rest-client
* https://github.com/igrigorik/em-http-request
* https://github.com/alebsack/rack-fiber_pool

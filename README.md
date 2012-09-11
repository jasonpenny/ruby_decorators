# Ruby Decorators

#### Ruby method decorators inspired by Python.

## Installation

Add this line to your application's Gemfile:

    gem 'ruby_decorators'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install ruby_decorators

## Usage

```ruby
class Batman < RubyDecorator
  def call(this)
    this.sub('world', 'batman')
  end
end

class Catwoman < RubyDecorator
  def initialize(*args)
    @args = args.any? ? args : ['catwoman']
  end

  def call(this)
    this.sub('world', @args.join(' '))
  end
end

class DummyClass
  extend RubyDecorators

  def initialize
    @greeting = 'hello world'
  end

  def hello_world
    @greeting
  end

  +Batman
  def hello_batman
    @greeting
  end

  +Catwoman
  def hello_catwoman
    @greeting
  end

  +Catwoman.new('super', 'catwoman')
  def hello_super_catwoman
    @greeting
  end
end

dummy = DummyClass.new

dummy.hello_world # => "hello world"
dummy.hello_batman # => "hello batman"
dummy.hello_catwoman # => "hello catwoman"
dummy.hello_super_catwoman # => "hello super catwoman"
```

## License

Copyright (c) 2012 [Fred Wu](http://fredwu.me/)

Licensed under the [MIT license](http://fredwu.mit-license.org/).

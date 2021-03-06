[ ![Codeship Status for SauloSilva/sinatra-active-model-serializers](https://codeship.com/projects/0be149a0-8d56-0132-3f2c-5691319bff63/status?branch=master)](https://codeship.com/projects/60665)

# Sinatra::ActiveModelSerializers

[![Gem Version](https://badge.fury.io/rb/sinatra-active-model-serializers.png)](http://badge.fury.io/rb/sinatra-active-model-serializers)

This gem has the function of adapt the Active Model Serializers to work in Sinatra from a more practical way with models.
If do you use everything at the default, just  require `sinatra_active_model_serializers` for serializers work correctly the a json response.

## Requirements

Ruby 1.9.2 or greater, Sinatra 1.4.5 or greater and Sinatra Contrib 1.4.2 or greater.

## Installation

`gem install sinatra-active-model-serializers`

or with bundler

```
# Gemfile
source :rubygems

gem 'sinatra'
gem 'sinatra-contrib'
gem 'sinatra-active-record'
gem 'sinatra-active-model-serializers'
```

## Configure

First you have to being with the active record configured in your system environment correctly. If the environment is not set up, see their [documentation](https://github.com/janko-m/sinatra-activerecord#sinatra-activerecord-extension).
After is simply do require from our library on your `application.rb`, eg.

```ruby
require 'rubygems'
require 'bundler'
Bundler.require :default

class App < Sinatra::Base
  get '/' do
    json Test.first
  end
end
```

## Sets

#### active_model_serializers

This attribute is an object, all inserted configuration this object it will be passed on to Active Model Serializers, eg.

```
set :active_model_serializers, { root: false }
```

#### serializers_path

By default this attribute is set up to look for the serializers from your project in "* app / serializers *". Whether you have a different environment you can set up by inserting the path of the string, eg.

```
set :serializers_path, './whatever_path/serializers'
```

or not to automatically requires

```
set :serializers_path, false
```

## Response JSON

When you return a json, you can send a the second parameter.
This the second parameter is an object. This object may contain new configurations to assign to the Active Model Serializers or to rewrite any already set by default, eg.

#### root

```
get '/' do
  json Resource.first, { root: false }
end
```

#### scope

```
get '/' do
  json Resource.first, { scope: self }
end
```

#### serializer

If you wish to use an another serializer than the default, you can explicitly pass it through the renderer

1. For a resource:

```ruby
json Resource.first, { serializer: ResourcePreviewSerializer }
```

## License

[MIT](https://github.com/SauloSilva/sinatra-active-model-serializers/blob/master/LICENSE)
---
published: true
title: Rails 5 migration
layout: post
---
I'm migrating my app to R5, it's mostly painless but here's a few caveats. 

## Mongoid

 Mongoid head is compatible with Rails 5 as of 2016-07-02 so use it in your gem file. 

~~~~ruby
gem 'mongoid', git: 'https://github.com/mongodb/mongoid.git'
~~~~

## rails_admin

 Rails Admin is currently unsuported so it's necessary to comment out or remove its inclusions.

~~~~bash
/config/initializers/rails_admin.rb
~~~~
and in your routes.rb file

~~~~ruby
  #mount RailsAdmin::Engine => '/admin', as: 'rails_admin'
~~~~
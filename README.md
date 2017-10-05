# README

This README would normally document whatever steps are necessary to get the
application up and running.

### PART ONE - create the app and install Devise gem for users to create an account and log in.
1.  create a ERB on DB Designer
2.  rails new instaRails
3.  git init
4.  git add .
5.  git commit -m ‘first commit’
6.  add gem 'devise'
6.  git checkout devise
7.  rails g devise:install
8.  add     <p class=“notice”><%= notice %></p>
            <p class=“alert”><%= alert %></p>
    to views/layouts/application.html.erb
 9. rails g devise User
10. rails db:migrate
11. Add before_action :authenticate_user! To controller/application_controller
12. rails g controller Home landing
13. root ‘home#landing’   to config/routes.rb
14. Have a look

### PART TWO - adding Bootstrap 4 gem to the rails appear
1. add following gems to your Gemfile
   gem 'bootstrap', '~> 4.0.0.beta'
   gem 'jquery-rails'
2. bundle install
3. add following to app/assets/stylesheets/application.css:
   /* Custom bootstrap variables must be set or imported *before* bootstrap.
   @import "bootstrap";
4. rename the folder to app/assets/stylesheets/application.scss:
5. add following to your app/assets/javascripts/application.js
   //= require jquery3
   //= require popper
   //= require bootstrap-sprockets
6. check it out


Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

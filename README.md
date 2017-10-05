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
   ```
   gem 'bootstrap', '~> 4.0.0.beta'
   gem 'jquery-rails'
   ```
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

### PART THREE - installing Shrine gem to upload photos
1. add following gem to your Gemfile
   gem "shrine"
2. install dependencies `bundle install`
3. enter following command `rails g scaffold photo title:string image_data:text users:references`
4. add [association](http://guides.rubyonrails.org/association_basics.html) between User and Photo 
4. migrate schema into database `rails db:migrate`
5. create folder initializers if it doesn't exist already and create a new file shrine.rb in config folder
6. paste following code into it
```
  require "shrine"
  require "shrine/storage/file_system"

  Shrine.storages = {
    cache: Shrine::Storage::FileSystem.new("public", prefix: "uploads/cache"), # temporary
    store: Shrine::Storage::FileSystem.new("public", prefix: "uploads/store"), # permanent
    }

  Shrine.plugin :sequel # or :activerecord
  Shrine.plugin :cached_attachment_data # for forms
  Shrine.plugin :rack_file # for non-Rails apps
```
7. create a new file image_uploader.rb in models folder
8. paste following
```
  class ImageUploader < Shrine
  end
```
9. add following code `include ImageUploader[:image]` to models/photos.rb
10.




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

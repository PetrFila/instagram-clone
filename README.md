# README

* Ruby version 2.4.1p111
* Rails version 5.1.4

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
11. Add `before_action :authenticate_user!` To controller/application_controller
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
  ```
   /* Custom bootstrap variables must be set or imported *before* bootstrap.
   @import "bootstrap";
   ```
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
10. in views create a new folder ```/shared/``` and new file ```_errors.html.erb```
11. paste following
```<% if object.errors.any? %>
  <h3>The following errors were found:</h3>

  <ul>
    <% object.errors.full_messages.each do |message| %>
      <li><%= message %></li>
    <% end %>
  </ul>
<% end %>

```
12. the user should be able to upload images by now
13. Set up validation. Go to config/initializers and paste following `Shrine.plugin :validation_helpers`
14. Set up validation logic. Go to models/image_uploader.rb and paste
```Attacher.validate do
    validate_max_size 1.megabyte, message: "is too large (max is 1 MB)"
    validate_mime_type_inclusion ['image/jpg', 'image/jpeg', 'image/png']
end

```
15. OPTIONAL: include `plugin :determine_mime_type` to image_uploader.rb class to determine the MIME type based on the file's contents
16. include `plugin :cached_attachment_data` to the same file to keep phots uploaded in case of receiving an error message when uploading
17. adding edit image feature. Paste following to photos_controller.rb
```
def edit
    @photo = Photo.find(params[:id])
end

def update
    @photo = Photo.find(params[:id])
    if @photo.update_attributes(photo_params)
      flash[:success] = 'Photo edited!'
      redirect_to photos_path
    else
      render 'edit'
    end
end
```
at very bottom before the end tag
```
def photo_params
  params.require(:photo).permit(:title, :image, :user_id, :remove_image)
end
```


Following tutorial was used to create this app. Please note there are some errors and typos so be careful when using it and compare the steps with another sources.
https://code.tutsplus.com/tutorials/uploading-files-with-rails-and-shrine--cms-27596

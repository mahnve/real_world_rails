!SLIDE subsection

# Libraries

!SLIDE bullets

* Vanilla Rails is just that
* The Rails ecosystem is awesome

!SLIDE code

# [Haml](http://haml-lang.com/)

    @@@ Haml
    !!! 5
    %head
      %title NGNews
    %body
      #container.page
        .beta
          = image_tag('beta.png')
        %header.head.line{:role => 'banner'}
          %nav.action-bar
            %ul
              %li

!SLIDE code

#Filters

    :javascript
      var s = $('body').data('foo', '#{I18n.t('search_news')}');
    :markdown
      # A title 

      Some text

!SLIDE bullets

# [InheritedResources](https://github.com/josevalim/inherited_resources)

* CRUD Controllers
* Does most of the work for you

!SLIDE code

# A lot of code looks like this:

    @@@ Ruby

    def update
        @foo = Foo.find(params[:id])
        respond_to do |format|
          if @foo.update_attributes(params[:foo])
            format.html { redirect_to(@foo) }
          else
            format.html { render :action => "edit" }
          end
        end
      end
    end

!SLIDE code

# With InheritedResources

    @@@ Ruby
    class FooController < ApplicationController
      inherit_resources
    end

!SLIDE bullets

# Formtastic

* Forms DSL
* Writing forms is boring
* And repetitive

!SLIDE code

# The simplest form

    @@@ Haml
    - semantic_form_for @user do |form|
      = form.inputs
      = form.buttons

!SLIDE code

# Slightly more complex
  
    @@@ Haml
    - semantic_form_for @user do |form|
      = form.inputs do
        = form.input :first_name
        = form.input :last_name
        = form.input :role, :as => checkbox
      = form.buttons do
        = form.commit_button
    
!SLIDE 

# [Devise](https://github.com/plataformatec/devise)

* A Swiss Army Knife For Your Authentication Needs

!SLIDE code

    @@@ Ruby
    class User < ActiveRecord::Base

      devise :database_authenticatable, :recoverable,
            :trackable, :timeoutable,
            :registerable, :confirmable, :lockable,
            :token_authenticatable
    end

!SLIDE bullets

# [CarrierWave](https://github.com/jnicklas/carrierwave)

* Attachments done easy

!SLIDE code

# In your model

    @@@ Ruby
    class Image < ActiveRecord::Base
      
      validates_presence_of :file
      
      mount_uploader :file, ImageUploader

    end

!SLIDE code

# The uploader

    @@@ Ruby


    class ImageUploader < CarrierWave::Uploader::Base
      include CarrierWave::MiniMagick
      storage :file # can be :S3
      process :resize_to_fit => [300,200]

      def store_dir
        "files/#{model.class.to_s.underscore}/#{mounted_as}/#{model.id}"
      end
      
      def extension_white_list
        %w(jpg jpeg gif png)
      end
    end

!SLIDE

# Alternative: [PaperClip](https://github.com/thoughtbot/paperclip)

!SLIDE bullets

# [DelayedJob](https://github.com/collectiveidea/delayed_job) 

* Large email batches
* Web service calls
* FTP calls
* Image processing
* ...

!SLIDE code

# A Job

    @@@ Ruby
    class FooJob 

      def initialize(foo_id)
        @foo_id = foo_id
      end

      def perform
        @service = FooService.new
        @service.send(Foo.find(@foo_id))
      end
    end

!SLIDE code

# Calling a job

    @@@ Ruby
    FooController < ActionController
      def something
        @foo = Foo.find(params[:id])
        Delayed::Job.enqueue FooJob.new(@foo.id) 
      end
    end

!SLIDE 

# Alternative: [Resque](https://github.com/defunkt/resque)

* Redis backed

!SLIDE 

# [Savon](https://github.com/rubiii/savon)

* If you have to use SOAP, Savon is your friend

!SLIDE code

    @@@ Ruby

    @client = Savon::Client.new do |wsdl|
      wsdl.document = SOME_URL
    end

    base_body ={ "something" => foo.id,
                 "something_else" => foo.name}
      
    @response = @client.request :wsdl, :foo_service do |soap|
      soap.namespaces['xmlns:soapenv'] = 'http://schemas.xmlsoap.org/soap/envelope/'
      soap.header = SOME_HEADER
      soap.body = base_body 
    end

!SLIDE 

# Jammit

* Packs your CSS and Javascripts

!SLIDE code

# Define your assets

    @@@ Yaml

    embed_assets: 'datauri'
    javascripts:
      common:
        - public/javascripts/jquery-ui-1.8.5.custom.min.js
        - public/javascripts/rails.js
    stylesheets:
      common:
        - public/stylesheets/oocss-base.css
        - public/stylesheets/colorbox.css

!SLIDE code

# In your view

      @@@ Haml
      = include_stylesheets :common
      = include_javascripts :common

! SLIDE subsection

# Views

!SLIDE 

    @@@ HTML
    <!DOCTYPE html>
    <html>
      <head>
        <title>NGNews</title>
      </head>
      <body>
        <div class='container page'>
          <div class='beta'>
            <%= image_tag('beta.png')%>
          <header class='head line' role='banner'>
            <nav class='action-bar'>
              <ul>
                <li>
              </ul>
            </nav>
          </header>
        </div>
      </body>
    </html>

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

## jquery-example-rails6
rails6で、`jquery`を`Gemfile`、`bundle`でインストールする。

### 手順0

`rails new (プロジェクト名)`で適当にrailsプロジェクトを作成する。

### 手順1
#### ・Gemfile
`Gemfile`に下記を追加し、`bundle install`。
```ruby
gem 'jquery-rails'
gem 'jquery-ui-rails'
```

#### ・app/assets/config/manifest.js
`app/assets/config/manifest.js`に下記を追加する。
```js
//= link_tree ../javascripts
```

#### ・app/views/layouts/application.html.erb
`app/views/layouts/application.html.erb`に下記を追加する。
```js
<!DOCTYPE html>
<html>
  <head>
    <title>Testjquery</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>

    /*下2行を修正、追加。*/
    <%#= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```


### 手順2
#### rails g controller test demo
`rails g controller test demo`で`testコントローラー`と`demoアクション`を作成。
#### ・config/routes.rb
```ruby
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
  get '/demo', to: 'test#demo'
end
```

#### ・app/controllers/test_controller.rb
```ruby
class TestController < ApplicationController
  def demo
  end
end
```

#### ・app/views/test/demo.html.erb
`app/views/test/demo.html.erb`に下記を追加する。
```html
<h1>Ajax#index</h1>
<p class="page_name">赤色になるよ</p>
```


#### ・app/assets/javascripts/application.js
`app/assets/javascripts/application.js`(jquery)に下記を追加する。
```js
// listed below.
//
// Any JavaScript/Coffee file within this directory, lib/assets/javascripts, or any plugin's
// vendor/assets/javascripts directory can be referenced here using a relative path.
//
// It's not advisable to add code directly here, but if you do, it'll appear at the bottom of the
// compiled file. JavaScript code in this file should be added after the last require_* statement.
//
// Read Sprockets README (https://github.com/rails/sprockets#sprockets-directives) for details
// about supported directives.
//
//= require jquery
//= require rails-ujs
//= require turbolinks
//= require_tree .


$(function(){
  $('.page_name').css("color", '#FF0000')
})
```

### 手順3
`rails s`で`localhost:3000`にアクセス。
下の文字が赤色になったらjqueryの読み込みが成功した。

![img](https://github.com/takihara-rbx/jquery-example-rails6/blob/master/reference/readme_image.png)

# README

This is a hello world app for my favorite Vue on Rails tutorial so far. 

It uses `foreman` to initiate the processes for both the rails server (for the backend) and webpack-dev-server (for the frontend) in one terminal.

Shout out to Ivan Shamatov for the [Tutorial](https://mkdev.me/en/posts/rails-5-vue-js-how-to-stop-worrying-and-love-the-frontend).

## Relevant Code

```
# Gemfile
gem 'webpacker'
```

```
# In the console

$ gem install foreman               # installs gem locally and not as a dependency
$ bundle install
$ rails webpacker:install           # installs webpacker
$ rails webpacker:install:vue       # installs vue, generates template, settings
$ yarn install                      # installs necessary npm-packages
```

```ecmascript 6
// app/javascript/packs/application.js

require('./hello_vue')
```

```ecmascript 6
// app/javascript/packs/hello_vue.js

import Vue from 'vue'
import App from '../components/app.vue'

document.addEventListener('DOMContentLoaded', () => {
  const app = new Vue({
    render: h => h(App)
  }).$mount()
  document.body.appendChild(app.$el)

  console.log(app)
})
```

```
// app/javascript/components/app.vue

<template>
  <div id="app">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      message: "Welcome to Cinematronix!"
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>

```

```
<!DOCTYPE html>
<html>
  <head>
    <title>Cinematronix</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>

    <%= javascript_pack_tag 'application' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

```
# In the console
$ rails g controller landing index
```

```ruby
# config/routes.rb
root to: 'landing#index' 
```

```
# Procfile
backend: rails s -p 3000
frontend: webpack-dev-server
```

```ruby
# config/environments/development.rb
Rails.application.configure do
  # Make javascript_pack_tag load assets from webpack-dev-server.
  config.x.webpacker[:dev_server_host] = 'http://localhost:8080' 
end
```

```
# In the console
# To start the application's server processes
$ foreman start
```
# README

Sample app that adds Bootstrap 5, JavaScript and Images to Rails 6.1 App

## Version

- ruby 3.2.1 (2023-02-08 revision 31819e82c8) [arm64-darwin22]
- Rails 6.1.7.3
- Bootstrap 5.3.0-alpha1

## Instructions

1. In `application.html.erb` change to stylesheet_pack_tag as shown:
```ruby
# from <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
<%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
```
1. Create new files/folders in `app/javascript`:
  ```
  app/javascript
  └───images
  │       test.jpg
  │
  └───packs
  │       application.js # already exists
  │       application.scss
  │
  └───src
  │       my_script.js
  │
  └───stylesheets
          my_styles.scss
  ```

  ```console
    cd new_app
    touch ./app/javascript/packs/application.scss
    mkdir -p ./app/javascript/src && touch ./app/javascript/src/my_script.js
    mkdir -p ./app/javascript/stylesheets && touch ./app/javascript/stylesheets/my_styles.scss
    mkdir -p ./app/javascript/images && cp ~/pictures/coco.jpg ./app/javascript/images/coco.jpg

  ```

3. Add Bootstrap and Popper JS to app
```shell
  yarn add bootstrap@5.3.0-alpha1 @popperjs/core

```

4. Include Bootstrap in `application.js` file:
```javascript
require.context("../images", true)
import "bootstrap"
import "@popperjs/core"
import "../src/my_script.js"
```

Include Bootstrap in `application.scss` file:
```scss
@import "~bootstrap/scss/bootstrap.scss";
@import "../stylesheets/my_styles.scss"

```

5. Create home controller with index action
   http://127.0.0.1:3000/home/index
```sh
  rails g controller home index
```

1. Add Bootstrap [modal](https://getbootstrap.com/docs/5.3/components/modal/) component in `app/views/home/index.html.erb`
```html
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
  Launch demo modal
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
```

7. Add Image tag in `app/views/home/index.html.erb`
```html+erb
<br>
<%= image_pack_tag "media/images/coco.jpg", height: '300px', width: 'auto' %>
```

8. may need to run 
```sh
  export NODE_OPTIONS=--openssl-legacy-provider && rails s
```

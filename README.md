# Proxy-facebook-login

> A Vue.js project is middle ware for login with facebook.

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

## Set App ID
``` bash
# set app id in function statusChangeCallback
let appId = 'YOUR_APP_ID'

# set app id in mounted
window.fbAsyncInit = () => {
  FB.init({
    appId: 'YOUR_APP_ID',
    cookie: true,
    xfbml: true,
    version: 'v2.8'
  })
  FB.getLoginStatus(function (response) {
    vm.statusChangeCallback(response)
  })
}
```

## Usage
``` bash
# login : redirect your app to..
http://localhost:8080/?action=login&plugin_uri=YOUR_REDIRECT_URL
# logout : redirect your app to..
http://localhost:8080/?action=logout&plugin_uri=YOUR_REDIRECT_URL

```
## Note.
``` bash
Don't forget to set app domain in your Facebook app.
```
For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

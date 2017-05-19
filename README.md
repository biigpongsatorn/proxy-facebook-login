# proxy-facebook-login

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

## Set app id and redirect Url
``` bash
# set app id and redirect Url
let appId = 'YOUR_APP_ID'
let uri = encodeURI('http://localhost:8080/')

# set app id
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

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

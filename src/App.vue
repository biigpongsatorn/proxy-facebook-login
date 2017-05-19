<template>
  <div id="app">
    <h1>facebook {{ action }} . . .</h1>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Proxy Facebook ',
      action: ''
    }
  },
  methods: {
    logout (uri) {
      let vm = this
      FB.logout(function (response) {
        window.location = encodeURI(uri)
      })
    },
    getParameterByName (name) {
      let url = window.location.href
      name = name.replace(/[\[\]]/g, "\\$&")
      let regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
          results = regex.exec(url)
      if (!results) return null
      if (!results[2]) return ''
      return decodeURIComponent(results[2].replace(/\+/g, " "))
    },
    statusChangeCallback (response) {
      let vm = this
      let appId = 'YOUR_APP_ID'
      let uri = encodeURI('http://localhost:8080/')
      let redirect_uri = vm.getParameterByName('redirect_uri') || JSON.parse(localStorage.getItem('redirect_uri'))

      if (vm.action === 'logout') {
        vm.logout(redirect_uri)
      } else {
        if (response.status === 'connected') {
          if (redirect_uri) {
            if (redirect_uri == JSON.parse(localStorage.getItem('redirect_uri'))) {
              localStorage.removeItem('redirect_uri')
            }
            // Send response to redirect_uri
            window.location = encodeURI(`${redirect_uri}?userID=${response.authResponse.userID}`)
          } else {
            // Handle Error
            alert('Not have redirect uri.')
          }
        } else {
          let param = vm.getParameterByName('redirect_uri')
          if (param) {
            localStorage.setItem('redirect_uri', JSON.stringify(param))
            window.location = encodeURI(`https://www.facebook.com/dialog/oauth?client_id=${appId}&redirect_uri=${uri}&response_type=token`)
          }
        }
      }
    }
  },
  mounted () {
    let vm = this
    vm.action = vm.getParameterByName('action')
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
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

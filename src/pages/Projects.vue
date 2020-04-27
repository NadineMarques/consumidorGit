<template>
  <div class="q-pa-md">
    <q-list>
      <q-item v-ripple>
        <q-item-section avatar>
          <q-avatar rounded id="avatar"></q-avatar>
        </q-item-section>

        <q-item-section id="name"></q-item-section>
      </q-item>
    </q-list>

    <q-list id="qlist">
    </q-list>
  </div>
</template>

<script>
export default {
  name: 'PageProjects'
}

var axios = require('axios')
var username = 'torvalds'

axios.get('https://api.github.com/users/' + username)
  .then(function (response) {
    var avatar = document.querySelector('#avatar')
    var name = document.querySelector('#name')

    avatar.innerHTML = '<img src="' + response.data.avatar_url + '">'
    name.textContent = response.data.login + ' - Repositórios'
  })

axios.get('https://api.github.com/users/' + username + '/repos')
  .then(function (response) {
    if (response.data) {
      console.log(response)
      var qlist = document.querySelector('#qlist')
      response.data.forEach(element => {
        var description = ''
        if (element.description) {
          description = '<div class="q-item__label q-item__label--caption text-caption">' + element.description + '</div>'
        }

        qlist.insertAdjacentHTML('beforeend', '<div tabindex="0" class="q-item q-item-type row no-wrap q-item--clickable q-link cursor-pointer q-focusable q-hoverable"><div tabindex="-1" class="q-focus-helper"></div><div class="q-item__section column q-item__section--avatar q-item__section--side justify-center"><i aria-hidden="true" role="presentation" class="material-icons q-icon notranslate text-primary">code</i></div><div class="q-item__section column q-item__section--main justify-center"><div class="q-item__label">' + element.name + description)
      })
    }
  })
</script>

<template>
  <div class="q-pa-md">
    <q-list>
      <q-item>
        <q-item-section avatar>
          <q-avatar rounded id="avatar"><img :src=avatar></q-avatar>
        </q-item-section>

        <q-item-section id="name">
          {{ login }} - Repositórios
        </q-item-section>
      </q-item>
    </q-list>

    <q-list id="qlist">
      <q-item clickable v-ripple v-for="repo in repos" v-bind:key="repo.name" :to="{ name: 'project', params: { user:login, name:repo.name } }" exact>
        <q-item-section>
          <q-item-label>
            {{ repo.name }}
          </q-item-label>

          <q-item-label caption>
            {{ repo.description }}
          </q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script>
var axios = require('axios')
var username = 'torvalds'

export default {
  name: 'PageProjects',

  data () {
    return {
      avatar: '',
      login: '',
      axios: require('axios'),
      username: 'torvalds',
      repos: ''
    }
  },

  mounted () {
    axios.get('https://api.github.com/users/' + username)
      .then(response => {
        this.avatar = response.data.avatar_url
        this.login = response.data.login
      })

    axios.get('https://api.github.com/users/' + username + '/repos')
      .then(response => {
        this.repos = response.data
      })
  }
}
</script>

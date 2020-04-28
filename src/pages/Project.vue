<template>
  <div class="q-pa-md">
    <q-list>
      <q-item>
        <q-item-section avatar>
          <q-avatar rounded><i class="las la-code-branch"></i></q-avatar>
        </q-item-section>

        <q-item-section>
          Branches - {{ repoName }}
        </q-item-section>
      </q-item>
    </q-list>

   <q-list id="qlist">
      <q-item clickable v-ripple v-for="branch in branches" v-bind:key="branch.name">
        <q-item-section>
          <q-item-label>
            {{ branch.name }}
          </q-item-label>

          <q-item-label caption>
            {{ branch.description }}
          </q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </div>
</template>

<script>
var axios = require('axios')

export default {
  name: 'PageProject',

  data () {
    return {
      avatar: '',
      repoName: '',
      branches: ''
    }
  },

  mounted () {
    axios.get(`https://api.github.com/users/${this.$route.params.user}`)
      .then(response => {
        this.avatar = response.data.avatar_url
      })

    axios.get(`https://api.github.com/repos/${this.$route.params.user}/${this.$route.params.name}`)
      .then(response => {
        this.repoName = response.data.full_name
      })

    axios.get(`https://api.github.com/repos/${this.$route.params.user}/${this.$route.params.name}/branches`)
      .then(response => {
        this.branches = response.data
      })
  }
}
</script>

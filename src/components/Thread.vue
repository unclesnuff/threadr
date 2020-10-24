<template lang="pug">
  .thread.ui.container
    .ui.one.column.centered.grid.cards
      .column(v-for='p in posts')
        post(
          :id="p.id",
          :img="p.img",
          :name="p.name",
          :comment="p.comment",
          :date="p.date",
          :ext="p.ext",
          :board="p.board"
        )
</template>
<script>
  import Post from './Post.vue'
  import axios from 'axios'

  export default {
    name: 'thread',
    data () {
      return {
        posts: []
      }
    },
    beforeMount () {
      axios.get('https://cors-anywhere.herokuapp.com/https://a.4cdn.org' + this.$route.params.board + '/thread/' + this.$route.params.id + '.json')
        .then(response => {
          response.data.posts.forEach(e => {
            this.posts.push({
              id: e.no,
              img: e.tim,
              name: e.name,
              comment: e.com,
              date: e.now,
              ext: e.ext,
              board: this.$route.params.board
            })
          })
        })
    },
    components: {
      Post
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container {
    padding-top:5%;
  }
</style>

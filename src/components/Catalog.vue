<template>
<div class="container ui">
    <div class="grid ui four column stackable cards">
        <div class="column" v-for="thread in threads">
            <threadPreview :id="thread.id" :description="thread.description" :img="thread.img" :board="board" :replies="thread.replies"></threadPreview>
        </div>
    </div>
</div>
</template>

<script>
import ThreadPreview from './ThreadPreview.vue'
import axios from 'axios'

export default {
    name: 'catalog',
    data() {

        return {
            threads: [],
            board: '',
            page: '0'
        }
    },
    methods: {
        // use Lodash debounce to throttle search rendering/reloading (400 milliseconds)
        searchTermChange: function () {
            //  pass event up to parent App.vue
            this.$emit("termChange", this.searchTerm);
        },
    },
    components: {
        ThreadPreview
    },
    watch: {

        '$route'(data) {
            let page = '0'
            this.board = data.path
            this.threads = []
            axios.get('https://cors-anywhere.herokuapp.com/https://a.4cdn.org' + this.board + '/catalog.json')
                .then((response) => {
                    response.data[page].threads.forEach(e => {
                        this.threads.push({
                            id: e.no,
                            description: e.com.substr(0, 150),
                            img: e.tim + e.ext,
                            replies: e.replies
                        })
                    })
                })
        }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
.container {
    padding-top: 5%;
}
</style>

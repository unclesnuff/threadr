<template>
<div class="top">
    <div class="ui menu inverted green"><a class="header item" v-on:click="showBar">VueChan</a></div>

    <div class="ui left sidebar inverted vertical menu">
        <router-link class="item" v-on:click="hideBar" v-for="menu in menus" :key="menu.board" :to="{name: 'catalog', params: { board: menu.board}}">{{menu.title}}</router-link>
    </div>

</div>
</template>

<script>
import axios from 'axios'
import jquery from 'jquery'

export default {
    name: 'sidebar',
    beforeMount() {
        axios.get('https://cors-anywhere.herokuapp.com/https://a.4cdn.org/boards.json')
            .then(response => {
                response.data.boards.forEach(e => {
                    this.menus.push({
                        title: e.title,
                        board: e.board
                    })
                })
            })
    },
    data() {
        return {
            menus: [],
            board: ''
        }
    },
    methods: {
        showBar: function () {
            jquery('.sidebar').sidebar('show')
        },
        hideBar: function () {
            jquery('.sidebar').sidebar('hide')
        }
    }
}
</script>

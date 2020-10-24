<template lang="pug">
.ui.fluid.card
    .image
        img(v-bind:src="imglink")
    .content(v-html="description")

    .extra.content
        i.comment.icon {{replies}} - {{id}}
        router-link.ui.button.primary.tiny.right.floated(tag="button" :to="{name: 'thread', params: { id: id, board: board}}") view thread
</template>

<script>
export default {
    name: 'threadPreview',
    props: ['id', 'img', 'description', 'board', 'replies'],
    beforeMount() {
        this.imglink = 'https://t.4cdn.org' + '' + this.board + '/' + this.img
    },
    data() {
        return {
            imglink: ''
        }
    }
}
</script>

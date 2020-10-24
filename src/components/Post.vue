<template lang="pug">
.ui.fluid.card
    .image
        img(v-bind:src="imglink")
    .content
        .header {{name}}
        .meta 
            span.date {{date}}
    description(v-html="comment")
</template>

<script>
export default {
    name: 'post',
    props: ['id', 'img', 'name', 'comment', 'date', 'board', 'ext'],
    beforeMount() {
        if (this.img !== undefined) {
            this.imglink = 'http://i.4cdn.org' + this.board + '/' + this.img + this.ext
        }
    },
    data() {
        return {
            imglink: ''
        }
    }
}
</script>

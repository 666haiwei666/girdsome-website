<template>
    <layout>
        <div class="journal-container">
            <div class="journal-header">
                <div class="journal-title">
                    <h1>{{jounals.title}}</h1>
                </div>
            </div>
            <div class="journal-meta">
                <div class="journal-author">
                    <div class="label">Author</div>
                    <div class="value"> {{jounals.author}}</div>
                </div>
                <div class="journal-date">
                    <div class="label">Date</div>
                    <div class="value">{{jounals.data}}</div>
                </div>
                <div class="journal-time">
                    <div class="label">Time</div>
                    <div class="value">{{jounals.time}}</div>
                </div>
            </div>
            <div v-html='html(jounals.content)'>

            </div>
        </div>
    </layout>
</template>
<page-query>
    query($id:ID!) {
    strapiJounals(id:$id){
    id
    title
    author
    data
    time
    description
    content
    }
    }
</page-query>

<script>
    let MarkdownIt = require('markdown-it')
    let md = new MarkdownIt()
    export default {
        computed: {
            imageUrl() {
                return function (imgurl) {
                    return process.env.GRIDSOME_API_URL + imgurl
                }
            },
            jounals() {
                return this.$page.strapiJounals
            }
        },
        methods: {
            html(markdown) {
                return md.render(markdown);
            }
        }

    }
</script>
<style>
    .journal-meta {
        display: flex;

    }

    .label {
        display: block;
        font-weight: 700;
        margin-bottom: .3rem;
    }

    .value {
        margin-bottom: .3rem;
    }

    .journal-meta>div {
        margin-right: 4rem;
    }

    .journal-header {
        padding: 2rem 0 4rem;
    }

    .journal-title {
        font-size: 2rem;
        margin: 0 0 4rem;
        padding: 0;
    }

    .journal-container {
        max-width: 840px;
    }
</style>
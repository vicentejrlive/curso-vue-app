<template>
    <div class="article-by-id">
        <PageTitle icon="fa fa-file-o" :main="article.name" :sub="article.description"></PageTitle>
        <div class="article-content" v-html="article.content">

        </div>
    </div>
</template>

<script>
import 'highlightjs/styles/dracula.css'
import hljs from 'highlightjs/highlight.pack.js'
import { baseApiUrl } from '@/global'
import axios from 'axios'
import PageTitle from '../template/PageTitle'

export default {
    name: 'articleById',
    components: { PageTitle },
    data(){
        return {
             article: {}
        }
    },
    mounted(){
        const url = `${baseApiUrl}/articles/${this.$route.params.id}`
        axios.get(url).then(res => this.article = res.data)
    },
    updated(){
        document.querySelectorAll('.article-content pre').forEach(e => {
            hljs.highlightBlock(e)
        })
    }
}
</script>

<style>
    .article-content{
        background-color: white;
        border-radius: 8px;
        padding: 25px;
    }

    .article-content pre{
        border-radius: 8px;
        padding: 20px;
        font-size: 1.2rem;
        background-color: #424242;
        color: white;
    }

    .article-content img{
        max-width: 100%;
    }

    .article-content :last-child{
        margin-bottom: 0;
    }
</style>
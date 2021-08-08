<template>
    <layout>
        <div class="product">
            <div class="product-header">
                <h1 class="project-title">{{product.title}}</h1>
                <div class="project-info">
                    <div class="categories-container">
                        <div class="categories">
                            <span class="label">Categories</span>
                            <div class="">
                                <span v-for="(item,index) in product.category">
                                    {{ item.title}}
                                </span>
                            </div>
                        </div>
                    </div>
                    <div class="year">
                        <div class="year">
                            <span class="label">year</span>
                            <div class="">
                                {{product.year}}
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="content">{{product.content}}</div>
            <img class="project-img" :src='imageUrl(product.image.url)' crossOrigin></img>
        </div>
    </layout>
</template>
<page-query>
    query($id:ID!) {
    strapiProjects(id:$id){
    id
    title
    year
    image {
    url
    }
    category {
    title
    }
    content
    }
    }
</page-query>

<script>
    export default {
        beforeRouteEnter(to, form, next) {
            next(vm => {
                document.body.style.color = vm.product.category[0].title
                document.body.style.backgroundColor = '#EDEDED'
            })
        },
        beforeRouteLeave(to, form, next) {
            document.body.style.color = null
            document.body.style.backgroundColor = ''
            next()
        },
        computed: {
            imageUrl() {
                return function (imgurl) {
                    return process.env.GRIDSOME_API_URL + imgurl
                }
            },
            product() {
                return this.$page.strapiProjects
            }
        }
    }
</script>
<style>
    .product {}

    .product-header {
        padding: 20vh 0 4rem;
    }

    .content {
        margin: 20px 0;
    }

    .project-info {
        display: inline-flex;
        flex-wrap: wrap;
        font-size: .8rem;
    }

    .categories-container {
        margin-right: 4rem;
    }

    .label {
        display: block;
        font-weight: 700;
        margin-bottom: .5rem;
    }

    .project-title {
        font-size: 4rem;
        margin: 0 0 4rem;
        padding: 0;
    }
</style>
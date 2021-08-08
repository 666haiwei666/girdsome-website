<template>
  <Layout>
    <div class="hero">
      <h1 class="hero-title">{{general.title}}</h1>
      <p class="hero-subtitle">
        {{general.subtitle}}
      </p>
    </div>
    <div class="projects">
      <div v-for="(item,index) in products" :key='index' class="project">
        <g-link class="nav__link" :to="`/project/${item.node.id}`">
          <img class="projects-img" :src='imageUrl(item.node.image.url)' crossOrigin></img>
          <div>
            <span class="project-title">{{item.node.title}}</span>
            <p class="category">
              <span v-for="(k,i) in item.node.category" :key='i'>
                {{k.title}}
              </span>
            </p>
          </div>
        </g-link>
      </div>
    </div>
    <div class="journals">
      <div class="label">Latest and greatest</div>
      <div class="latest-journals">
        <g-link v-for="(item,index) in journals" :key='index' class="journal" :to="`/journal/${item.node.id}`">
          <div class="title">{{item.node.title}}</div>
        </g-link>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query {
  allStrapiJounals(sort: [{ by: "id" ,order: ASC }]) {
  edges {
  node {
  id
  title
  }
  }
  }
  allStrapiGeneral{
  edges {
  node {
  id
  title
  subtitle
  }
  }
  }
  allStrapiProjects(sort: [{ by: "id" ,order: ASC }]) {
  edges {
  node {
  id
  title
  category {
  title
  }
  image {
  id
  url
  }
  }
  }
  }
  }
</page-query>

<script>
  export default {
    metaInfo: {
      title: 'Hello, world!'
    },
    computed: {
      imageUrl() {
        return function (imgurl) {
          return process.env.GRIDSOME_API_URL + imgurl
        }
      },
      general() {
        return this.$page.allStrapiGeneral.edges[0].node
      },
      products() {
        return this.$page.allStrapiProjects.edges
      },
      journals() {
        return this.$page.allStrapiJounals.edges
      }
    }
  }
</script>

<style scoped>
  .latest-journals {
    margin: 0;
    border-left: 0;
    border-right: 0;
    border-top: 1px solid #cccccc;
    border-bottom: 1px solid #cccccc;
    display: flex;
  }

  .journal {
    border-left: 1px solid #cccccc;
    border-right: 1px solid #cccccc;
    padding: 2rem 0;
    width: 25%;
    display: inline-block;
    text-decoration: none;
    text-align: center;
  }
  .journal:hover{
     background-color: #cccccc;
  }

  .title {
    color: black;
    font-size: 1rem;
    line-height: 1.35;
    font-weight: 600;
  }

  .label {
    display: block;
    font-weight: 700;
    margin-bottom: .5rem;
  }

  .home-links a {
    margin-right: 1rem;
  }

  .projects {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 4rem;
  }

  .project {
    text-align: center;
  }

  .projects-img:hover {
    transform: scale(1.03);
  }

  .projects-img {
    width: 100%;
    height: 560px;
    -o-object-fit: cover;
    object-fit: cover;
    transition: all .15s ease;
    box-shadow: 0 0 40px -20px rgb(0 0 0 / 25%);
  }

  .project-title {
    font-size: 1rem;
    color: #333333;
    margin: 2rem 0 1rem;
  }

  .category {
    font-size: .8rem;
    color: #cccccc;
  }

  .category>span {
    display: inline-block;
    margin-left: 15px;
  }

  .hero {
    text-align: center;
    width: 480px;
    max-width: 100%;
    margin: 0 auto;
    padding: 4rem 0 8rem;
  }

  .hero-title {
    font-size: 3rem;
    font-weight: 700;
    padding: 0;
    margin: 0 0 2rem;
  }

  .hero-subtitle {
    font-size: 1.15em;
    font-weight: 400;
    line-height: 1.68;
    opacity: .6;
  }
</style>
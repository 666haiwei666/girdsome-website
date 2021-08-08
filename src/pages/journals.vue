<template>
  <Layout>
    <div class="journal-hero">
      <div class="journal-hero-title">a wise person once said..</div>
    </div>
    <div class='journals'>
      <g-link v-for="(item,index) in journals" :key='index' class="journal" :to="`/journal/${item.node.id}`">
        <h2 class="title">{{item.node.title}}</h2>
        <p class="description">{{item.node.description}}</p>
      </g-link>
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
  description
  }
  }
  }
  }
</page-query>
<script>
  export default {
    metaInfo: {
      title: 'About us'
    },
    computed: {
      journals() {
        return this.$page.allStrapiJounals.edges
      }
    }
  }
</script>
<style>
  .journal-hero {
    padding: 4rem 0;
    text-align: center;
    color: #cccccc;
  }

  .journal-hero-title {
    font-size: 3rem;
    font-weight: 700;
    padding: 0;
    margin: 0;
  }

  .journals {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .journal {
    padding: 5rem 6rem;
    width: 100%;
    transition: transform .5s ease;
    text-decoration: none;
    text-align: center;
    color: black;
    display: inline-block;
  }

  .journal:hover {
    background-color: #cccccc;
  }
</style>
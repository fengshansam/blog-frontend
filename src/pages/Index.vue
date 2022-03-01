<template>
  <Layout>
    <header
      class="masthead"
      :style="{
        backgroundImage:`url(${GRIDSOME_API_URL + general.cover[0].url})`
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{general.title}}</h1>
              <span class="subheading">{{general.title}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">
                {{edge.node.title}}
              </h2>
            </g-link>
            <p class="post-meta">
              Posted by
              {{edge.node.created_at}}
              <p>
                <g-link :to="'/post/' + edge.node.id" v-for="tag in edge.node.tags" :key="tag.id">{{tag.title}} &nbsp;&nbsp;</g-link>
              </p>
            </p>
             <hr class="my-4" />
          </div>
          <Pager :info="$page.posts.pageInfo"/>
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query($page: Int){
  posts: allStrapiPost(perPage: 2, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges{
      node{
        id
        title
        created_at
        tags{
          id
          title
        }
      }
    }
  }
  allStrapiGeneral{
    edges{
      node{
        id
        title
        cover{
          id
          url
        }
      }
    }
  }
}
</page-query>


<script>
import { Pager } from 'gridsome'
export default {
  name: 'HomePage',
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager
  },
  computed: {
    general () {
      return this.$page.allStrapiGeneral.edges[0].node
    }
  }
};
</script>

<style>
</style>

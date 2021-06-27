<template>
  <Layout>
    <div>
      <div class="container">
        <div class="journal-hero">
          <h1 class="journal-header">a wise person once said...</h1>
        </div>
      </div>
      <g-link
        class="journal-post"
        v-for="edge in $page.posts.edges"
        :key="edge.node.id"
        :to="'/journal/' + edge.node.id"
      >
        <div class="container journal">
          <h2 class="journal-title">{{ edge.node.title }}</h2>
          <div class="journal-excerpt">{{ edge.node.describe }}</div>
        </div>
      </g-link>
    </div>
  </Layout>
</template>

<page-query>
query {
  posts: allStrapiJournal {
    edges {
      node {
        id
        title
        describe
      }
    }
  }
}
</page-query>

<script>
import MarkdownIt from "markdown-it";
const md = new MarkdownIt();

export default {
  name: "Journal",
  methods: {
    mdToHtml(markdown) {
      return md.render(markdown);
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 4rem 0 0;
}
.journal-hero {
  padding: 4rem 0;
  text-align: center;
  color: #f3f3f3;
}
.journal-header {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0;
}
.journal-title {
  font-size: 2rem;
  color: #000;
}
.journal-post {
  display: block;
  text-decoration: none;
  color: #000;
}

.journal-post:hover {
  background: #f3f3f3;
  text-decoration: none !important;
  color:#000;
}
.journal {
  padding: 5rem 0;
  max-width: 720px;
  transition: transform 0.5s ease;
}
.journal:hover {
  transform: translateX(4rem);
}

.journal-exceperpt {
  color: #2b2b2b;
}
p {
  line-height: 1.5;
  font-size: 1.15rem;
}
</style>

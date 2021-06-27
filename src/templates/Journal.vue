<template>
  <Layout>
    <div class="journal">
      <div class="container journal-container">
        <div class="journal-header">
          <h1 class="journal-title">{{ $page.journal.title }}</h1>
          <div class="journal-meta">
            <div class="journal-author">
              <span class="label">Author</span>
              <span class="author-name">{{$page.journal.author.username}}</span>
            </div>
            <div class="journal-date">
              <span class="label">Date</span>
              <div>27. June 2021</div>
            </div>
            <div class="journal-time">
              <span class="label">Time</span>
              <span>1 min read</span>
            </div>
          </div>
        </div>
        <div
          class="journal-content"
          v-html="mdToHtml($page.journal.content)"
        ></div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  journal:strapiJournal (id: $id) {
    title
    content
    author{
      username
    }
  }
}
</page-query>

<script>
var MarkdownIt = require("markdown-it");
const md = new MarkdownIt();
export default {
  name: "JournalTempalte",
  methods: {
    mdToHtml(markdown) {
      return md.render(markdown);
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.journal-container {
  max-width: 840px;
  padding: 4rem 0 0;
  margin: 0 auto;
}
.journal-header {
  padding: 2rem 0 4rem;
}
.journal-title {
  font-size: 4rem;
  margin: 0 auto;
  padding: 4rem 0 8rem;
}
.journal-meta {
  display: flex;
  flex-wrap: wrap;
  font-size: 0.8rem;
}
.journal-author {
  margin-right: 4rem;
}
.journal-date {
  margin-right: 4rem;
}
.journal-time {
  margin: 0;
}
.label {
  display: block;
  font-weight: 700;
  margin-bottom: 0.5rem;
}
</style>

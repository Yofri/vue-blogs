<template>
  <div class="single-blog">
    <h1> {{blog.title}} </h1>
    <ul>
      <li v-for="category in blog.categories">
        {{category}}
      </li>
    </ul>
    <article> {{blog.content}} </article>
    <p>By: {{blog.author}} </p>
  </div>
</template>

<script>
  import searchMixin from '../mixins/searchMixin';

  export default {
    data() {
      return {
        id: this.$route.params.id,
        blog: {}
      }
    },
    created() {
      this.$http.get('https://vue-blog-7a8fa.firebaseio.com//posts/' + this.id + '.json')
                .then((data) => {
                  return data.json();
      }).then((data) => {
        this.blog = data;
      })
    }
  }
</script>

<style scoped>
  .single-blog {
    max-width: 600px;
    margin: 0 auto;
    padding: 1.25em;
    background: #eee;
    border: 1px dotted #aaa; }
</style>

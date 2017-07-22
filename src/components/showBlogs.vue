<template>
  <div class="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="search" placeholder="search blogs">
    <div class="single-blog" v-for="blog in filteredBlogs">
      <router-link v-bind:to="`/blog/${blog.id}`">
        <h2 v-rainbow> {{blog.title | upperCase}} </h2>
      </router-link>
      <article> {{blog.content | truncate}} </article>
    </div>
  </div>
</template>

<script>
  import searchMixin from '../mixins/searchMixin';

  export default {
    data() {
      return {
        blogs: [],
        search: ''
      }
    },
    created() {
      this.$http.get('https://vue-blog-7a8fa.firebaseio.com//posts.json')
                .then((data) => {
                  return data.json();
      }).then((data) => {
        let blogsArr = [];
        for (let key in data) {
          data[key].id = key;
          blogsArr.push(data[key]);
        }
        this.blogs = blogsArr;
      });
    },
    filters: {
      upperCase(val) {
        return val.toUpperCase();
      },
      truncate(val) {
        return `${val.slice(0, 100)}...`;
      }
    },
    directives: {
      'rainbow': {
        bind(el, binding, vnode) {
          el.style.color = `#${Math.random().toString(16).slice(2, 8)}`;
        }
      }
    },
    mixins: [searchMixin]
  }
</script>

<style scoped>
  .show-blogs {
    max-width: 600px;
    margin: 0 auto; }

  /*.show-blogs a {
    color: #444;
    text-decoration: none; }*/

  .single-blog {
    padding: 1.25em;
    margin: 1.25em 0;
    box-sizing: border-box;
    background-color: #eee; }

  input[type="text"] {
    padding: 0.5em;
    width: 100%;
    box-sizing: border-box; }
</style>

<template>
  <div>
    <app-header></app-header>
    <router-view></router-view>
  </div>
</template>

<script>
  import showBlogs from './components/showBlogs.vue';
  // import listBlogs from './components/listBlogs.vue';
  // import addBlog from './components/addBlog.vue';
  import header from './components/header.vue';

  export default {
    components: {
      // 'show-blogs': showBlogs,
      // 'list-blogs': listBlogs,
      // 'add-blog': addBlog,
      'app-header': header
    }
  }
</script>

<style>
  body {
    font-family: 'Roboto', Helvetica, Arial, sans-serif;
    margin: 0;
    padding: 0; }
</style>

<template>
  <div class="add-blog">
    <h2>Add a New Blog Post</h2>
    <form v-if="!submitted">
      <label>Blog Title:</label>
      <input type="text" v-model.lazy="blog.title" required>

      <label>Blog Content:</label>
      <textarea v-model.lazy="blog.content"></textarea>

      <div class="checkboxes">
        <p>Blog Categories:</p>

        <label>Ninjas</label>
        <input type="checkbox"
               value="ninjas"
               v-model="blog.categories" />

        <label>Wizards</label>
        <input type="checkbox"
               value="wizards"
               v-model="blog.categories" />

        <label>Warrior</label>
        <input type="checkbox"
               value="warrior"
               v-model="blog.categories" />
      </div>

      <label>Author:</label>
      <select v-model="blog.author">
        <option v-for="author in authors"> {{author}} </option>
      </select>

      <hr />

      <button v-on:click.prevent="post">Add Blog</button>
    </form>

    <h3 v-if="submitted">Thanks for adding your post</h3>

    <h3>Preview blog</h3>
    <div class="preview">
      <p> {{blog.title}} </p>
      <ul>
        <li v-for="category in blog.categories"> * {{category}} </li>
      </ul>
      <p> {{blog.content}} </p>
      <p>By: {{blog.author}} </p>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        blog: {
          title: '',
          content: '',
          categories: [],
          author: ''
        },
        authors: ['The Angular Avenger', 'The Vue Vindicator', 'The React Turncoat'],
        submitted: false
      }
    },
    methods: {
      post: function() {
        this.$http.post('https://vue-blog-7a8fa.firebaseio.com//posts.json', this.blog)
                  .then((data) => {
                    this.submitted = true;
        });
      }
    }
  }
</script>

<style>
  .add-blog * {
    box-sizing: border-box; }

  .add-blog {
    margin: 4em auto;
    max-width: 600px;
    padding: 1.25em; }

  label {
    display: block;
    margin: 1em 0 0.5em; }

  input[type="text"],
  textarea,
  select {
    display: block;
    width: 100%;
    padding: 0.5em; }

  .add-blog h3 {
    margin-top: 3em; }

  .preview {
    padding: 0.75em;
    border: 1px dotted #ccc; }

  .preview p:first-of-type {
    font-size: 1.5em; }

  input[type="checkbox"] {
    display: inline-block;
    margin-right: 0.75em; }

  .preview li {
    display: inline; }

  .checkboxes label {
    display: inline-block; }

  hr {
    display: none; }

  button {
    display: block;
    margin: 1.25em 0;
    background-color: crimson;
    color: #fff;
    border: 0;
    padding: 1em;
    border-radius: 0.25em;
    font-size: 1rem;
    cursor: pointer;
  }
</style>

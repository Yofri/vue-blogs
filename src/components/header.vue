<template>
  <nav>
    <ul>
      <li>
        <router-link to="/" exact>Blog</router-link>
      </li>
      <li>
        <router-link to="/add" exact>Add Post</router-link>
      </li>
    </ul>
  </nav>
</template>

// <script>
//   export default {}
// </script>

<style scoped>
  ul {
    list-style-type: none;
    text-align: center;
    margin: 0; }

  li {
    display: inline-block;
    margin: 0 0.75em; }

  a {
    color: #fff;
    text-decoration: none;
    padding: 0.5em 0.75em;
    border-radius: 4px; }

  nav {
    background-color: #444;
    padding: 0.75em;
    margin-bottom: 3em; }

  .router-link-active {
    background-color: #eee;
    color: #444; }
</style>

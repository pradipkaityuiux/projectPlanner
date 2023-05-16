<template>
    <nav class="main-nav">
      <router-link :to="{ name: 'Home'}">Projects</router-link>
      <router-link :to="{ name: 'AddProject'}">Add a New Project</router-link>
    </nav>
  </template>
  
  <script>
  export default {
  name:"Navbar"
  }
  </script>
  
  <style scoped>
  .main-nav{
    text-align: center;
    margin: 40px auto;
  }
  .main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 20px;
    color: #727272;
    font-size: 18px;
  }
  a.router-link-active{
    color: #2e2e2e;
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
  }
  
  </style>
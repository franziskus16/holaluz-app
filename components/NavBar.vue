<template>
      <div class="nav">
        <nuxt-link to="/" class="brand">Holaluz</nuxt-link>
        <nav>
          <nuxt-link to="/meet">Conocenos</nuxt-link>&nbsp;|
          <nuxt-link to="/create">Tarifas</nuxt-link>
        </nav>
      </div>
    </template>
    
    <style scoped>
    .brand {
      font-family: 'Yantramanav', sans-serif;
      font-weight: 700;
      font-size: 1.5em;
	    background: linear-gradient(to right, #ffba03 0%, #e6007d 100%);
	    -webkit-background-clip: text;
	    -webkit-text-fill-color: transparent;
      text-decoration: none;
    }
    .nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 60px;
    }
    .nav .nav-item {
      box-sizing: border-box;
      margin: 0 5px;
      color: rgba(0, 0, 0, 0.5);
      text-decoration: none;
    }
    .nav .nav-item.router-link-exact-active {
      color: #39b982;
      border-bottom: solid 2px #39b982;
    }
    .nav a {
      display: inline-block;
    }
    </style>

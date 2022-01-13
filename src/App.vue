<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <router-view/>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #35495E;
}

header {
  display: flex;
  padding: 10px 16px;
  align-items: center;
  justify-content: center;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}

header h1 {
  color: #fff;
  text-decoration: none;
  font-size: 28px;
}
header h1 span {
  color: #42B883;
}
</style>

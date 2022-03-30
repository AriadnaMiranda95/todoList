<template>
  <header>
    <a href="/" class="title">Vue Trello</a>
  </header>
</template>

<script>
export default {
  name: 'app-header'
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oswald&family=Yanone+Kaffeesatz&display=swap');
header {
  box-sizing: border-box;
  background: rgb(2,226,197);
  background: linear-gradient(90deg, rgba(2,226,197,1) 0%, rgba(0,255,222,1) 0%, rgba(240,103,228,1) 100%);
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin: 0;
  padding: 1rem;
  width: 100%;
}

.title {
  align-self: center;
  color: #ffffff;
  text-decoration: none;
  font-size: 2rem;
  font-weight: bold;
  margin-right: 1rem;
  font-family: 'Oswald', sans-serif;
  font-family: 'Yanone Kaffeesatz', sans-serif;
}

.title:hover{
  color: #de72e4;
}

</style>

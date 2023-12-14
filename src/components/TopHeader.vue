<!-- <script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script> -->

<template>
    <div class="container">
        <span>Logo</span>
        <span>Home</span>
        <span>Live sessions</span>
        <span>Video Series</span>
        <span>AP books</span>
        <span>AP articles</span>
        <span>Invite</span>
        <span>In media</span>
        <span>Donate</span>
    </div>
    <div class="second-container">
        <div class="access-text">Get access to all 350+ video series at once!</div>
        <div class="access-btn">Click Here</div>
    </div>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <!-- <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3> -->
  </div>
</template>

<style scoped>

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}
.container {
    align-items: center;
    width:100%;
    height: 7vh;
    display: flex;
    justify-content: space-around;
    color: rgb(233, 228, 228);
    background-color: #d24115;
}
span {
    font-weight: 700;
    font-size: 15px;
}
.second-container {
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    background-color: black;
    height: 8vh;
}
.access-text {
    font-size: 20px;
    margin: 10px;
}
.access-btn {
    font-size: 15px;
    padding: 0 10px;
    border: 1px solid white;
    border-radius: 8px;
    margin: 10px;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>

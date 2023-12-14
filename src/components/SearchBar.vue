<script>
import axios from 'axios';

const emitClickEvent = () => {
  // Emit a custom event to notify the parent component
  emit('click');
};

export default {
    data() {
        return {
            dataApi: [],
        };
    },
    mounted() {
        this.fetchDataFromApi();
    },
    methods: {
        async fetchDataFromApi() {
            try {
                const response = await axios.get('https://api.acharyaprashant.org/v2/legacy/courses/tags');
                // alert(JSON.stringify(response))
                this.dataApi = response.data;
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        },
  
    },
};
</script>

<template>
    <div class="container">
       <div class="left"><img src="../assets/video-series.png" alt="facebook" style="cursor: pointer;">

        <button class="all" @click="emitClickEvent">All</button>
       <input class="search-box" placeholder="Search for the video series">
       <button class="search-icon"><img src="../assets/search.png" width="20px"></button>
    </div>
    <div class="right">
    <button class="login">Login</button>
</div>
</div>
</template>

<style scoped>

.container {
    padding: 0 30px;
    border-bottom: 1px solid rgb(179, 177, 177);
    align-items: center;
    height: 6vh;
    display: flex;
    justify-content: space-between;
    color: #d24115;
    background-color: white;
    margin-top: 10px;
}
.left {
    font-weight: bold;
    font-size: 18px;
    
    width: 60%;
    display: flex;
}
.all {
    background-color: white;
    border-color: rgb(179, 177, 177);
    border-right: none;
    cursor: pointer;
}
.search-box {
    width: 70%;
    color: black;
    height: 5.6vh;
}
.search-icon {
    background-color: #fed7aa;
    cursor: pointer;
}
span {
    font-weight: 700;
    font-size: 15px;
}
.login {
    border: 1px solid transparent;
    border-radius: 6px;
    background-color: #ea580c;
    color: white;
    height: 20px;
    width: 40px;
    cursor: pointer;
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

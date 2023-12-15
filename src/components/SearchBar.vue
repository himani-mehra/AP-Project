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
        }

    }
};
</script>

<template>
    <div class="container">
        <div class="left"><img src="../assets/video-series.png" alt="series" style="cursor: pointer;">

            <div class="search-bar">
                <div class="all-dropdown" @click="emitClickEvent">
                    <button class="all">All</button>
                    <img class="down-arrow" src="../assets/down-arrow.png" width="15px" height="15px">
                </div>
                <input class="search-box" placeholder="Search for the video series" @click.stop="emitClickEvent">
                <button class="search-icon">
                    <img src="../assets/search.png" width="20px">
                </button>
            </div>

        </div>
        <div class="right">
            <button class="login">Login</button>
        </div>
    </div>
</template>

<style scoped>
.container {
    padding: 0 30px;
    border-bottom: 1px solid rgb(226, 224, 224);
    align-items: center;
    height: 6vh;
    display: flex;
    justify-content: space-between;
    color: #d24115;
    background-color: white;
    margin-top: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.right {
    flex: 50%;
    display: flex;
    justify-content: flex-end;
}

.left {
    font-weight: bold;
    font-size: 18px;
    width: 50%;
    display: flex;
    align-items: center;
}

.search-bar {
    width: -webkit-fill-available;
    display: flex;
    margin-left: 20px;
    margin-bottom: 7px;

}

.all-dropdown {
    display: flex;
    justify-content: space-around;
    border: 1px solid rgb(224, 223, 223);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    display: flex;
    cursor: pointer;
    width: 13%;
    border-radius: 4px 0 0 4px;
}

.down-arrow {
    margin-top: 10px;
}

.all {
    font-size: 12px;
    font-weight: 400;
    color: #64748b;
    cursor: pointer;
    border: none;
    background-color: white;
}

.search-box {
    width: 100%;
    background-color: white;
    border: none;
    border: 1px solid rgb(224, 223, 223);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    height: 5.6vh;
}

.search-icon {

    border: 1px solid rgb(224, 223, 223);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    background-color: #fed7aa;
    cursor: pointer;
    border-radius: 0 4px 4px 0;
}

span {
    font-weight: 700;
    font-size: 15px;
}

.login {
    margin-bottom: 10px;
    border: 1px solid transparent;
    border-radius: 6px;
    background-color: #ea580c;
    color: white;
    height: 30px;
    width: 50px;
    cursor: pointer;
    font-size: 15px;

}</style>

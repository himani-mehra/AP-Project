<script>
import axios from 'axios';

export default {
    data() {
        return {
            apiDetails: [],
        };
    },
    mounted() {
        this.fetchDataFromApi();
    },
    methods: {
        async fetchDataFromApi() {
            try {
                const response = await axios.get('https://api.acharyaprashant.org/v2/legacy/courses/series/optuser/course-series-eeb9d3');
                this.apiDetails = response.data;
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        },
        getImageUrl(thumbnail) {
            return `${thumbnail.domain}/${thumbnail.basePath}/${thumbnail.key}`;
        },
        formatCourseDuration(courseHours) {
            const hours = Math.floor(courseHours);
            const minutes = Math.round((courseHours - hours) * 60);
            const hoursString = hours > 0 ? `${hours} hour${hours > 1 ? 's' : ''}` : '';
            const minutesString = minutes > 0 ? `${minutes} minute${minutes > 1 ? 's' : ''}` : '';
            return `${hoursString}${hoursString && minutesString ? ' ' : ''}${minutesString}`;
        },
    },
};
</script>
<template>
    <div class="home-section">
        <span>Home</span>
        <img class="arrow-img" src="../assets/gray-arrow.png" alt="arrow" width="15px" height="15px"
            style="cursor: pointer;">

        <span class="span-sec"> संतवाणी</span>
    </div>
    <div class="topic" v-if="apiDetails.details">{{ apiDetails.details.title }}</div>
    <div class="mainn">
        <div class="container">
            <div class="left-section" v-if="apiDetails.details">
                <div class="image-container">
                    <img class="image"
                        src="https://cimg.acharyaprashant.org/images/img-4337ee73-d8a3-4c8b-951b-d09a5a6468d3/10/image.jpg"
                        alt="Course Thumbnail">
                    <img class="overlay" src="https://acharyaprashant.org/images/ic_apsignature_hindi.png"
                        alt="Overlay Image">
                </div>

            </div>
            <div class="right-section">
                <div class="heading" v-if="apiDetails.details">{{ apiDetails.details.subtitle }}</div>

                <div v-if="apiDetails.details" class="paragraph" style="color: #55535c;">
                    {{ apiDetails.details.description }}
                </div>
            </div>
        </div>
        <div class="share-section">
            <div class="share-series">Share this series:</div>
            <div class="social-media-section">
                <a class="facebook"
                    href="https://www.facebook.com/v5.0/dialog/share?app_id=671373654631248&channel_url=https%3A%2F%2Fstaticxx.facebook.com%2Fx%2Fconnect%2Fxd_arbiter%2F%3Fversion%3D46%23cb%3Df21323e34d76334%26domain%3Dacharyaprashant.org%26is_canvas%3Dfalse%26origin%3Dhttps%253A%252F%252Facharyaprashant.org%252Ff1e47c230d4f7ec%26relation%3Dopener&display=popup&e2e=%7B%7D&fallback_redirect_uri=https%3A%2F%2Facharyaprashant.org%2Fen%2Fcourses%2Fseries%2Fcourse-series-eeb9d3&hashtag=%23AcharyaPrashant&href=https%3A%2F%2Facharyaprashant.org%2Fen%2Fcourses%2Fseries%2Fcourse-series-eeb9d3&locale=en_US&next=https%3A%2F%2Fstaticxx.facebook.com%2Fx%2Fconnect%2Fxd_arbiter%2F%3Fversion%3D46%23cb%3Df3ae4f33e1ff5bc%26domain%3Dacharyaprashant.org%26is_canvas%3Dfalse%26origin%3Dhttps%253A%252F%252Facharyaprashant.org%252Ff1e47c230d4f7ec%26relation%3Dopener%26frame%3Df1bd6132a5bd24%26result%3D%2522xxRESULTTOKENxx%2522&quote=&sdk=joey&version=v5.0">
                    <img src="../assets/facebook.png" alt="facebook" width="30px" height="30px" style="cursor: pointer;">
                </a>
                <a class="twitter"
                    href="https://twitter.com/intent/tweet?url=https%3A%2F%2Facharyaprashant.org%2Fen%2Fcourses%2Fseries%2Fcourse-series-eeb9d3&text=%0A&hashtags=AcharyaPrashant,VideoSeries,wisdom,spirituality"
                    target="_blank">
                    <img src="../assets/twitter.png" alt="twitter" width="30px" height="25px"
                        style="cursor: pointer; margin-top: 4px;">
                </a>
                <a class="whatsapp"
                    href="https://api.whatsapp.com/send/?text=%0Ahttps%3A%2F%2Facharyaprashant.org%2Fen%2Fcourses%2Fseries%2Fcourse-series-eeb9d3&type=custom_url&app_absent=0"
                    target="_blank">
                    <img src="../assets/whatsapp.png" alt="twitter" width="30px" height="30px" style="cursor: pointer;">
                </a>
                <a class="linkedin"
                    href="https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Facharyaprashant.org%2Fen%2Fcourses%2Fseries%2Fcourse-series-eeb9d3"
                    target="_blank">
                    <img src="../assets/linkedin.png" alt="twitter" width="30px" height="30px" style="cursor: pointer;">
                </a>
            </div>
        </div>
        <div class="recommentded-video">
            <div class="video-series" v-if="apiDetails.details">Video Series ({{ apiDetails.details.coursesCount }})</div>
            <div class="course-grid">
                <div v-for="(course, index) in apiDetails.courses" :key="course.id" class="course-item">
                    <p class="bhaag">{{ `भाग ${index + 1}` }}</p>
                    <h2>{{ course.title }}</h2>
                    <p style="font-size: 14px;">{{ course.subtitle }}</p>
                    <p>{{ formatCourseDuration(course.courseHours) }}</p>
                    <p>Contribution: {{ course.amount }} <span class="original-amount">{{ `₹${course.originalAmount}`
                    }}</span></p>
                    <p class="language">{{ course.language }}</p>
                    <div class="payment-sec">
                        <div class="cart">ADD TO CART</div>
                        <div style="color: rgb(177 190 201);">|</div>
                        <div class="enrol">ENROL</div>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
.mainn {
    padding: 0 2rem;
}

.share-section {
    padding: 1rem 0;
    width: 40%;
}

.share-series {
    margin-bottom: 10px;
    font-weight: bold;
    color: rgb(92, 91, 91);
}

.social-media-section {
    width: 50%;
    display: flex;
    justify-content: space-between;
}

.facebook img:hover {
    content: url('../assets/change-facebook.png');
}

.twitter img:hover {
    content: url('../assets/change-twitter.png');
    width: 30px;
    height: 30px;
}

.whatsapp img:hover {
    content: url('../assets/change-whatsapp.png');
}

.linkedin img:hover {
    content: url('../assets/change-linkedin.png');
}





.container {
    display: flex;
}

.left-section {
    width: 50%;
}

.right-section {
    margin-left: 1rem;
    width: 80%;
}

.image {
    width: 100%;
    border-radius: 4px;
}

.heading {
    font-weight: bold;
    font-size: 20px;
    color: #1e293b;
}

.home-section {
    margin-top: 1rem;
    padding: 0 2rem;
    align-items: center;
    display: flex;
    color: rgb(92, 91, 91);
    background-color: white;
}

.arrow-img {
    margin: 2px 4px 0 4px;
}

.topic {
    color: #1e293b;
    margin: 1rem 0;
    padding: 0 2rem;
    font-weight: bold;
    font-size: 20px;
}

.span-sec {
    font-weight: 550;
    color: #475569;
    /* margin-left: 8px; */
    margin-top: 4px;
    font-size: 13px;
}

.image-container {
    width: 100%;
    position: relative;
    display: inline-block;
}

.overlay {
    position: absolute;
    bottom: 0;
    right: 0;
    width: 20%;
}

.video-series {
    font-size: 20px;
    font-weight: 600;
    margin-top: 2rem;
    padding-bottom: 10px;
    border-bottom: 1px solid #c6d0df;
}

.course-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    /* Adjust the gap between items as needed */
}

.course-item {
    cursor: pointer;
    border-bottom: 1px solid rgb(195, 201, 214);
    flex: 1 0 calc(33.33% - 20px);
    padding: 10px;
    max-width: calc(33.33% - 20px);
    box-sizing: border-box;
}

.course-item:hover {
    border-radius: 8px;
    border-bottom: none;
    background-color: #f1f5f9;
}

.bhaag {
    width: 10%;
    background-color: #94a3b8;
    color: white;
    font-size: 12px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 4px;
    margin-bottom: 0.5rem;
}

h2 {
    font-size: 15px;
    color: #2c384d;
    font-weight: 600;
    padding-top: 3px;
}

p {
    font-size: 15px;
    color: #4b5c79;
    padding-top: 3px;

}

.original-amount {
    text-decoration: line-through;
    margin-left: 5px;
    /* Add some margin for better visibility */
    top: 2px;
}

.language {
    display: flex;
    align-items: center;
    /* Center vertically */
    justify-content: center;
    /* Center horizontally */
    width: 40px;
    height: 20px;
    background-color: #c7e6f8;
    border-radius: 4px;
    font-size: 0.75rem;
    margin-top: 0.5rem;
}

.payment-sec {
    margin-top: 0.5rem;
    width: 40%;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.enrol {
    font-size: 12px;
    color: #ed8529;
    font-weight: bold;
}

.cart {
    font-size: 12px;
    color: #ed8529;
    font-weight: bold;
}

.enrol:hover {
    color: #cc7324;
}

.cart:hover {
    color: #cc7324;
}


@media (max-width: 800px) {
    .course-item {
        flex: 1 0 calc(50% - 20px);
        /* Two items in a row for smaller screens */
        max-width: calc(50% - 20px);
        /* Set maximum width accordingly */
    }
}

@media (max-width: 600px) {
    .course-item {
        flex: 1 0 calc(100% - 20px);
        /* One item in a row for even smaller screens */
        max-width: calc(100% - 20px);
        /* Set maximum width accordingly */
    }
}

@media (min-width: 1024px) {

    .greetings h1,
    .greetings h3 {
        text-align: left;
    }
}
</style>

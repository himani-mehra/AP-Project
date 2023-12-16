<template>
  <div class="container">
    <div class="left">
      <div style="font-weight: bold; font-size: 18px;">FAQs</div>
      <div class="faq-text">
        Can’t find the answer you’re looking for? Reach out to our
        <a href="https://acharyaprashant.org/en/technical-support" target="_blank" style="color: #e36b20;">support</a>
        team.
      </div>
    </div>
    <div class="right">
      <div v-for="item in apiData" :key="item.id">
        <div class="question-container">
          <div class="question">{{ item.question }} </div>
          <div class="dropdown-icon" @click="toggleAnswer(item)">
            {{ item.showAnswer ? '&#129173;' : '&#129175;' }}
          </div>
        </div>
        <div v-if="item.showAnswer" class="answer">{{ item.answer }}</div>
        <hr style="border-color: rgb(252, 253, 253);">

      </div>
    </div>
  </div>
  <div>
    <img src="../assets/footer-img.png" alt="footer" width="100%" style="cursor: pointer;">

  </div>
</template>
  
<script>
import axios from 'axios';

export default {
  data() {
    return {
      apiData: [],
    };
  },
  mounted() {
    this.fetchDataFromApi();
  },
  methods: {
    async fetchDataFromApi() {
      try {
        const response = await axios.get('https://api.acharyaprashant.org/v2/legacy/courses/faqs?language=english');
        this.apiData = response.data.map(item => ({ ...item, showAnswer: false }));
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    toggleAnswer(item) {
      item.showAnswer = !item.showAnswer;
    },
  },
};
</script>
  

<style scoped>
.container {
  background-color: #f9fbfd;
  display: flex;
  padding: 4rem;
}

.left {
  width: 33.33%;
}

.right {
  width: 100%;
  padding-left: 6rem;
}

.faq-text {
  font-size: 18px;
}


.question-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
  padding: 10px;
}

.question {
  flex-grow: 1;
  font-weight: bold;
  color: #475569;
  font-size: 16px;
  cursor: pointer;
}

.dropdown-icon {
  cursor: pointer;
}

.answer {
  margin-top: 8px;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>

<script setup>
import TopHeader from './components/TopHeader.vue'
import SearchBar from './components/SearchBar.vue'
import MainPage from './components/MainPage.vue'
import FAQSection from './components/FAQSection.vue'
import { ref } from 'vue'
import SearchBarModal from './components/SearchBarModal.vue'


const isSearchBarOpen = ref(false);

const openSearch = () => {
  isSearchBarOpen.value = true;
};

const closeSearch = () => {
  isSearchBarOpen.value = false;
};
</script>

<template>
  <TopHeader> </TopHeader>
  <SearchBar @click="openSearch"> </SearchBar>
  <SearchBarModal v-if="isSearchBarOpen" @close="closeSearch"></SearchBarModal>
  <MainPage>  </MainPage>
  <FAQSection> </FAQSection>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

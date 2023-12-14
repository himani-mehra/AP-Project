<script setup>
import { defineProps, defineEmits, ref, onMounted } from 'vue';
import axios from 'axios';

const props = defineProps(['isVisible']);
const emits = defineEmits();
const tags = ref([]);
const hoveredTagGroup = ref(null);


const closeModal = () => {
    emits('close');
};


onMounted(async () => {
    try {
        const response = await axios.get('https://api.acharyaprashant.org/v2/legacy/courses/tags');
        tags.value = response;
    } catch (error) {
        console.error('Error fetching data:', error);
    }
});
const showSubDropdown = (tagGroup) => {
    hoveredTagGroup.value = tagGroup;
};

</script>

<template>
    <div class="modal" @click="closeModal">
        <div class="modal-content" @click.stop>
            <div class="dropdown-container">
                <div class="dropdown main-dropdown">
                    <div class="main-dropdown-item" @mouseover="showSubDropdown(null)">
                        All
                    </div>
                    <div v-for="(innerArray, outerIndex) in tags" :key="outerIndex">
                        <div v-for="(element, innerIndex) in innerArray[0]" :key="innerIndex" class="display-flex">
                            <div class="main-dropdown-item"
                                @mouseover="element.hasChildren ? showSubDropdown(innerArray) : showSubDropdown(null)">
                                {{ element.name.english }}
                            </div>

                            <div class="arrow" v-if="element.hasChildren">
                                <img src="../assets/gray-arrow.png" alt="gray arrow" class="gray-arrow" />
                                <img src="../assets/orange-arrow.png" alt="orange arrow" class="orange-arrow" />
                            </div>
                        </div>
                    </div>
                    <!-- {{ element }} -->
                </div>
                <div v-if="hoveredTagGroup" class="dropdown sub-dropdown">
                    <div v-for="(innerArray, outerIndex) in tags" :key="outerIndex">
                        <div v-for="(element, innerIndex) in innerArray[1]" :key="innerIndex" class="display-flex">
                            <div class="main-dropdown-item">
                                {{ element.name.english }}
                                <!-- {{ element }} -->
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.modal {
    cursor: pointer;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
}

.modal-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    z-index: 1000;
}

.dropdown-container {
    display: flex;
}

.dropdown {
    max-height: 300px;
    overflow-y: auto;
}

.main-dropdown {
    flex: 1;
}

.sub-dropdown {
    flex: 1;
}

.display-flex {
    display: flex;
    align-items: center;
    color: #ee7a3e;
}

/* .arrow {
    margin-top: 8px;
} */
.arrow {
    position: relative;
    width: 20px;
    height: 20px;
    display: inline-block;
}

.arrow img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    /* Ensure the image covers the container */
    transition: opacity 0.3s ease, display 0s 0.3s;
    /* Delay display change to avoid flicker */
}

.arrow .gray-arrow {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 1;
    z-index: 1;
}

.arrow .orange-arrow {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
    z-index: 2;
}

.arrow:hover .gray-arrow {
    opacity: 0;
    display: none;
}

.arrow:hover .orange-arrow {
    opacity: 1;
}

.main-dropdown-item {
    font-weight: 700;
    color: #515151;
}

.main-dropdown-item:hover {
    color: #ee7a3e;
}

.main-dropdown-item,
.sub-dropdown-item {
    padding: 8px;
    cursor: pointer;
}
</style>

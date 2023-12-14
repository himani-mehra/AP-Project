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
                            <div class="main-dropdown-item" @mouseover="showSubDropdown(innerArray)">
                                {{ element.name.english }}
                            </div>
                            <div v-if="element.hasChildren">*</div>
                        </div>
                    </div>
                    {{ element }}
                    <div v-if="hoveredTagGroup" class="dropdown sub-dropdown">
                        <div v-for="tag in hoveredTagGroup" :key="tag.tagId" class="sub-dropdown-item">
                            <!-- {{ tag }} -->
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
    /* border: 1px solid #ccc; */
}

.main-dropdown {
    flex: 1;
}

.sub-dropdown {
    flex: 1;
}
.display-flex {
    display: flex;
}
.main-dropdown-item {
    font-weight: 700;
    color: #61666e;
}
.main-dropdown-item:hover {
    color: #ee7a3e;
}
.main-dropdown-item,
.sub-dropdown-item {
    padding: 8px;
    /* border-bottom: 1px solid #ccc; */
    cursor: pointer;
}
</style>

<script>
export default {
    data() {
        return {
            apiUrl: 'https://api.acharyaprashant.org/v2/legacy/courses/tags',
            hierarchicalStructure: [],
        };
    },
    methods: {
        fetchData() {
            fetch(this.apiUrl)
                .then(response => response.json())
                .then(data => {
                    const level0Map = {};

                    data.forEach(level => {
                        level.forEach(item => {
                            const { level: itemLevel, tagId, parent, name } = item;

                            if (itemLevel === 0) {
                                level0Map[tagId] = { name: name.english, level: itemLevel, tagId, children: [], showChildren: false };
                            } else if (itemLevel === 1) {
                                if (level0Map[parent]) {
                                    level0Map[parent].children.push({ name: name.english, level: itemLevel, tagId, parent, children: [] });
                                }
                            }
                        });
                    });

                    this.hierarchicalStructure = Object.values(level0Map);
                })
                .catch(error => console.error('Error fetching data from the API:', error));
        },
        showChildren(tagId) {
            this.hierarchicalStructure.forEach(item => {
                if (item.tagId === tagId) {
                    item.showChildren = true;
                }
            });
        },
        hideChildren(tagId) {
            this.hierarchicalStructure.forEach(item => {
                if (item.tagId === tagId) {
                    item.showChildren = false;
                }
            });
        },
        shouldShowArrow(parentItem) {
      return parentItem.children.some(child => child.parent === parentItem.tagId);
    },
        closeModal() {
            this.$emit('close');
        },
    },
    mounted() {
        this.fetchData();
    },
};
</script>

<template>
    <div class="modal" @click="closeModal">
      <div class="modal-content" @click.stop>
        <div class="main-dropdown-item">
          All
        </div>
        <div
          class="dropdown-container main-dropdown-item"
          v-for="item in hierarchicalStructure"
          :key="item.tagId"
          @mouseenter="showChildren(item.tagId)"
          @mouseleave="hideChildren(item.tagId)"
        >
          {{ item.name }}
          <div class="arrow" v-if="shouldShowArrow(item)">
            <img src="../assets/gray-arrow.png" alt="gray arrow" class="gray-arrow" />
            <img src="../assets/orange-arrow.png" alt="orange arrow" class="orange-arrow" />
          </div>
          <div v-if="item.showChildren" class="dropdown-children">
            <div class="main-dropdown-item" v-for="child in item.children" :key="child.tagId">
              {{ child.name }}
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
    transition: opacity 0.3s ease, display 0s 0.3s;
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








  .dropdown-children {
    max-height: 200px; /* Set the maximum height you want */
    overflow-y: auto; /* Enable vertical scrolling when content overflows */
  }

</style>
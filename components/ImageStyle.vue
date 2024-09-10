<template>
  <div class="text-center">
    <div class="spinner-container" v-if="loading">
      <div class="spinner-border text-primary">
        <span class="visually-hidden"></span>
      </div>
    </div>
    <div class="grid-container" v-else>
      <div
        className="gif-item"
        v-for="(gif, index) in limitedImg"
        :key="index"
        @click="handleClick(index)"
      >
        <span class="absolute-center">
          <i
            class="fa-solid fa-circle-check icon-primary-color"
            v-if="showCheck[index]"
          ></i
        ></span>
        <div class="absolute-bottom">
          <button
            class="custom-btn-img"
            data-bs-toggle="tooltip"
            data-bs-placement="top"
            :title="gif.title"
          >
            {{ gif.title }}
          </button>
        </div>
        <img
          class="gif-item-image"
          :src="gif.images.fixed_height.url"
          :alt="gif.title"
        />
      </div>
    </div>
    <p
      class="mt-4 mb-0 text-underline text-primary text-center pointer"
      @click="toggleShowMore"
    >
      {{ showAll ? "แสดงน้อยลง" : "โหลดเพิ่ม" }}
    </p>
  </div>
</template>
<script setup>
import { fetchGIFs } from "@/services/api";
const initialWord = "naruto";
const allImg = ref([]);
const showCheck = ref([]);
const showAll = ref(false);
const loading = ref(false);
const limit = ref(12);

const getFetchGIFs = () => {
  loading.value = true;
  fetchGIFs(initialWord)
    .then((res) => {
      allImg.value = res;
      showCheck.value = Array(res.length).fill(false);
    })
    .finally(() => {
      loading.value = false;
    });
};

const handleClick = (index) => {
  showCheck.value[index] = true;
  setTimeout(() => {
    showCheck.value[index] = false;
  }, 500);
};

const toggleShowMore = () => {
  showAll.value = !showAll.value;
};

const limitedImg = computed(() => {
  return showAll.value ? allImg.value : allImg.value.slice(0, limit.value);
});

onMounted(() => {
  getFetchGIFs();
});
</script>
<style scoped lang="scss">
.text-underline {
  text-decoration: underline;
}

.spinner-container {
  height: 260px;
  align-content: center;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;

  .gif-item {
    position: relative;
    text-align: center;
    border-radius: 8px;
    cursor: pointer;

    .absolute-center {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    .absolute-bottom {
      position: absolute;
      left: 50%;
      bottom: -4%;
      width: 95%;
      transform: translate(-50%, -50%);
    }

    .custom-btn-img {
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
      opacity: 0.7;
      background-color: #ffffff;
      border: 0px;
      border-radius: 8px;
      width: 100%;
    }

    .gif-item-image {
      border-radius: 8px;
      width: 100%;
      height: 200px;
      object-fit: cover;
    }

    &:hover {
      .icon-primary-color {
        color: #0d6efd;
      }

      .custom-btn-img {
        background-color: #0d6efd;
        color: #ffffff;
        opacity: 0.9;
      }
    }
  }

  @media (max-width: 600px) {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>

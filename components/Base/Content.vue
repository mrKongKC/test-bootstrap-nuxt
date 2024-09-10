<!-- collapse unable to use switch arrow animation
so I will use the own animation resolve this issue 
-->
<template>
  <div class="d-flex flex-column gap-1 w-100">
    <button
      @click="toggleCollapse"
      class="custom-header"
      :class="{ pointer: collapse }"
    >
      <h5 class="text-dark fw-bold">{{ title }}</h5>
      <span
        v-show="collapse"
        :class="{
          'rotate-animation': !isCollapseShown,
          'normal-form': isCollapseShown,
        }"
      >
        <i class="fa-solid fa-chevron-down"></i>
      </span>
    </button>
    <div v-if="collapse">
      <transition>
        <div
          v-if="isCollapseShown"
          class="mt-2"
        >
          <slot></slot>
        </div>
      </transition>
    </div>
    <div v-else>
      <slot></slot>
    </div>
  </div>
</template>
<script setup>
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  collapse: {
    type: Boolean,
    default: false,
  },
});

const isCollapseShown = ref(true);
const toggleCollapse = () => {
  if (props.collapse) {
    isCollapseShown.value = !isCollapseShown.value;
  }
};
</script>
<style scoped>
.custom-header {
  padding: 0;
  margin: 0;
  background-color: #ffffff;
  border: 0px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: default;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(180deg);
  }
}

.normal-form {
  transform: rotate(0deg) ease-in-out;
  transition: all 0.3s ease-in-out;
}

.pointer {
  cursor: pointer;
}

.rotate-animation {
  transform: rotate(180deg);
  animation: rotate 0.3s ease-in-out;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease-in-out;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>

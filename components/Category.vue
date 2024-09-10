<!-- I selected pure css Grid 
 because container row col class.
it's padding make the ui look quite not good enough -->
<template>
  <div class="grid-container">
    <div class="d-flex" v-for="(category, index) in categories" :key="index">
      <input
        type="checkbox"
        class="btn-check"
        :id="`grid-${index}`"
        autocomplete="off"
        :checked="index === 0"
        @change="handleCheck(index)"
      />
      <label
        class="btn btn-outline-primary w-100 gap-1 d-flex align-items-center justify-content-center py-2 px-3"
        :for="`grid-${index}`"
        style="height: 50px"
      >
        <i v-if="checkedIndexes.includes(index)" class="fa-solid fa-circle-check"></i>
        <p style="margin-bottom: 4px;" class="no-wrap">{{ category }}</p>
      </label>
    </div>
  </div>
</template>

<script setup>
const categories = [
  "การงาน",
  "การเงิน",
  "ความรัก",
  "สุขภาพ",
  "ความมั่นใจ",
  "ความสำเร็จ",
  "วาสนา",
  "ศัตรู",
  "ความหวัง",
  "ความสุข",
  "การเรียน",
  "หายนะ",
  "ครอบครัว/ญาติ",
  "ความเจริญ",
  "ชื่อเสียง",
  "โชคลาภ",
  "เสริมเสน่ห์",
  "อำนาจ/บารมี",
  "ตวามปลอดภัย",
  "เพื่อน/มิตรภาพ",
];

const checkedIndexes = ref([0]) 

const handleCheck = (index) => {
  if (checkedIndexes.value.includes(index)) {
    checkedIndexes.value = checkedIndexes.value.filter(i => i !== index)
  } else {
    checkedIndexes.value.push(index)
  }
}
</script>

<style scoped lang="scss">
.no-wrap{
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;

  @media (max-width: 600px) {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>

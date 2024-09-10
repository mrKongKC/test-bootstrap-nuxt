<template>
  <div id="size-component">
    <div class="d-flex gap-3 justify-content-center custom-flex">
      <div
        class="d-flex flex-column flex-fill"
        v-for="(size, index) in sizes"
        :key="index"
      >
        <input
          type="radio"
          class="btn-check"
          name="btnradio"
          :id="`btnradio${index}`"
          autocomplete="off"
          checked
        />
        <label
          class="btn btn-outline-primary w-100 d-flex align-items-center justify-content-between py-2 px-3"
          :for="`btnradio${index}`"
          style="height: 50px"
        >
          <span :class="[size.className]"></span>
          <p class="m-0">{{ size.title }}</p>
        </label>
      </div>
    </div>
  </div>
</template>
<script setup>
const sizes = [
  {
    title: "แนวตั้ง",
    className: "rectangle-vertical",
  },
  {
    title: "แนวนอน",
    className: "rectangle-horizontal",
  },
  {
    title: "จัตุรัส",
    className: "square",
  },
];
</script>
<style lang="scss">
#size-component {
  .custom-flex {
    @media (max-width: 426px) {
      flex-direction: column;
    }
  }
  .rectangle-vertical {
    display: inline-block;
    width: 14px;
    height: 30px;
    border: 2px solid #007bff;
    background-color: transparent;
  }

  .rectangle-horizontal {
    display: inline-block;
    width: 30px;
    height: 14px;
    border: 2px solid #007bff;
    background-color: transparent;
  }

  .square {
    display: inline-block;
    width: 20px;
    height: 20px;
    border: 2px solid #007bff;
    background-color: transparent;
  }

  .btn-check:checked + .btn,
  .btn.active,
  .btn.show,
  .btn:first-child:active,
  :not(.btn-check) + .btn:active {
    .rectangle-vertical,
    .rectangle-horizontal,
    .square {
      border: 2px solid #ffffff;
    }
  }
}
</style>

<template>
  <div class="p-4 h-100vh d-flex justify-content-center main-bg">
    <div
      class="d-flex overflow-scroll mx-container align-items-start justify-content-center h-container text-white shadow p-3 bg-body rounded"
    >
      <div class="d-flex flex-column gap-4 w-100 p-4">
        <BaseContent title="ขนาด">
          <ScreenSize />
        </BaseContent>
        <BaseContent title="หมวดหมู่" collapse>
          <Category />
        </BaseContent>
        <BaseContent title="สไตล์ภาพ" collapse>
          <ImageStyle />
        </BaseContent>
      </div>
    </div>
  </div>
</template>
<style>
html,
body {
  height: 100vh;
  overflow: hidden;
  box-sizing: border-box;
}

.pointer {
  cursor: pointer;
}

.h-100vh {
  height: 100vh;
}

.overflow-scroll {
  scrollbar-width: none;
  overflow: scroll;
}

.overflow-scroll::-webkit-scrollbar {
  display: none;
}

.main-bg {
  overflow: hidden;
  background: #d3d3d7;
}

.mx-container {
  max-width: 550px;
  width: 100%;
}

.h-container {
  height: calc(100dvh - 72px);
}
</style>

<template>
  <button class="add__btn" @click="$emit('openModal')">
    <img src="@/assets/img/edit.svg" alt="add" />
  </button>
</template>

<script>
export default {};
</script>

<style>
.add__btn {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 16px;
  width: 56px;
  height: 56px;
  position: fixed;
  right: 30px;
  bottom:30px;
}
</style>
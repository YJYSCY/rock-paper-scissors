<template>
  <div class="card">
    <p>{{ card.value }}</p>
    <p>{{ card.suit }}</p>
  </div>
</template>

<script>
export default {
  props: ['card'],
};
</script>

<style scoped>
.card {
  /* 样式定义 */
  width: 60px;
  height: 90px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 1px solid #000;
  margin: 5px;
  font-size: 24px;
}
</style>

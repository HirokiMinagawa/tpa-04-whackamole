<template>
  <div class="counter">
    <h2>{{ this.title }}</h2>
    <h1>{{ this.number }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Counter',
  props: ['number', 'title'],
};
</script>

<style>
.counter {
  border: 1px solid #000;
  margin-top: 20px;
  padding: 20px;
}

.counter h1,
.counter h2 {
  margin: 0;
}
</style>

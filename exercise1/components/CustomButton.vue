<template>
  <touchable-opacity class="list-button">
    <text>{{ item.id }}. {{ item.text }}</text>
  </touchable-opacity>
</template>

<script>
export default {
  props: {
    item: {
      Type: Object,
    },
  },
}
</script>

<style>
.list-button {
    
  border-color: red;
  border-style: solid;
  border-radius: 5;
  border-width: 2;
  padding: 10px;
}
</style>

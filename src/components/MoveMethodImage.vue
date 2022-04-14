<template>
  <div>
    <v-img
      v-if="method == 'level-up'"
      :src="require('../assets/level-up.png')"
      width="30px"
    ></v-img>
    <v-img
      v-else-if="method == 'egg'"
      :src="require('../assets/egg.png')"
      width="30px"
    ></v-img>
    <v-img
      v-else-if="method == 'machine'"
      :src="require('../assets/book.png')"
      width="30px"
    ></v-img>
    <v-img
      v-else-if="method == 'tutor'"
      :src="require('../assets/teacher.png')"
      width="30px"
    ></v-img>
  </div>
</template>

<script>
export default {
  props: {
    method: String,
  },
};
</script>

<style lang="scss" scoped></style>

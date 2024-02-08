<script>
export default {
  name: "Header",
  created() {},
  data() {
    return {};
  },
  props: {},
  methods: {},
};
</script>

<template>
  <header>
    <div class="container">
      <div class="logo">
        <img src="/src/assets/logo.png" alt="">
      </div>
    </div>
  </header>
</template>


<style lang="scss" scoped>
  .container {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    .logo {
      width: 300px;
    }
  }
</style>
<template>
  <div class="container">
    <div class="leftBox">
      <left-frame></left-frame>
    </div>
    <div class="rightBox">
      <right-frame></right-frame>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomePageIndex",
  components: {
    LeftFrame: () => import("./leftFrame"),
    RightFrame: () => import("./rightFrame"),
  },
  data() {
    return {};
  },
  mounted() {},
  methods: {},
};
</script>
<style lang='scss' scoped>
.container {
  height: calc(100vh);
  display: flex;
  overflow: hidden;
  .leftBox {
    flex: 1;
     padding: 20px;
    border-right: solid 2px blue;
  }
  .rightBox {
    flex: 1;
    padding: 20px;
  }
}
</style>
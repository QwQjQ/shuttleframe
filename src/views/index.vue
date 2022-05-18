<template>
  <div>
    <shuttleFrame :leftList="leftList" :rightList="rightList"></shuttleFrame>
  </div>
</template>

<script>
import shuttleFrame from "../components/shuttle-frame.vue";

export default {
  name: "WorkspaceJsonIndex",
  components: {
    shuttleFrame
  },
  data() {
    return {
      leftList: ["111", "222", "333", "444", "555"],
      rightList: ["111", "222", "333", "444", "555"]
    };
  },

  mounted() {},

  methods: {}
};
</script>

<style lang="scss" scoped>
</style>
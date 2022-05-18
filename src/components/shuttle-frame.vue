<template>
  <div class="container">
    <div class="leftFrame">
      <div class="SearchBox">
        <input type="text" placeholder="请输入" />
      </div>

      <div v-for="(item,index) in leftList" :key="index">
        <div class="leftListItem">
          <input type="checkbox" value="item" />
          <span>{{item}}</span>
        </div>
      </div>
    </div>

    <div class="rightFrame">
      <div class="SearchBox">
        <input type="text" placeholder="请输入" />
      </div>
      <div v-for="(item,index) in rightList" :key="index">
        <div class="rightListItem">
          <p>
            <input type="checkbox" value="item" />
            {{item}}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "shuttle-frame",

  props: {
    leftList: {
      type: Array,
      default: function() {
        return [];
      }
    },
    rightList: {
      type: Array,
      default: function() {
        return [];
      }
    }
  },
  data() {
    return {
      // 左边参数列表
      //   leftList: [],
      // 右边参数列表
      //   rightList: []
    };
  },

  mounted() {
    console.log(this.leftList);
    console.log(this.rightList);
  },

  methods: {}
};
</script>

<style lang="scss" scoped>
</style>
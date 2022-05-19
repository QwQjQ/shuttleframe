<template>
  <div class="container">
    <!--左边穿梭框-->
    <div class="leftFrame">
      <div class="SearchBox">
        <input type="text" placeholder="请输入" />
      </div>
      <div v-for="(item,index) in leftList" :key="index">
        <div class="leftListItem">
          <p>
            <input type="checkbox" name="leftCheckbox" value="item" />
            {{item}}
          </p>
        </div>
      </div>
    </div>
    <!--中间按钮框-->
    <div class="centerFrame">
      <div class="centerBtn">
        <button
          class="btnMoveRight"
          @click="moveRight"
          @mouseover="mouseoverMoveRight"
          @mouseout="mouseoutMoveRight"
        >&gt;</button>
        <button class="btnMoveLeft" @click="moveLeft">&lt;</button>
      </div>
    </div>
    <!--右边穿梭框-->
    <div class="rightFrame">
      <div class="SearchBox">
        <input type="text" placeholder="请输入" />
      </div>
      <div v-for="(item,index) in rightList" :key="index">
        <div class="rightListItem">
          <p>
            <input type="checkbox" name="rightCheckbox" value="item" />
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

  methods: {
    // 获取左边选中的参数
    getLeftChecked() {
      let leftChecked = [];
      let leftCheckbox = document.getElementsByName("leftCheckbox");
      for (let i = 0; i < leftCheckbox.length; i++) {
        if (leftCheckbox[i].checked) {
          leftChecked.push(leftCheckbox[i].value);
        }
      }
      return leftChecked;
    },

    // 获取右边的参数
    getRightChecked() {
      let rightChecked = [];
      let rightCheckbox = document.getElementsByName("rightCheckbox");
      for (let i = 0; i < rightCheckbox.length; i++) {
        if (rightCheckbox[i].checked) {
          rightChecked.push(rightCheckbox[i].value);
        }
      }
      return rightChecked;
    },

    // 判断是否有选中的参数
    isChecked: function(arr) {
      for (let i = 0; i < arr.length; i++) {
        if (arr[i].checked) {
          return true;
        }
      }
      return false;
    },

    // 向右移动点击事件
    moveRight: function() {
      // 获取左边选中的参数
      let leftChecked = this.getLeftChecked();
      // 判断左边是否有选中的参数
      if (leftChecked.length == 0) {
        // 获得btnMoveRight[0]
        let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
        // 设置btnMoveRight的disabled属性为true
        btnMoveRight.disabled = true;
        return;
      }
    },
    // 向左移动点击事件
    moveLeft: function() {},

    // 鼠标移入btnMoveRight事件
    mouseoverMoveRight: function() {
      // 获得左边的参数
      let leftChecked = this.getLeftChecked();
      // 获得btnMoveRight[0]
      let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
      // 判断leftChecked是否有选中的参数
      if (this.isChecked(leftChecked)) {
        // 设置btnMoveRight的disabled属性为false
        console.log(leftChecked);
        btnMoveRight.disabled = false;
      } else {
        console.log("true" + leftChecked);
        // 设置btnMoveRight的disabled属性为true
        btnMoveRight.disabled = true;
      }
    },
    // 鼠标移出btnMoveRight事件
    mouseoutMoveRight: function() {
      // 获得btnMoveRight[0]
      let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
      // 设置btnMoveRight的disabled属性为false
      btnMoveRight.disabled = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 500px;
  background-color: #fff;
}
.leftFrame {
  width: 40%;
  height: 100%;
  background-color: red;
}
.centerFrame {
  width: 20%;
  height: 100%;
  background-color: green;
}
.rightFrame {
  width: 40%;
  height: 100%;
  background-color: skyblue;
}
</style>
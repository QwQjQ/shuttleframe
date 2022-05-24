<template>
  <div class="container">
    <!--左边穿梭框-->
    <div class="leftFrame">
      <div class="SearchBox">
        <input type="text" placeholder="请输入" />
      </div>
      <div v-for="(item,index) in shuttleLeftList" :key="index">
        <div class="leftListItem">
          <p>
            <input type="checkbox" @change="leftCheckChange" name="leftCheckbox" :value="item" />
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
      <div v-for="(item,index) in shuttleRightList" :key="index">
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
      // 左边列表
      shuttleLeftList: this.leftList,
      // 右边列表
      shuttleRightList: this.rightList,
      // 左边选中的参数列表
      leftChecked: [],
      // 右边参数列表
      rightChecked: []
    };
  },

  mounted() {
    console.log(this.leftList);
    console.log(this.rightList);
  },

  methods: {
    // 获取左边选中的参数
    getLeftChecked: function() {
      this.leftChecked = [];
      // 获取左边的复选框元素
      let leftCheckbox = document.getElementsByName("leftCheckbox");
      for (let i = 0; i < leftCheckbox.length; i++) {
        if (leftCheckbox[i].checked) {
          console.log(leftCheckbox[i].value);
          // 添加到左边选中的参数列表
          this.leftChecked.push(leftCheckbox[i].value);
        }
      }
      return;
    },

    // 获取右边的参数
    getRightChecked: function() {
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
      this.getLeftChecked();
      // 获得btnMoveRight[0]
      let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
      console.log("this.leftChecked", this.leftChecked);
      // 判断左边是否有选中的参数
      if (this.leftChecked.length == 0) {
        // 设置btnMoveRight的disabled属性为true
        btnMoveRight.disabled = true;
        return;
      } else {
        // 获取左边的复选框元素
        let leftCheckbox = document.getElementsByName("leftCheckbox");
        let index = 0;
        for (let i = 0; i < leftCheckbox.length; i++) {
          if (leftCheckbox[i].checked) {
            this.shuttleRightList.push(leftCheckbox[i].value);
            if (index >= 1) {
              this.shuttleLeftList.splice(i - index, 1);
            } else {
              this.shuttleLeftList.splice(i, 1);
            }
            index++;
          }
        }

        console.log("shuttleLeftList", this.shuttleLeftList);
        // 设置btnMoveRight的disabled属性为false
        // btnMoveRight.disabled = false;
      }
    },
    // 向左移动点击事件
    moveLeft: function() {},

    // 鼠标移入btnMoveRight事件
    mouseoverMoveRight: function() {
      // 获得左边的参数
      this.getLeftChecked();
      // 获得btnMoveRight[0]
      let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
      // 判断leftChecked是否有选中的参数
      if (this.isChecked(this.leftChecked)) {
        // 设置btnMoveRight的disabled属性为false
        console.log(this.leftChecked);
        // btnMoveRight.style.cursor = "not-allowed";
        // btnMoveRight.disabled = false;
      } else {
        console.log("true" + this.leftChecked, btnMoveRight);
        // 设置btnMoveRight的disabled属性为true
        // btnMoveRight.style.cursor = "not-allowed";
      }
    },
    // 鼠标移出btnMoveRight事件
    mouseoutMoveRight: function() {
      // 获得btnMoveRight[0]
      let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
      console.log("执行了移出事件");
      // 设置btnMoveRight的disabled属性为false
      // btnMoveRight.disabled = false;
      btnMoveRight.style.cursor = "allowed";
    },
    // 左边复选改变事件
    leftCheckChange: function() {
      this.getLeftChecked();
      console.log("this.leftChecked", this.leftChecked);
      // 获得向右移动按钮元素
      let btnMoveRight = document.getElementsByClassName("btnMoveRight")[0];
      // 获得左边的参数
      if (this.isChecked(this.leftChecked)) {
        // 设置btnMoveRight的disabled属性为false
        console.log("有参数", this.leftChecked);
        btnMoveRight.style.backgroundColor = "red";
      } else {
        btnMoveRight.style.backgroundColor = "#ffffff";
      }
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
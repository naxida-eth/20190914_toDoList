<template>
  <div class="toDo">
    <div class="toDoList">
      <h1>
        <p>正在进行的项目</p>
        <span>{{DoListLength}}</span>
      </h1>
      <ul>
        <li v-for="doItem in DoList" :key="doItem.id">
          <button v-on:click="checkItem(doItem.isOver,doItem.id)"></button>
          <p>{{doItem.addDoItem}}</p>
          <a href="javascript:" v-on:click="deleteItem(doItem.isOver,doItem.id)">-</a>
        </li>
      </ul>
    </div>
    <div class="overList">
      <h1>
        <p>已经完成</p>
        <span>{{OverListLength}}</span>
      </h1>
      <ul>
        <li v-for="overItem in OverList" :key="overItem.ids">
          <button v-on:click="checkItem(overItem.isOver,overItem.id)"></button>
          <p>{{overItem.addDoItem}}</p>
          <a href="javascript:" v-on:click="deleteItem(overItem.isOver,overItem.id)">-</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "index",
  props: ["addDoItem"],
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      // DoList：准备做的项目对象数组
      DoList: [],
      // OverList：已经做完的项目对象数组
      OverList: [],
      // DoListLength：准备做的项目对象数组长度
      DoListLength: 0,
      // OverListLength：已经做完的项目对象数组长度
      OverListLength: 0
    };
  },
  mounted() {},
  methods: {
    pushItem(addDoItem) {
      let me = this;
      let isOver = false;
      me.DoListLength = me.DoList.length + 1;
      let id = me.DoListLength;
      me.DoList.push({ // addDoItem : 项目具体内容 ,isOver : 判断是否已经完成项目 false 未完成 true 完成
        id: id,
        addDoItem: addDoItem,
        isOver: isOver
      });
    },
    checkItem(isOver, id) {
      let me = this;
      let doList = me.DoList;
      let overList = me.OverList;
      let removeItem = "";
      let doItem = "";
      if (isOver == false) {
        removeItem = doList.splice(id - 1, 1);
        removeItem[0].id = overList.length + 1;
        removeItem[0].isOver = true;
        me.DoList = [];
        me.OverList.push(removeItem[0]);
        me.OverListLength = me.OverList.length;
        for (let i = 0, len = doList.length; i < len; i++) {
          me.DoList.push({
            id: i + 1,
            addDoItem: doList[i].addDoItem,
            isOver: doList[i].isOver
          });
        }
        me.DoListLength = me.DoList.length;
      } else {
        doItem = overList.splice(id - 1, 1);
        doItem[0].id = doList.length + 1;
        doItem[0].isOver = false;
        me.OverList = [];
        me.DoList.push(doItem[0]);
        me.DoListLength = me.DoList.length;
        for (let i = 0, len = overList.length; i < len; i++) {
          me.OverList.push({
            id: i + 1,
            addDoItem: overList[i].addDoItem,
            isOver: overList[i].isOver
          });
        }
        me.OverListLength = me.OverList.length;
      }
    },
    deleteItem(isOver, id) {
      let me = this;
      let returnItem = "";
      let doList = me.DoList;
      let overList = me.OverList;
      if (isOver == false) {
        returnItem = doList.splice(id - 1, 1);
        me.DoList = [];
        for (let i = 0, len = doList.length; i < len; i++) {
          me.DoList.push({
            id: i + 1,
            addDoItem: doList[i].addDoItem,
            isOver: doList[i].isOver
          });
        }
        me.DoListLength = me.DoList.length;
      } else {
        returnItem = overList.splice(id - 1, 1);
        me.OverList = [];
        for (let i = 0, len = overList.length; i < len; i++) {
          me.OverList.push({
            id: i + 1,
            addDoItem: overList[i].addDoItem,
            isOver: overList[i].isOver
          });
        }
        me.OverListLength = me.OverList.length;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.toDo {
  display: warp;
  width: 100%;
  min-width: 600px;
  justify-content: center;
  align-items: center;
}
.toDo .toDoList,
.toDo .overList {
  display: flex;
  width: 52%;
  margin: auto;
  margin-top: 24px;
  min-width: 600px;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
}
.toDo .toDoList h1,
.toDo .overList h1 {
  display: flex;
  width: 100%;
  height: 60px;
  background: #4f7facf6;
  justify-content: space-between;
  align-items: center;
}
.toDo .toDoList h1 p,
.toDo .overList h1 p {
  margin-left: 20px;
}
.toDo .toDoList h1 span,
.toDo .overList h1 span {
  width: 40px;
  height: 40px;
  margin-right: 20px;
  line-height: 40px;
  background: #6299cca9;
  border-radius: 50%;
}
.toDo .toDoList h1 span {
  background: #706050ec;
}
.toDo .toDoList ul,
.toDo .overList ul {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  align-content: space-around;
  justify-content: space-around;
}
.toDo .toDoList ul li,
.toDo .overList ul li {
  position: relative;
  display: flex;
  width: 98%;
  height: 40px;
  margin-top: 12px;
  border-bottom: 2px solid #4cb86c;
  line-height: 40px;
  list-style: none;
  flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
}
.toDo .overList ul li {
  border-bottom: 2px solid #706050ec;
}
.toDo .toDoList ul li button,
.toDo .overList ul li button {
  position: absolute;
  left: 12px;
  width: 22px;
  height: 22px;
  border: 0;
  cursor: pointer;
}
.toDo .overList ul li button {
  background: #706050ec;
}
.toDo .toDoList ul li a,
.toDo .overList ul li a {
  position: absolute;
  right: 12px;
  width: 20px;
  height: 20px;
  border: 4px solid #54cf5ed7;
  border-radius: 50%;
  background: #d3c0c0d2;
  line-height: 20px;
}
.toDo .overList ul li a {
  border: 4px solid #706050ec;
}
.toDo .overList h1 {
  background: #9e9a96;
}
</style>

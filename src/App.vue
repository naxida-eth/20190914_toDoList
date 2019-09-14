<template>
  <div id="app">
    <div class="header">
      <div class="header_box">
        <span>ToDoList</span>
        <input type="text" v-model="addDoItem" @change="ListPush(addDoItem)" placeholder="添加待办事项" />
      </div>
    </div>
    <router-view ref="index" :addDoItem="addDoItem"></router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      addDoItem:"",
    }
  },
  methods: {
    ListPush(addDoItem){
      let me =this;
      me.$refs.index.pushItem(addDoItem);
      me.addDoItem="";
    }
  },
};
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
a{
  text-decoration: none;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.header {
  width: 100%;
  min-width: 600px;
  background: rgba(26, 22, 22, 0.829);
}
.header .header_box {
  display: flex;
  width: 42%;
  height: 60px;
  margin: auto;
  min-width: 600px;
  justify-content: space-around;
  align-items: center;
}
.header .header_box span{
  font-size: 32px;
  color: aliceblue;
}
.header .header_box input{
  padding: 6px 0;
  width: 280px;
  height: 20px;
  border-radius: 10px;
  text-indent: 12px;
}
</style>

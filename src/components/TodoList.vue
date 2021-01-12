<template>
  <div id="todo-list">
    <nav-bar class="nav-bar">
      <div slot="left">Todo</div>
      <div slot="right">
        <input type="text" placeholder="请输入待办事件" class="input" v-model="inputValue" @keydown.enter="enterValue" @focusout="enterValue">
      </div>
    </nav-bar>
    <scroll class="content" ref="scroll">
      <list :list="doingList" @deleteEvent="deleteEvent" @change="change">
        <div slot="title">正在进行</div>
      </list>
      <list :list="doneList" @deleteEvent="deleteEvent" @change="change">
        <div slot="title">已经完成</div>
      </list>
    </scroll>
  </div>
</template>

<script>
import NavBar from "@/common/NavBar";
import List from "@/common/List";
import Scroll from "@/common/Scroll";
export default {
  name: "TodoList",
  components:{
    NavBar,
    List,
    Scroll
  },
  data(){
    return {
      inputValue:'',
      list:[],
    }
  },
  computed:{
    doingList(){
      return this.list.filter((item) => item.isDone == false)
    },
    doneList(){
      return this.list.filter((item) => item.isDone == true)
    }
  },
  methods:{
    save(){
      localStorage.list = JSON.stringify(this.list)
      this.$refs.scroll.refresh()
    },
    enterValue(){
      if(this.inputValue.length){
        let arr = this.doingList.find((item) => {
          return item.value == this.inputValue
        })
        if(arr){
          alert('事务已存在')
        }else{
          this.list.push({
            value: this.inputValue,
            isDone: false,
            id:this.list.length
          })
        }
      }
      this.save()
      this.inputValue = ''
    },
    deleteEvent(id){
      this.list.splice(id,1)
      for(let i in this.list){
        this.list[i].id = i
      }
      this.save()
    },
    change(id){
      this.list[id].isDone = !this.list[id].isDone
      this.save()
    }
  },
  mounted() {
    this.list = JSON.parse(localStorage.list)
  }
}
</script>

<style scoped>
  #todo-list{
    height: 100vh;
    position: relative;
  }
  .nav-bar{
    background: skyblue;
    color: white;
    font-size: 20px;
    font-weight: bold;
  }
  .content{
    position: absolute;
    top: 49px;
    bottom: 0;
    left: 0;
    right: 0;
  }
  .input{
    height: 26px;
    width: 220px;
    margin: 0 10px;
    padding: 5px;
    border: 1px solid white;
    border-radius: 5px;
    font-size: 14px;
    color: gray;
  }
</style>
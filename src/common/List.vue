<template>
<div id="list">
  <transition name="slide-fade">
    <div class="title" v-if="list.length">
      <slot name="title"></slot>
    </div>
  </transition>
  <transition-group name="slide-fade">
    <div v-for="(item,index) in list" :key="index" :class="['content',item.isDone? 'done':'']">
      <div class="check" @click="change(item.id)"></div>
      <div class="value">
        {{item.value}}
      </div>
      <div class="delete" @click="deleteEvent(item.id)">删除</div>
    </div>
  </transition-group>
</div>
</template>

<script>
  export default {
    name: "List",
    props:{
      list:{
        type:Array,
        default(){
          return []
        }
      }
    },
    methods:{
      deleteEvent(id){
        this.$emit('deleteEvent',id)
      },
      change(id){
        this.$emit('change',id)
      }
    }
  }
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all .3s linear;
}
.slide-fade-leave-active {
  transition: all .3s linear;
}
.slide-fade-enter, .slide-fade-leave-to
  /* .slide-fade-leave-active for below version 2.1.8 */ {
  transform: translateX(10px);
  transform: translateY(-10px);
  opacity: 0;
}
.title{
  padding: 5px;
  font-size: 16px;
  color:gray;
  font-weight: 520;
}
.content{
  padding: 8px;
  margin: 5px;
  display: flex;
  background: skyblue;
  border-radius: 10px;
  letter-spacing: 1px;
}
.done{
  background: lightgray;
}
.check{
  width: 14px;
  height: 14px;
  box-shadow: 0 0px 5px white;
  border-radius: 10px;
}
.value{
  flex: 1;
  padding: 0 10px;
  font-size: 14px;
  line-height: 16px;
  color: white;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.delete{
  width: 30px;
  font-size: 14px;
  color: white;
}
</style>
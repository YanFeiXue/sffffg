<template>
<li @mouseenter="isShow=true" @mouseleave="isShow=false" :class="{myClass:isShow}">
          <label>
            <input type="checkbox" :checked= "todo.isOver" @click="updateO"/>
            <span>{{todo.content}}</span>
          </label>
          <button class="btn btn-danger" v-show="isShow" @click="deleteO">删除</button>
        </li>
</template>

<script>
import PubSub from 'pubsub-js'
export default {
  name: '',
  props:{
    todo:Object,
    index:{
    type:Number,
    required:true
  },
  updateOne:Function,
  },
  data(){
    return{
      isShow:false
    }
  },
  methods:{
    updateO(){
      PubSub.publish('heihei',this.index)
    },
    deleteO(){
      this.$bus.$emit('deleteOne',this.index)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.myClass{
  background-color: hotpink;
}
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

</style>

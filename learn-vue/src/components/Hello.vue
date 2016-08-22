<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model='msg2' @keyup.enter="onenter">
    <ul id="remove">
      <li @click='clickme(item)' :class='{finnish:item.istrue}' v-for='item in items' >{{ item.label }}.{{ item.istrue }}</li>
    </ul>
    <button @click='remove'>删除所有数据</button>
  </div>
</template>

<script>
import Store from './store'
export default {
  data () {
    return {
      msg: 'Hello World!',
      items:Store.fetch(),
      msg2:''
    }
  },
  methods: {
    clickme:function(item){
       item.istrue = !item.istrue;
    },
    onenter:function(){
      this.items.push({
        label: this.msg2,
        istrue:false
      }),
      this.msg2='';
    }
  },
  watch: {
    items: {
      handler:function(items){
        Store.save(items)
      },
      deep:true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: #42b983;
}
.finnish{
  color:red;
  text-decoration: line-through;
}
</style>

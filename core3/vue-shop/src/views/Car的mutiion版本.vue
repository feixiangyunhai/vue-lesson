<template> 
  <div>
   <Header>购物车</Header>
    <div class="container">
      <label for="checkall">
         <span>全选</span>
         <input v-model="checkAll" class="inp" type="checkbox" id="checkall">
       </label>
       <ul>
         <li v-for='item in carlist' :key='item.id' class="car-item">
          
           <div>
            <input v-model='item.sele' type="checkbox" class="inp" >
           </div>
           <div>
             <p>{{item.name}}</p>
             <img :src="item.img"/>
           </div>
         </li>
       </ul>
    </div>
  </div>
</template>
<script>
import Header from '../components/Header'
import {mapState} from 'vuex'
export default {
   name: 'car',
  components:{
    Header
  },
  computed:{
    ...mapState(['carlist']),
    checkAll:{
      get(){
        return this.$store.getters.checkAllVal
      },
      set(val){ //只要checkAll改变就会触发set方法，下面每一项都要跟着这个值做改变
       // [name:'',id:'',sele: true,name:'',id:'',sele: false]
        //通过vuex的数据必须经过mutations去修改值
        // 全选值改变触发所有单选框改变的事件
       this.$store.commit('changeAll',val)
      }
    }
  }
}
</script>
<style scoped>
.inp{
  appearance: none; 
  width: 40px;
  height: 40px;
  border: 1px solid yellowgreen;
  outline: none;
  border-radius: 8px;
}
.inp:before{
   content: '';
   position: relative;
   left: 6px;
   top: 3px;
    width: 20px;
   height: 20px;
}
.inp:checked.inp:before{
  content: '✔';
  font-size: 28px;
  position: relative;
  color: yellowgreen;
  left: 6px;
  top: 3px;
  display: inline-block;
 
}
 car-item{
   display: flex;
   flex-direction: row
 }
</style>

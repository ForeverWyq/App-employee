<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
    <!-- 内容区域 -->
    <div>
      <!-- 订单n个 -->
      <briup-product-item 
      v-for="o in orders"
      :key="o.id" :data="o">
      </briup-product-item>
    </div>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import {get, post} from '../../http/axios';
export default {
  data(){
    return {
      categories:[],
      orders:[]
    }
  },
  computed:{
    ...mapState("user",["info"])
  },
  created(){
    // 查询订单
    this.loadorders();
  },
  methods:{
    // 加载待接单信息
    loadorders(){
      let url = "/order/query"
      let params={
        waiterId:this.info.id,
        status:"待接单"
      }
      get(url,params).then((response)=>{
        this.orders=response.data;
      })
    }
  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>
<template>
  <div class="order_item">
    <van-row class="header"> 
      <van-col span="12">订单编号: {{data.id}}</van-col>
      <van-col span="12" class="status">{{data.status}}</van-col>
    </van-row>
    <van-row>
      <van-col :span="24" :offset="1">
        <div v-if="data.waiter!=null">
          顾客姓名：{{data.customer.realname}}</div>
        <div v-if="data.waiter!=null">
          顾客联系方式：{{data.customer.telephone}}</div>
        <div>服务内容:
          <span v-for="line in data.orderLines" :key="line.id">
            {{line.product.name}}
          </span>
        </div>
        <div>服务时间：{{data.orderTime | datefmt}}</div>
        <div>服务地点：
          {{data.address.province}}
          {{data.address.city}}
          {{data.address.area}}
          {{data.address.address}}
        </div>
      </van-col>
    </van-row>
    <br>
    <div class="text-right">
        <van-button size="small" type="warning" plain 
        @click="rejectHandler(data.id)">拒绝</van-button>&nbsp;
        <van-button size="small" type="primary" plain 
        @click="acceptHandler(data.id)">接受</van-button>
    </div><br>
  </div>
</template>
<script>
import {get} from '../http/axios';
export default {
  props:{
    data:{type:Object}
  },
  methods:{
    acceptHandler(id){
        let url = "/order/takeOrder";
        let params={
          orderId:id
        }
        get(url,params).then(()=>{
          this.$router.push("/manager/order");
        })
    },
    rejectHandler(id){
        let url = "/order/rejectOrder";
        let params={
            orderId:id
        }
        get(url,params).then(()=>{
          this.$router.push("/manager/order");
        })
    }
  }
}
</script>
<style scoped>
.order_item {
  margin: .5em 1em;
  padding: .5em;
  border-radius: 5px;
  background: #ffffff;
}
.order_item .header {
  line-height: 2.5em;
  font-size: 14px;
}
.order_item .header .status {
  text-align: right;
  font-size: 12px;
  color: #fd621f;
}
.order_item img {
  width: 100%;
  border-radius: 3px;
}


</style>
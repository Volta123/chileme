<template lang="pug">
    div.carts
        el-table(:data='cartsList',border)
            el-table-column(prop="goodname",label="商品")
            el-table-column(prop="num",label="数量")
            el-table-column(prop="price",label="金额")
            el-table-column(prop="methods",label="操作")
                template(slot-scope="scope")
                    el-button(type="text",size="small",@click="deleteHandle(scope.row)") 删除
        el-divider
        el-button(type='danger' @click="deleteAllGoods") 清空
        el-button(type='success' @click="orderData") 结算 
</template>
<script>
export default {
    data(){
        return{}
    },
    props:['cartsList'],
    methods:{
        deleteHandle(row){
            console.log(row)
            console.log('-----------父')
            this.$emit('dianji',row)
        },
        deleteAllGoods(){
            this.Axios({
                method:'GET',
                url:'/api/carts/deteleAll'
            }).then(res=>{
                console.log(res)
                 this.$emit('shanchu')
            }).catch(err=>{
                console.log(err)
            })
        },
        orderData(){
             //axios的请求
            this.Axios({
                method:'POST',//请求方式
                url:'/api/order/addOrder',//请求地址
                // params:{},//请求携带的参数，若该请求不需要携带参数，则忽略
            }).then(res=>{//请求成功的回调函数  res请求返回的结果  res是从carts_controller.js里面的ctx.body来的
                console.log(res)
            }).catch(err=>{//请求失败的回调函数  err请求失败的返回结果
                console.log(err)
            })
        },
    }
}
</script>
<style lang="scss" scoped>
.el-table{
    width:90%;
    margin:auto;
}
</style>
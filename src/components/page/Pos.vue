<template>
  <div>
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width:100%;">
              <el-table-column prop="goodsName" label="商品名称" ></el-table-column>
              <el-table-column prop="count" label="数量" width="70"></el-table-column>
              <el-table-column prop="price" label="价格" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button type="text" size="small" @click="deleteGoodsList(scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addGoodsToList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger">删除</el-button>
              <el-button type="success">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">

          </el-tab-pane>
          <el-tab-pane label="外卖">

          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="17">
        <div class="title">常用商品</div>
        <div class="often-goods">
          <ul>
            <li v-for="(goods) in oftenGoods" v-bind:key="goods.value" @click="addGoodsToList(goods)">
              <span>{{goods.goodsName}}</span>
              <span class="o-price">￥{{goods.price}}元</span>
            </li>
          </ul>
        </div>
        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <div>
                <ul class='cookList'>
                  <li v-for="(food) in type0Goods" v-bind:key="food.value" @click="addGoodsToList(food)">
                      <span class="foodImg"><img :src="food.goodsImg" width="100%"></span>
                      <span class="foodName">{{food.goodsName}}</span>
                      <span class="foodPrice">￥{{food.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小食">
              <div>
                <ul class='cookList'>
                  <li v-for="(food) in type1Goods" v-bind:key="food.value" @click="addGoodsToList(food)">
                      <span class="foodImg"><img :src="food.goodsImg" width="100%"></span>
                      <span class="foodName">{{food.goodsName}}</span>
                      <span class="foodPrice">￥{{food.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <div>
                <ul class='cookList'>
                  <li v-for="(food) in type2Goods" v-bind:key="food.value" @click="addGoodsToList(food)">
                      <span class="foodImg"><img :src="food.goodsImg" width="100%"></span>
                      <span class="foodName">{{food.goodsName}}</span>
                      <span class="foodPrice">￥{{food.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <div>
                <ul class='cookList'>
                  <li v-for="(food) in type3Goods" v-bind:key="food.value" @click="addGoodsToList(food)">
                      <span class="foodImg"><img :src="food.goodsImg" width="100%"></span>
                      <span class="foodName">{{food.goodsName}}</span>
                      <span class="foodPrice">￥{{food.price}}元</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Pos',
  data () {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: []
    }
  },
  created: function () {
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods').then(response => {
      this.oftenGoods = response.data
    }).catch(reason => {
      alert('网络错误')
    })

    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods').then(response => {
      this.type0Goods = response.data[0]
      this.type1Goods = response.data[1]
      this.type2Goods = response.data[2]
      this.type3Goods = response.data[3]
    }).catch(reason => {
      alert('网络错误')
    })
  },
  mounted: function () {
    var orderHeight = document.body.clientHeight
    document.getElementById('order-list').style.height = orderHeight + 'px'
  },
  methods: {
    addGoodsToList (goods) {
      let isHave = false
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId === goods.goodsId) {
          isHave = true
        }
      }

      if (isHave) {
        let arr = this.tableData.filter(o => o.goodsId === goods.goodsId)
        arr[0].count++
      } else {
        let newGoods = {goodsId: goods.goodsId, goodsName: goods.goodsName, count: 1, price: goods.price}
        this.tableData.push(newGoods)
      }
    },
    deleteGoodsList (goods) {
      if (goods.count > 1) {
        goods.count--
      } else {
        this.tableData.pop(goods)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pos-order{
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}
.div-btn{
  margin-top: 10px;
}
.title{
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
  text-align: left;
}
.often-goods ul li{
  list-style: none;
  float: left;
  border:1px solid #e5e9f2;
  padding: 10px;
  margin: 10px;
  background-color: #fff;
  cursor: pointer;
}
.o-price{
  color:#588fff;
}
.goods-type{
  clear: both;
}
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
       cursor: pointer;
}
.cookList li span{
    display: block;
    float:left;
}
.foodImg{
    width: 40%;
}
.foodName{
    font-size: 18px;
    padding-left: 10px;
    color:brown;

}
.foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top:10px;
}
</style>

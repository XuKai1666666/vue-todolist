<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="shop-stocks">
      <ol>库存清单：
        <ul v-for="cargo in cargoes" :key="cargo.name" :num="cargo.num">
          {{ cargo.name }}*******{{ cargo.num-cargo.num2 }}
        </ul>
      </ol>
    </div>
    <hr>
    <p>shop</p>
    <div id="shop-box" v-for="(cargo, index) in cargoes" :index="index" :key="cargo.name" :price="cargo.price" :num2="cargo.num2">
      <label :for=index>
        货物{{ index + 1 }}:{{ cargo.name }}￥{{ cargo.price }}元
      </label>
      <!-- <input type="checkbox" :id="cargo.index" :value="cargo" v-model="shopcart" /> -->
      <button @click="addToShopCart(cargo.num2,index)" >+</button> 
      数量：{{cargo.num2}}
      <button @click="subToShopCart(cargo.num2,index)" >-</button> 
      <br>
    </div>
    <br>
    <hr>
    <div id="shopcart-box">
      <table>
        <tr>
          <th>序号</th>
          <th>物品</th>
          <th>价格</th>
          <th>操作</th>
        </tr>
        <tr v-for="(cargo, index) in shopcart" :index="index" :key="cargo.name" :price="cargo.price">
          <td>{{ index + 1 }}</td>
          <td>{{ cargo.name }}</td>
          <td>{{ cargo.price }}元</td>

          <td><button @click="deleteTodo(index)">删除</button></td>
        </tr>
        <br>
        <tr>结算：￥{{ totalPrice }}元</tr>
      </table>
      get:value:{{ shopcart }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      cargoes: [
        { name: '啤酒', price: 3,num:10,num2:1 },
        { name: '花生', price: 6,num:10,num2:0 },
        { name: '瓜子', price: 5,num:10,num2:0 },
        { name: '香烟', price: 9,num:10,num2:0 }
      ],
      shopcart: [
        { name: '啤酒', price: 3,buynum:1 }
      ],
      //  counter:0,
    }
  },
  computed: {
    totalPrice() {
      var total = 0;
      for (var i = 0; i < this.shopcart.length; i++) {
        var item = this.shopcart[i];
        total += item.price;
      }
      return total;
    },
  },
  methods: {
    deleteTodo(index) {//
      this.shopcart.splice(index, 1)
    },
    // settlement() {
    //   //选择数量，确认后点击结算，计算总金额
    // },
    addToShopCart(num,index){//单品增加数量 --不得大于库存
    console.log(num,index)
      console.log(this.cargo)
      this.cargoes[index].num2++
      //添加到shopcart
      console.log(this.addToShopCart)
      console.log(this.shopcart)
      if(this.cargoes[index].num2<=this.cargoes[index].num){//如果购买的小于库存

      //将+选择的商品加入购物车中
      this.shopcart.push({
        name:this.cargoes[index].name,
        price:this.cargoes[index].price,
        buynum:this.cargoes[index].num2}
      
      )
      }else{
        alert('没有库存了')
        this.cargoes[index].num2--//超出库存时扳回库存值
      }
    },
    subToShopCart(num,index){//单品减少数量--不得小于0
     console.log(num,index)
     console.log(this.cargo)
       this.cargoes[index].num2--

       if(this.cargoes[index].num2>=0){//如果购买的小于库存
       //将-选择的商品在购物车中去除
       this.shopcart.shift({
        name:this.cargoes[index].name,
        price:this.cargoes[index].price,
        buynum:this.cargoes[index].num2
      })
      }else{
        this.cargoes[index].num2++//小于0时扳回0
      }
    }
  }

}

</script>

<style scoped>
.todolist-box {
  margin: auto;
}
</style>

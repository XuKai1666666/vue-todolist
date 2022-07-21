<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="shop-stocks">
      <ol>库存清单：
        <ul v-for="cargo in cargoes" :key="cargo.name" :num="cargo.num">
          {{ cargo.name }}*******{{ cargo.num - cargo.num2 }}
        </ul>
      </ol>
    </div>
    <hr>
    <p>shop</p>
    <div id="shop-box" v-for="(cargo, index) in cargoes" :index="index" :key="cargo.name" :price="cargo.price"
      :num2="cargo.num2">
      <label :for=index>
        货物{{ index + 1 }}:{{ cargo.name }}￥{{ cargo.price }}元
      </label>
      <!-- <input type="checkbox" :id="cargo.index" :value="cargo" v-model="shopcart" /> -->
      <button @click="addToShopCart(cargo.num2, index)">+</button>
      数量：{{ cargo.num2 }}
      <button @click="subToShopCart(cargo.num2, index)">-</button>
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
          <th>数量</th>
          <th>操作</th>
        </tr>
        <tr v-for="(cargo, index) in shopcart" :index="index" :key="cargo.name" :price="cargo.price"
          :buynum="cargo.buynum">
          <td>{{ index + 1 }}</td>
          <td>{{ cargo.name }}</td>
          <td>{{ cargo.price }}元</td>
          <td>{{ cargo.buynum }}</td>
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
        { name: '啤酒', price: 3, num: 10, num2: 1 },
        { name: '花生', price: 6, num: 10, num2: 3 },
        { name: '瓜子', price: 5, num: 10, num2: 0 },
        { name: '香烟', price: 9, num: 10, num2: 0 }
      ],
      shopcart: [
        { name: '啤酒', price: 3, buynum: 1 },
        { name: '花生', price: 6, buynum: 3 },

      ],
      //  counter:0,
    }
  },
  computed: {
    totalPrice() {
      var total = 0;
      for (var i = 0; i < this.shopcart.length; i++) {
        var item = this.shopcart[i];
        total += item.price * item.buynum;
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
    addToShopCart(num, index) {//单品增加数量 --不得大于库存
      // console.log(num, index)
      // console.log(this.cargo)
      this.cargoes[index].num2++
      //添加到shopcart
      // console.log(this.addToShopCart)
      // console.log(this.shopcart)

      if (this.cargoes[index].num2 <= this.cargoes[index].num) {//如果购买的小于库存
        console.log(this.shopcart)
        //判断数组中的Object中是否存在某个满足条件的元素
        console.log(this.shopcart.some(item => item.name === '啤酒'))
        //将+选择的商品加入购物车中
        if (this.shopcart.some(item => item.name === this.cargoes[index].name)) {//如果列表已经有此同名商品则buynum++
          // this.shopcart.buynum++
          console.log(this.shopcart.findIndex(item => item.name === this.cargoes[index].name))//找出数组中的object中存在那个元素的索引
          console.log(this.cargoes[index].name)

          //
          let shopcartindex = this.shopcart.findIndex(item => item.name === this.cargoes[index].name)
          this.shopcart[shopcartindex].buynum++
        }
        else {//列表没有此同名商品则 push整个object
          this.shopcart.push({
            name: this.cargoes[index].name,
            price: this.cargoes[index].price,
            buynum: this.cargoes[index].num2
          })
        }
      } else {
        alert('没有库存了')
        this.cargoes[index].num2--//超出库存时扳回库存值
      }
    },
    subToShopCart(num, index) {//单品减少数量--不得小于0
      console.log(num, index)
      console.log(this.cargo)
      this.cargoes[index].num2--


      if (this.cargoes[index].num2 >= 0) {//购买数量需大于等于0
        let shopcartindex = this.shopcart.findIndex(item => item.name === this.cargoes[index].name)//找出已购买商品的数组
        //如果列表已经有此同名商品,且购买的商品数量（buynum>1）大于1，则buynum--,
        if (this.shopcart.some(item => item.name === this.cargoes[index].name)&& this.shopcart[shopcartindex].buynum>1 ) {

          this.shopcart[shopcartindex].buynum--
        } else if(this.shopcart[shopcartindex].buynum==1 && this.shopcart.some(item => item.name === this.cargoes[index].name)) {
          //将-选择的数量为1的商品在shopcart中去除
          this.shopcart.splice (shopcartindex, 1)
        }
      } else {
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

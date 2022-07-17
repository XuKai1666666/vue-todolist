git <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="shop-box" v-for="(cargo, index) in cargoes" :index="index" :key="cargo.name" :price="cargo.price">
    
      <label for={{index}}>
        货物{{ index+1 }}:{{cargo.name}}￥{{cargo.price}}元
        
      </label>
      <input type="checkbox" 
      :id="cargo.index"  :value="cargo" v-model="shopcart"  />
    </div>
    <br>
    <hr>

    <div id="shopcart-box">
      <table >
        <tr>
          <th>序号</th>
          <th>物品</th>
          <th>价格</th>
          <th>操作</th>
        </tr>
        <tr v-for="(cargo, index) in shopcart" :index="index" :key="cargo.name" :price="cargo.price">
          <td>{{ index+1 }}</td>
          <td>{{ cargo.name }}</td>
          <td>{{ cargo.price }}元</td>
          <td><button @click="deleteTodo(index)">删除</button></td>
        </tr>
        <br>
        <tr >总价为{{totalPrice}}</tr>
      </table>
      get:value:{{shopcart}}
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
        { name: '啤酒', price: 3 },
        { name: '花生', price: 6 },
        { name: '瓜子', price: 5 },
        { name: '矿泉水', price: 2 }
      ],
      shopcart:[
        {name: '啤酒', price: 3 }
      ],
    }
  },
  computed: {
        totalPrice(){
            var total = 0;
            for(var i=0;i<this.shopcart.length;i++){
                var item = this.shopcart[i];
                total += item.price;
            }
            return total;
        },
    },
  methods: {
    deleteTodo(index) {
      this.shopcart.splice(index, 1)
    }
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todolist-box {
  margin: auto;
}
</style>

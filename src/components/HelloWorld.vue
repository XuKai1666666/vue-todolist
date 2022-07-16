git <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
<table class="todolist-box">
  <span>
    做什么：
    <input type="text" ref="getTextValue" @keyup.enter="addTodo">
    <input type="date" ref="getDateValue" @keyup.enter="addTodo">
    <button @click="addTodo" >添加</button>
  </span>
    <tr>
        <th>序号</th>
        <th>做什么</th>
        <th>什么时候做</th>
        <th>操作</th>
    </tr>
    <tr v-for="(todo,index) in todos"
        :index="index"
        :key="todo.text"
        :date="todo.tododate"
    >
        <td>{{index}}</td>
        <td>{{todo.text}}</td>
        <td>{{todo.tododate}}</td>
        <td><button @click="deleteTodo(index)">删除</button></td>
    </tr>
</table>
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
      todos: [
        { text: 'Learn JavaScript',tododate:'2020-1-1' },
        { text: 'Learn Vue',tododate:'2020-1-1'  },
        { text: 'Build something awesome',tododate:'2020-1-1'  }
      ],
    }
  },
  methods:{
    addTodo(){

      console.log( this.$refs.getTextValue.value)
      console.log( this.$refs.getDateValue.value)

      if(this.$refs.getTextValue.value=='' || this.$refs.getDateValue.value=='' ){
        alert('请输入有效值')
      }
      else{
      this.todos.push({
        text: this.$refs.getTextValue.value,
        tododate: this.$refs.getDateValue.value
      })
      }
      //清空输入区
      this.$refs.getTextValue.value= this.$refs.getDateValue.value='';
    },
    deleteTodo(index){
      this.todos.splice(index, 1)
    }
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todolist-box{
  margin:auto;
}
</style>

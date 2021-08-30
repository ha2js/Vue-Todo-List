<template>
<div class="container">
    <h2>Todo List</h2>
    <!-- 전체 삭제 버튼 넣기 -->
    <div class="input-group" style="margin-bottom:10px;">
        <input type="text" class="form-control" 
            placeholder="할일을 입력하세요" 
            v-model="name" 
            v-on:keyup.enter="createTodo(name)">
        <span class="input-group-btn">
            <button class="btn btn-default" type="button" 
            @click="createTodo(name)">추가</button>
        </span>
    </div>
    <ul class="list-group">
        <div v-if="flag">
        <li :key="index" class="list-group-item" v-for="(todo, index) in todos"> {{todo.name}}
	        <div class="btn-group pull-right" 
		    style="font-size: 12px; line-height: 1;">
		    <button type="button" 
		    class="btn-link dropdown-toggle" 
		    data-toggle="dropdown" 
		    aria-haspopup="true" 
		    aria-expanded="false">
			    더보기<span class="caret"></span>
		    </button>
		    <ul class="dropdown-menu">
                <li><a href="#">수정</a></li>
			    <li><a href="#" @click="deleteTodo(index)">삭제</a></li>
		    </ul>
	        </div>
        </li>
        </div>
        <div v-else-if="!flag" style="text-align:center; margin-top:50px;">
            <h3>등록된 정보가 없습니다</h3>
        </div>
    </ul>
</div>
</template>

<script>
export default {
  name: 'TodoPage',
  data () {
    return {
        flag:false,
        name: null,
        todos: []
    }
  },
  methods: {
      deleteTodo(i) {
          this.todos.splice(i,1);
          if (this.todos.length == 0) {
              this.flag = false;
          }
      },
      createTodo(name){
          if(name != null) {
              this.todos.push({name:name});
              this.name = null;
              if (this.flag == false) {
              this.flag = true;
            }
          }
          else {
              alert("입력하세요");
          }
      }
  }
}
</script>
<style>
</style>
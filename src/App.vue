<template>
    <article id="todo-list">
        <header class="header">
          <h1 class="header">Todos</h1>
          <input class="new-todo"
                placeholder="What needs to be done?"
                v-model = "newTodo"
                @keyup.enter="addNewTodo">
        </header>
        <todos-list v-show="isTodos"
                    :todoLists = "todoList"
                    :remains = "remaining"
                    @toggleCompleteThis = "toggleCompleteOne"
                    @deleteThis = "deleteOneTodo"
                    @toggleAllEve = "completeAllTodos">
                    </todos-list>
        <todo-footer v-show = "isTodos"
                    :remainings = "remaining"
        ></todo-footer>
    </article>
</template>

<script>
    import todosList from './component/todos-list.vue';
    import todoFooter from './component/todo-footer.vue';

    export default {
        name: 'todo-list',
        data () {
            return {
                isTodos: false,
                newTodo: '',
                todoId: 0,
                todoList: []
            }
        },
        components: {
            todosList,
            todoFooter
        },
        computed: {
            remaining: function(){
                return this.todoList.filter(function(todo){
                    return !todo.todoDone;
                })
            }
        },
        methods: {
            addNewTodo: function(){
                var newVal = this.newTodo && this.newTodo.trim();
                if( newVal ){
                    this.isTodos = true;
                    this.todoList.push({
                        todoId: this.todoId++,
                        todoTitle: newVal,
                        todoDone: false
                    });
                    this.newTodo = '';
                }
            },
            toggleCompleteOne: function(arg){
                this.todoList[arg].todoDone = !this.todoList[arg].todoDone;
            },
            deleteOneTodo: function(arg){
                this.todoList.splice(arg, 1);
            },
            completeAllTodos: function(arg){
                this.todoList.forEach(function(ele){
                    ele.todoDone = arg;
                })
            }
        },
        watch: {
            todoList: function(val){
                if(val.length === 0){
                    this.isTodos = false;
                }

            }
        }
    }
</script>

<style>
    body{font-family: 'Avenir', Helvetica, Arial, sans-serif; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale; color:#4d4d4d; background:#f5f5f5; line-height:1.4em;}
    #todo-list {position:relative; margin:130px auto 60px; max-width:550px; min-width:300px; text-align: center; color:#2c3e50; background:#fff; box-shadow:0 2px 4px 0 rgba(0,0,0,0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);}
    .header h1{position:absolute; top:-155px; width:100%; font-size:100px; font-weight:100; color:rgba(175,47,47,0.15);}
    .header .new-todo{padding:16px 16px 16px 60px; width:100%; font-size:24px; border:none; color:inherit; background:rgba(0,0,0,0.003); box-shadow:inset 0 -2px 1px rgba(0,0,0,0.03); box-sizing:border-box; outline:none;}
</style>

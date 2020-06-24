<template>
<div>


  <div class="container">
      <div class="row">
           <div class="col-12">
              <h1>Vue To-Do</h1>
            </div> 
      </div>
      <div class="row">
          <div class="col-1 col-lg-2"></div>
          <div class="col-10 col-lg-8">
              <h3>
              Add new Task 
             </h3>
             <h4 id="error">
                 {{error.length>1?error:""}}
             </h4>
          <form @submit.prevent="">
              
              <input v-model="addNewtodoString"  value="ss" id = "addinput" type="text" class="form-control addnew"><button class="btn btn-info p-6 m-3" @click.prevent="addTodo(addNewtodoString)">Add</button>
          </form>
           
          </div>
          <div class="col-1 col-lg-2"></div>
      </div>
      <div class="row">
          <div class="col-1 col-lg-2"></div>
          <div class="col-10 col-lg-8">
               <ul class="list-group">
                   <Todo
                   v-for="(todo, index) in todos" 
                   :key="index"
                   :todoString="todo.todoString"
                   :completed="todo.completed"
                   @on-delete="deleteTodo(todo)"
                   @on-toggle ="toggleTodo(todo)"
                   @on-edit = "editTodo(todo,$event)"
                   />
                  
               </ul>
          </div>
          <div class="col-1 col-lg-2"></div>
      </div>
     
  </div>
   <div class="footer">
          <h4>Created by Hardik </h4>
   </div>
  </div>
</template>

<script>
import Todo from "./indComp";

 //localStorage.setItem("todos", JSON.stringify([{todoString:"learn anguar",completed:false}]));
//var localTodo = JSON.parse(localStorage.getItem("todos"));
export default{
   
    components:{
        Todo
    },
    data(){
        var getData=()=>{
            if(localStorage.getItem("todos")!==null){
            return JSON.parse(localStorage.getItem("todos"));}
            else { console.log("in else");
                 localStorage.setItem("todos",JSON.stringify([{todoString:"learn vue",completed:false}]));
                  return [{todoString:"learn vue",completed:false}];
                  } 
        }
        return {
            error:"",
             addNewtodoString:"",
            todos:[
             ...getData()
            ]
        }
    },
    methods:{
        // getTodos(){
        //     return JSON.parse(localStorage.getItem("todos"));
        // },
        clearAll(){
            localStorage.clear();
            this.todos = [];
        },
        addTodo(newtodo){
            if(newtodo.length >2){
                console.log(this.todos.indexOf(newtodo));
                var strings = this.todos.map(w=>w.todoString);
                console.log(strings)
                if(strings.indexOf(newtodo) !== -1){
                    this.error = "task already exists";
                    return;
                }else {
          this.todos.push({
              todoString:newtodo,
              completed:false
          })
          localStorage.setItem("todos", JSON.stringify([...this.todos,{todoString:newtodo,completed:false}]));
          this.error = "";}
          }else {
              this.error = "task should be of atleast 3 characters long"
          }
          this.addNewtodoString = "";
        },
        toggleTodo(todo){
            //todo.completed = !todo.completed;
            this.todos = this.todos.filter(t=> {
                if(t == todo){
                    t.completed = !t.completed;
                }return true;
            });
           localStorage.setItem("todos",JSON.stringify(this.todos));
        },
        editTodo(todo,newtodo){
            todo.todoString = newtodo;
        },
        deleteTodo(todo){
            console.log(todo);
            this.todos = this.todos.filter(d=>d.todoString!==todo.todoString);
            localStorage.setItem("todos",JSON.stringify(this.todos));
        }
    }
}

</script>

<style>
body{
    margin: 0ch;
    padding: 0ch;
}
ul{
    text-decoration: none;
}
.addnew{
    display: inline;
  
}
h4{
    margin-bottom: 0ch;
    padding: 1rem;
    color: grey;
}
#error{
    color: #d44017 ;
   
}
.footer{
    margin-top: 5rem;
    height: 7rem;
    position: relative;
    margin-bottom: 0ch;
    padding: 0ch;
    background-color: rgb(66, 66,66);
}

#app{
    margin-top: 0ch;
    padding: 0ch;
    background: linear-gradient(326deg, #aeeedd, #c8e1f2, #ddc8f2, #f2c8de);
    background-size: 800% 800%;

    -webkit-animation: AnimationName 12s ease infinite;
    -moz-animation: AnimationName 12s ease infinite;
    animation: AnimationName 12s ease infinite;
}

@-webkit-keyframes AnimationName {
    0%{background-position:0% 99%}
    50%{background-position:100% 2%}
    100%{background-position:0% 99%}
}
@-moz-keyframes AnimationName {
    0%{background-position:0% 99%}
    50%{background-position:100% 2%}
    100%{background-position:0% 99%}
}
@keyframes AnimationName {
    0%{background-position:0% 99%}
    50%{background-position:100% 2%}
    100%{background-position:0% 99%}
}
</style>

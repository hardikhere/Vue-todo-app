<template>
    <li class="d-flex align-items-center list-group-item">
        <span id="number"></span>
        <button 
        id="text"
        v-if="!isEditing"
        :class ="{completed}"
        @click="$emit('on-toggle')"
        class="btn border-0 text-left flex-grow-1">
            {{todoString}}
        </button>
        <form  v-else @submit.prevent="endEditing()" class="felx-grow-1">
            <input id="text" @blur="startEditing()" v-model="newTodoString" type="text" class="form-control input"/>
        </form>
        <div v-if="!completed">
         <button @click="startEditing()" class="btn btn-success b"><i class="fa fa-pencil" aria-hidden="true"></i></button>
         <button @click="$emit('on-delete')" class="btn btn-danger b"><i class="fa fa-trash" aria-hidden="true"></i></button>
        </div>
        <div v-else>
         <span @click="startEditing()" ><i class="fa fa-check-circle" aria-hidden="true"></i></span>
        
        </div>
        
    </li>
</template>

<script>
export default {
    props:{
        todoString:String,
        completed:Boolean
    },
    data(){
        return {
            isEditing:false,
            newTodoString:"",
           
        }
    },
    methods:{
        startEditing(){
            if(!this.isEditing){
                this.newTodoString =this.todoString;
                this.isEditing = true;
            }else {
                this.endEditing();
            }
        
        },
        endEditing(){
            this.isEditing = false;
            this.$emit('on-edit',this.newTodoString)
        }
    }
}
</script>

<style scoped>

.completed{
    text-decoration: line-through;
    
}
.input{
    display: block;
    width:40vw;
}
#number{
    height: 0.6rem;
    width: 0.6rem;
    display: inline-block;
    border-radius: 30px;
    background-color: #41b883;
}
#text{
    font-size:1.5rem;
    color:rgb(66,66,66)
}
.b{ 
    margin: 0.4rem;
}
.fa-check-circle{
    font-size: 3rem;
    color: lightseagreen;
    margin: 0.4rem;
}
</style>
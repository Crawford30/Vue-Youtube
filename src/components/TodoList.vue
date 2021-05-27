<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
               <p class="display-3">Vue Crash Course</p>
            </div>
        </div>

        <div class="row">
            <!-- <p>Add Create Form</p> on receiving some information we call event-->

             <NewTodo @on-addtodo="addTodo($event)"/>
            <!-- <div class="col-12 col-lg-6">
                <NewTodo @on-addtodo="addTodo($event)"/>

            </div> -->
            
        </div>


        <div class="row">
            <!-- event pass from child to parent -->
            <div class="col-12 col-lg-6">
                <ul class="list-group">

                    <Todo v-for="(todo, index) in todos" 
                    :key="index" 
                    :todoString="todo.todoString"
                    :completed="todo.completed"
                    @on-delete="deleteTodo(todo)"
                    @on-toggle="toggleTodo(todo)"
                    @on-edit="editTodo(todo, $event)"

                    
                    
                    />
                </ul>
            </div>
        </div>
    </div>
 
</template>


<script>
import Todo from "./Todo.vue";
import NewTodo from "./NewTodo";


export default {
    components: {

     Todo,
     NewTodo
    },

    data(){

        return {
            todos: [
                {todoString: "Make Angular Crash Course", completed: false},
                {todoString: "Cook some food", completed: false},
                {todoString: "Make youtube videos", completed: true},
                {todoString: "Do some exercise", completed: false},
                {todoString: "Publish these videos", completed: true}

            ]
        };
    },

    methods: {
        addTodo(newTodo){
            this.todos.push({todoString:newTodo, completed:false

            });
        },

        //pass entire object
        toggleTodo(todo){
            todo.completed = !todo.completed;
        },
        editTodo(todo, newTodoString){
                   //if it has a property of todoString, it will be updated with newTodoString
            todo.todoString = newTodoString;
        },
        deleteTodo(deleteTodo){
            this.todos = this.todos.filter(
                //filters allows everybody but removes deleteTodo.todoString
                // todo => todo.todoString !== deleteTodo.todoString  

                //or 

                 todo => todo !== deleteTodo
                );
        },
    }

   

};

</script>

<style>

</style>
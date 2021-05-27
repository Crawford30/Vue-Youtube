<template>
<h1>
    <li class="d-flex align-items-center list-group-item">
        <button 
        v-if="!isEditing"
        :class="{completed}"
        @click="$emit('on-toggle')"
        
        class="btn border-0 text-left flex-grow-1">{{todoString}}</button>
    
    <form  v-else @submit.prevent="endEditing()" class="flex-grow-1">
        <!-- informing the input by modeling , by calling v-model-->
        <!-- @blur is executed when a user clicks outside -->
        <input @blur="startEditing()" v-model="newTodoString" type="text"  class="form-control">
    </form>

    <button @click="startEditing()" class="btn btn-outline-primary">Edit</button>
    <button @click="$emit('on-delete')" class="btn btn-outline-danger">Delete</button>

    </li>

</h1>
    
</template>


<script>
export default {

    props: {
        todoString: String,
        completed: Boolean

    },
    data() {
        return {
            isEditing: false,
            newTodoString: ""
        };
    },

    methods: {
        startEditing(){
            if(!this.isEditing){
                this.newTodoString = this.todoString; //todoString is coming from the props
                this.isEditing = true; //flip the switch
            }
            else {

                this.endEditing();

            }
        },
        endEditing(){
            this.isEditing = false;
            this.$emit('on-edit', this.newTodoString);
        },


    },
    
};
</script>


<style scoped>
.completed{
    text-decoration: line-through;
}

</style>
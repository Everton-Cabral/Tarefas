<template>
    <div class="new-task">
        <input v-model="name" @keydown.enter="add()" type="text" class="form-element" placeholder="Nova Tarefa?">
        <button @click="add()" class="form-element">+</button>
    </div>
</template>

<script>
export default {
    data(){
        return{
            name:''
        }
    },
    methods:{
        add(){
            this.$emit('taskAdded', {name: this.name})
            this.name = ''
        }
    }
}
</script>

<style>
    .new-task{
        margin:5% 5% 5% 5%; 
        width: 90%;
        display: flex;
        justify-content: center;
       
    }
    .form-element {
        outline: none;
        font-size: 2rem;
        border: 1px solid #fff;
        padding: 5px 10px 8px;
        color: #fff;
    }
    input.form-element {
        width: 50%;
        background: #fff2;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
    }
    button.form-element{
        border-left: none;
        background-color: #2196f3;
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }
   @media(max-width: 800px){
        input.form-element{
            width: 70%;
        }
   }
   @media(max-width: 700px){
        .form-element{
            font-size: 1.5rem;
        }
   }
   
</style>

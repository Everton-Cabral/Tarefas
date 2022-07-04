<template>
    <div 
        @click="$emit('taskStateChanged', task)"
        class="task" :class="seletorClass"> 
        <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
         {{task.name}}
    </div>
</template>

<script>
export default {
    props:{
        task:{type: Array, required: true}
    },
    computed: {
        seletorClass(){
            return{
                pending: this.task.pending,
                done: !this.task.pending
            }
        }
    }
}
</script>

<style>
    .task {
        position: relative;
        box-sizing: border-box;
        width: 350px;
        height: 100px;
        padding: 10px;
        border-radius: 8px;
        font-size: 1.5rem;
        font-weight: 300;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .pending {
        border-left: 12px solid #b73229;
        background-color: #f44336;
    }

    .done {
        color: #DDD;
        border-left: 12px solid #0a8f08;
        background-color: #4caf50;
        text-decoration: line-through;
    }
    .pending .close {
        background-color: #b73229;
    }
    .done .close {
        background-color: #0a8f08;
    }
    .close {
        position: absolute;
        right: 10px;
        top: 10px;
        font-size:0.9rem;
        font-weight:600;
        height: 20px;
        width: 20px;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        
    }
    @media(max-width: 700px){
        .task{
            height: 75px;
            font-size: 1rem;
        }
    }
</style>

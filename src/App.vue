<template>
	<div id="app">
		<h1>Tarefas</h1>
			<appTaskProgress :progress="progress"/>
			<appNewTask @taskAdded="addTask"/>
			<app-task-grid 
			@taskDeleted="deleteTask"
			@taskStateChanged="toggleTaskState"
			:tasks="tasks">
			</app-task-grid>
	</div>

</template>


<script>
import appTaskProgress from './components/TaskProgress'
import appNewTask from './components/NewTask'
import  appTaskGrid from './components/TaskGrid'
export default {
	components:{appTaskProgress, appTaskGrid, appNewTask},
	data(){
		return{
			tasks: []
		}
	},
	computed:{
		progress(){
			const total = this.tasks.length
			const done = this.tasks.filter( t => !t.pending).length
			return Math.round(done / total * 100) || 0
		}
	},
	watch: {
		tasks:{
			deep: true,
			handler(){
				localStorage.setItem('tasks', JSON.stringify(this.tasks))
			}
		}
	},
	methods: {
		addTask(task){
			const sameName = t => t.name === task.name
			const reallyNew = this.tasks.filter(sameName).length == 0
			if (reallyNew){
				this.tasks.push({
					name: task.name,
					pending: task.pending || true
				})
			}
		},
		deleteTask(task){
			const i = this.tasks.indexOf(task)
			if(i>=0) this.tasks.splice(i, 1)
			
		},
		toggleTaskState(i){
			this.tasks[i].pending = !this.tasks[i].pending
		}
	},
		created(){
			const json = localStorage.getItem('tasks')
			this.tasks = JSON.parse(json)
		} 
}
				
			
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
		margin: 0px 0px 0px 0px;
		
	}

	#app {
		width: 100%;
		height: auto;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		
		
	}

	#app h1 {
		margin-top: 10%;
	
		font-weight: 300;
		font-size: 3rem;
	}
</style>

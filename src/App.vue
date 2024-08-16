<template>
	<div id="app">
		<h1>Tasks</h1>
		<TasksProgress :progress="progress" />
		<NewTask @taskAdded="addTask($event)" />
		<TaskGrid 
			:tasks="tasks" 
			@taskDeleted="deleteTask($event)" 
			@taskStateChanged="toggleTaskState($event)"
		/>
	</div>
</template>

<script>
import TasksProgress from './components/TasksProgress.vue';
import NewTask from './components/NewTask.vue'
import TaskGrid from './components/TaskGrid.vue'
export default {
	name: 'App',
	components: {
		TasksProgress,
		NewTask,
		TaskGrid
	},
	data() {
		return {
			tasks: []
		}
	},
	computed: {
		progress() {
			const total = this.tasks.length
			const done = this.tasks.filter(t => !t.pending).length
			return Math.round(done / total * 100) || 0
		}
	},
	watch: {
		// irá ficar monitorando as tasks, sempre que for alterado, irá cair aqui
		// deep: true irá vasculhar profundamente as mudanças de estados do objeto
		tasks: {
			deep: true,
			handler() {
				localStorage.setItem('tasks', JSON.stringify(this.tasks))
			}
		}
	},
	methods: {
		addTask(task){
			const sameName = t => t.name === task.name
			const isNewTask = this.tasks.filter(sameName).length == 0

			if (isNewTask){
				this.tasks.push({
					name: task.name,
					pending: task.pending || true
				})

			}
		},
		deleteTask(index) {
			/* em caso de uma task como parametro
			   const index = this.tasks.indexOf(task)
			   if (index >= 0) this.tasks.splice(id, 1)
			 */
			this.tasks.splice(index, 1)
		},
		toggleTaskState(index) {
			this.tasks[index].pending = !this.tasks[index].pending
		}
	},
	created() {
		const json = localStorage.getItem('tasks')
		const array = JSON.parse(json)
		this.tasks = Array.isArray(array) ? array : []
	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
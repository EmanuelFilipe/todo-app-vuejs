<template>
    <div class="task-grid">
        <template v-if="tasks.length">
            <Task v-for="(task, index) in tasks" :key="task.name"
                @taskDeleted="$emit('taskDeleted', index)"
                @taskStateChanged="$emit('taskStateChanged', index)"
                :task="task">
            </Task>
        </template>
        <p v-else class="no-task">
            You don't have any tasks
        </p>
    </div>
</template>

<script>
import Task from './Task.vue'
    export default {
        name: 'TaskGrid',
        props: { 
            tasks: { type: Array, required: true }
        },
        components: {
            Task
        },
        created(){
        }
    }
</script>

<style scoped>
.task-grid {
    /* flex default is in row*/
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

.task-grid .task {
    margin: 10px;
}

.no-task {
    color: #AAA;
    font-size: 1.8rem;
}
</style>
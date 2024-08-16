<template>
    <div class="tasks-progress">
        <span class="progress-value">
            {{ progress }}%
        </span>
        <div class="progress-bar" :style="{width: progress + '%'}"></div>
    </div>
</template>

<script>
    export default {
       name: 'TasksProgress',
       props: {
        progress: {
            type: Number, required: true
        }
       }
    }
</script>

<style scoped>
    .tasks-progress {
        position: relative;
        width: 80%;
        border: 1px solid #fff;
        color: #fff;
        border-radius: 8px;
        margin-bottom: 15px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .progress-bar {
        position: absolute;
        height: 100%;
        background-color: #4caf50;
        align-self: flex-start;
        border-radius: 8px;
    }

    .progress-value {
        /* coloca o valor na frente */
        z-index: 1;
        font-size: 1.5rem;
    }
</style>
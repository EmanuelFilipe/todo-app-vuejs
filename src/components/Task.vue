<template>
    <div @click="$emit('taskStateChanged', task)" 
        class="task" :class="stateClass">
        <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
        <p>{{ task.name }}</p>
    </div>
</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: { type: Object, required: true }
        },
        //computa qual tipo da classe aplicar
        computed: {
            stateClass() {
                return {
                    pending: this.task.pending,
                    done: !this.task.pending
                }
            }
        }
    }
</script>

<style scoped>
.task {
    /* para o x do close */
    position: relative;
    box-sizing: border-box;
    width: 350px;
    height: 150px;
    padding: 10px;
    border-radius: 8px;
    font-size: 2rem;
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
    /* posicionar onde quiser */
    position: absolute;
    right: 10px;
    top: 10px;
    font-size: 1rem;
    font-weight: 600;
    height: 20px;
    width: 20px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    cursor: pointer !important;
}
</style>
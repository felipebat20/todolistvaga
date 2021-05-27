<template>
    <div>
         <div v-for="(task, index) in tasks" :key="index">
             <list-task
                :task="task" 
                class="task"
                v-on:taskchanged="$emit('reloadList')"
             />

         </div>
    </div>
</template>

<script>

import listTask from './listTask';

export default {
    props: ['tasks'], 
    components: {
        listTask
    }
}
</script>

<style scoped>
.task{
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}

</style>
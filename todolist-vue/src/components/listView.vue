<template>
    <div>
         <div v-for="(task, index) in tasks" :key="index">
             <list-task
                :task="task" 
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


</style>
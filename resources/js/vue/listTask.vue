<template>
    <div class="task">
        <input 
            type="checkbox"
            @change="updateCheck()"
            v-model="task.completed"

        />
        <span :class="[task.completed ? 'completed' : '', 'taskText']">{{ task.name }}</span>

        <button @click="removeTask()" class="trashcan">
            <font-awesome-icon icon="trash"/>
        </button>

    </div>
</template>

<script>
export default {
    props: ['task'],
    methods: {
        updateCheck(){
            axios.put('api/task/' + this.task.id, {
                task: this.task
            })
            .then( response => {
                if( response.status == 200 ) {
                    this.$emit('taskchanged');
                }
            })
            .catch( error=> {
                console.log(error);
            })
        },
        removeTask(){
             axios.delete('api/task/'+ this.task.id)
             .then( response => {
                if( response.status == 200 ) {
                    this.$emit('taskchanged');
             }
            })
            .catch( error=>{
                console.log("error");
            })
        }
    }
}
</script>

<style scoped>
.completed {
    text-decoration: line-through;
    color: #999999;

}
.taskText {
    width: 100%;
    margin: 5px;
    margin-left: 5px;
    font-size: 0.8em;


}
.task{
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
}
.trashcan {
    background: #e6e6e6;
    border: none;
    color: #FF0000;
    outline: none;
    cursor: pointer;
}
input{
    cursor: pointer;
}

</style>
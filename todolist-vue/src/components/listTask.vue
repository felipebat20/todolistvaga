<template>
    <div class="task">
        <input 
            type="checkbox"
            @change="updateCheck()"
            v-model="task.completed"

        />
        <input type="text" v-model="task.name" :class="[task.completed ? 'completed' : '', 'taskText']" :readonly="update == false" @keyup.enter="updateTask()">
        <button @click="startUpdate()" class="pencil" >
            <font-awesome-icon icon="pencil-alt"/>
        </button>
        <button @click="removeTask()" class="trashcan">
            <font-awesome-icon icon="trash"/>
        </button>

    </div>
</template>

<script>
import axios from 'axios';
export default {
    props: { task: { required: true, type: Object } },
    data(){
        return{
        update: false,
        nome: ""
        }
    },
    methods: {
        updateCheck(){
            axios.put('http://localhost:8080/api/task/' + this.task.id, {
                task: this.task
            })
            .then( response => {
                if( response.status == 200 ) {
                    this.$emit('taskchanged');
                }
                console.log(this.task);
            })
            .catch( error=> {
                console.log(error);
            })
        },

        startUpdate(){
            this.update = true;
        },

        
        updateTask(){

            if(this.task.name.trim() === ""){
                return;
            }
            
            axios.put('http://localhost:8080/api/task/' + this.task.id, {
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
            this.nome = "";
        },

        removeTask(){
             axios.delete('http://localhost:8080/api/task/'+ this.task.id)
             .then( response => {
                if( response.status == 200 ) {
                    this.$emit('taskchanged');
             }
            })
            .catch( error=>{
                console.log(error);
            })
        }
    },
    computed: {
        
    }

}
</script>

<style scoped>
input[type="checkbox"]{
    cursor: pointer;
}
input[type="text"]{
    cursor: pointer;
}
.completed {
    text-decoration: line-through;
    color: #999999;

}
.taskText {
    width: 100%;
    margin: 5px;
    margin-left: 5px;
    font-size: 1em;
    cursor: default;
    border: none;
    background: #e6e6e6;
}
.task{
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
    padding: 0.8em;
    background: #e6e6e6;
    margin-top: 5px;
}
.trashcan {
    background: #e6e6e6;
    border: none;
    color: #FF0000;
    outline: none;
    cursor: pointer;
}
.pencil{
    border: none;
    margin: auto 1em;
    font-size: 1em;
    color: blue;
    cursor: pointer;
}


</style>
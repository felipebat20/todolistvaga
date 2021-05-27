<template>
    <div class="todoListContainer"> 
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-task-form
                v-on:reloadList="getList()"
                />
        </div>
        <list-view 
            :tasks="tasks"
            v-on:reloadList="getList()"
            />
    </div>
</template>

<script>
import axios from 'axios';
import addTaskForm from './addTaskForm.vue'
import listView from './listView.vue'
export default {
    components:{
        addTaskForm,
        listView
    },
    data: function(){
        return {
            tasks: []
        }
    },
    methods:{
        getList (){
            axios.get('http://localhost:8080/api/tasks')
            .then( response =>   {
                this.tasks = response.data;
            })
            .catch( error => {
                console.log( error);
            })
        }
    },
    created(){
        this.getList();
    }
}

</script>

<style scoped>
    .todoListContainer{
        width: 500px;
        margin: 25px auto;

    }
    .heading{
        display: block;
        background: #e6e6e6;
        padding: 10px;
        border-radius: 5px;
        height: 100px;
        box-sizing: border-box;
    }
    #title{
        text-align: center;
    }
    .heading h2{
        font-family: 'Roboto', sans-serif;
        font-weight: 400;
        font-size: 28px;
        margin-top: 10px;
        padding: 10px;
    }
</style>